# Automated Market Sentiment Analysis News-Letter 

## Motivation 
To build an automated data pipeline to conduct market sentiment analysis on popular tech companies such as Meta, Google, Microsoft etc, and then 
broadcast summarized reports to subscribed users. 

## Architecture Diagram (Overview) 
1. Kafka produces data by querying the latest tweets surrounding topics related to the tech companies via X's (former Twitter) API.
2. Kafka then streams that data into Apache Spark Job, which processes the tweet and does market sentiment analysis on it.
    * As of right now, sentiment analysis and text-summarization are conducted using an LLM. (GPT 3.5/LLAMA)
3. The Spark job then produces results, writes it to another Kafka stream.
4. The last Spark job consumes the stream, and broadcasts the data to users via mail.
    
![Market Sentiment analysis workflow](https://github.com/oysters76/techms_newsletter/assets/75514064/f7345930-fbb9-46e8-b70d-43833e93fcfe)

## Future Work 

1. Add more spark jobs into the pipeline to do further sentiment analysis, and to collect market sentiment statistics.
2. Update a dashboard frontend (D3 JS/Apache Superset) in real-time with the data collected.

## Technologies used 
1. PySpark
2. Apache Kafka
3. X (Twitter) API
4. Python3

## Proposed Project Structure 
```
market_sentiment_analysis/
├── config/
│   ├── kafka_config.py
├── data/
│   ├── sample_data.json
├── logs/
│   └── app.log
├── src/
│   ├── __init__.py
│   ├── kafka_producer.py
│   ├── sentiment_analysis.py
│   ├── kafka_consumer.py
│   ├── spark_streaming.py
├── tests/
│   ├── __init__.py
│   ├── test_kafka_producer.py
│   ├── test_sentiment_analysis.py
│   ├── test_spark_streaming.py
├── requirements.txt
├── README.md
└── run.sh
```

