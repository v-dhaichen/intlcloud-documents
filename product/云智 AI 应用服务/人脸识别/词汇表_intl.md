### APK 
APK (Android Package) is the installation package for Android. An app can be installed by transferring its APK file to the Android OS.

### Offline SDK
An offline SDK is a toolkit that implements a certain function of a software product without network connection. The offline SDK of Face Recognition supports real-time processing on the device side.

### QPS
QPS (Queries per Second) measures the requests processed concurrently per second. 1 QPS means that the API processed 1 request per second; 50 QPS means that the API processed 50 requests per second.

### Group
A group is a collection of face libraries of persons with known identities. The [face search](https://cloud.tencent.com/document/product/867/32798) and [face verification](https://cloud.tencent.com/document/product/867/32806) service can only be used with the [group management](https://cloud.tencent.com/document/product/867/32794) service.

### Data Set
A data set is a collection of data. In the field of machine learning, it usually refers to a collection of data that is specifically collected and labeled. Sometimes, it is also called sample set.

### Sample
A sample is an event or object in a data set/sample set. In Face Recognition, a face image is a sample.

### Training Set
A training set is a pre-labeled sample set used to train a model. Test sets and training sets must be strictly differentiated.

### Test Set
A test set is a pre-labeled sample set that is used to test the effects of a trained model.

### Similarity Score/Match Score
The similarity score/match score is a key indicator for [face comparison](https://cloud.tencent.com/document/product/867/32802) and [face search](https://cloud.tencent.com/document/product/867/32798), estimating the similarity of the faces - the higher the score, the higher the similarity. A recommended similarity threshold with a FAR of 0.1% or 0.01% is generally provided. When the score is higher than the recommended similarity threshold, we may conclude that these two faces are of the same person. Otherwise, they are from different persons.

### Learning/Training
Learning/training is the process of learning a model from data, which is done by executing a learning algorithm.

### Positive Sample and Negative Sample
Positive and negative samples are relative concepts. Assuming that there are 10 face images in Face Recognition, of which 4 ones are of person A and 6 person B, if the purpose is to identify A, then the number of positive samples is 4 and the number of negative samples is 6; however, if the purpose is to identify B, then the number of positive samples is 6 and the number of negative samples is 4.

### Recall Rate
In Face Recognition, let's say we have P positive samples (face images from the same person) in the test set, and N negative samples (face images from different persons). If the algorithm correctly identifies (true positive) TP positive samples and incorrectly recognize (false negative) FN positive samples as negative; and the algorithm correctly identifies (true negative) TN negative samples and incorrectly identifies (false positive) FP negative samples as positive,  where TP + FN = P and TN + FP = N, we have the recall rate is TP / P * 100%.

### False Acceptance Rate (FAR)
FAR = FP / N * 100%

### Precision Rate
Precision rate = TP / (TP + FP) * 100%

### Top N Hit Rate
In face search, the top N hit rate is the probability that the face with the correct identity is listed in the top N results. If the number of searches is M, and the face with the correct identity is listed in the top N results for TN times, then the top N hit rate = TN / M * 100%.
