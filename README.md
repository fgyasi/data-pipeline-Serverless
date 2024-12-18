# Serverless Data Pipeline GCP

**Deploy an end to end data pipeline for Chicago traffic api data and measure function performance using: Cloud Functions, Pub/Sub, Cloud Storage, Cloud Scheduler, BigQuery, Stackdriver Trace**

**Usage:**

- Use this as a template for your data pipelines
- Use this to extract and land Chicago traffic data
- Pick and choose which modules/code snippets are useful
- Understand how to measure function performance throughout execution
- Show me how to do it better :)

**Data Pipeline Operations:**

1. Creates raw data bucket
2. Creates BigQuery dataset and raw, staging, and final tables with defined schemas
3. Downloads data from Chicago traffic API
4. Ingests data as pandas dataframe
5. Uploads pandas dataframe to raw data bucket as a parquet file
6. Converts dataframe schema to match BigQuery defined schema
7. Uploads pandas dataframe to raw BigQuery table
8. Run SQL queries to capture and accumulate unique records based on current date
9. Sends function performance metrics to Stackdriver Trace

**Technologies:** Cloud Shell, Cloud Functions, Pub/Sub, Cloud Storage, Cloud Scheduler, BigQuery, Stackdriver Trace

**Languages:** Python 3.7, SQL(Standard)

**Technical Concepts:**

- This was designed to be a python native solution and starter template for simple data pipelines
- This follows the procedural paradigm which groups like-functions in separate files and imports them as modules into the main entrypoint file. Each operation goes through ordered actions on objects vs. OOP in which objects perform the actions
- Pub/Sub is used as middleware as opposed to invoking an HTTP-triggered cloud function to minimize overhead code securing the URL in addition to Pub/Sub serving as a shock absorber to a sudden burst in invocations
- This is not intended for robust production deployment as it doesn't account for edge cases and dynamic error handling
- Lessons Learned: Leverage classes for interdependent functions and creating extensibility in table objects. I also forced stacktracing functionality to measure function performance on a pub/sub trigger, so you can't create a report based on http requests to analyze performance trends. Stackdriver Trace will start auto-creating performance reports once there's enough data.
