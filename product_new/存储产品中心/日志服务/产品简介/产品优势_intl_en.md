## Rich Features

- LogListener provides one-stop log service, including log collection, storage, search, transfer, and shipping features.
- LogListener parses the log structure in many ways, including full text in a single line, full text in multi lines, separator, JSON, and regular expressions.
- LogListener allows you to select from multiple data access methods based on your business needs. For more information, see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
- LogListener provides multiple search syntaxes and allows you to query logs by keyword, fuzzy match, or scope.

## Stable and Reliable

- CLS has a highly scalable distributed storage architecture. It supports horizontal expansion and automatic service scaling, and easily stores and manages massive log data.
- The CLS backend storage manages and stores logs in multiple copies, thereby reliably ensuring data security.

## Simple and Efficient

- LogListener can be configured simply and visual through a UI. You can quickly access CLS through LogListener.
- Data can be consumed immediately after being written to CLS. Query results of hundreds of millions of data records can be returned in seconds.
- The service is billed by actual usage. You do not need to build or maintain a log system, preventing resource idling and waste.

## Ecological Expansion

- The logs of certain cloud products have already been integrated into CLS. For more information, see [Access List](https://intl.cloud.tencent.com/document/product/614/12502#.E6.97.A5.E5.BF.97.E6.BA.90.E6.8E.A5.E5.85.A5).
- Logs are shipped to Cloud Object Storage (COS), which supports long-term archive storage of logs.
- Logs are shipped to CKafka, which supports real-time log consumption and facilitates further log processing and analysis.
