## Knowledge Graph-based Conversations
Traditional Q&A database is unable to intepret incomplete questions or handle excessive inquiries. Tencent Big Data AI team built operation models using field-specific knowledge graphs and then realized multi-round conversation system. The system uses natural language understanding technology to identify parts of customer intentions, search knowledge graph network and ask customers for explanations. The system also has context memory.

## Deep Migration Learning-based Learning Model and Cold Start Solution
TICSR integrates the traditional machine learning and deep learning models. Traditional machine learning model captures character matched information while deep learning model captures question semantic correlations. Having both of them makes the system more reliable regardless of data volumes.

Traditional customer service systems is based on question matching, has few similar questions, and is unable to train a stable model. TICSR's deep migration learning, however, uses general corpus (not provided by users) to train basic model, and adopts user-provided smaller corpus for migration learning. An integrated model is generated to train stable models even if the cold start Q&A database there is unsophisticated. Offline evaluation experiments have proven that when the number of similar questions is 1, the accuracy of the deep migration learning model is 40% higher than that of the traditional model, and if the number is 5, the accuracy improvement can be 100%.

## Corpus Mining Based on Big Data
Based on Tencent's big data, we can find customer questions from certain fields' corpus that are industry-related. These questions can be used to train deep learning models and creating Q&A database. The data solution is a unique asset to Tencent's Big Data team, helping users efficiently build Q&A database in cold starts.
