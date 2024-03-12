# Problem statement

One way to speed up nearest neighbor classification is to replace the training set by a carefully chosen subset of “prototypes” – i.e. instead of keeping the entire training set to use for nearest neighbor classification, carefully choose a small but representative subset to search for nearest neighbors in. Because this set is smaller than the training data, search will be faster and thus so will classification. However, if poor prototypes are chosen, the resulting test accuracy may be much worse. 

Think of a good strategy for choosing prototypes from the training set, bearing in mind that the ultimate goal is good classification performance on test data. 
- What properties make a set of examples effective for nearest neighbor classification? 
- Can you formalize these properties and use them to select protoypes automatically? 
- Assume that 1-NN will be used.

# Approach

- what are the things i know about classification?
- what are the things i know about nn specifically?
- data pruning techniques for image datasets
	- paper: beating neural scaling law via model distillation
- energy based image selection
- clustering first

Two approaches from the high level can be used:
- Redundancy removal
- Bottom-up selection

clustering: use k-means to reduce the cluster to a single point,
or keep the median or mean data point,

given an image matrix, we commonly flatten them, then use euclidian distance to compare similarity.

Some data points are better than others,
for one data point, some elements in the matrix / array is more important than others. This shouldn't matter too much.

# Experiments
## Full training
Training accuracy for full dataset: 1.0 
Test accuracy for full dataset: 0.9691
## Random Dropping
Running 1-NN on 1000 subset data
Avg Test Accuracy: 0.8908000000000003 Min Test Accuracy: 0.8908 Max Test Accuracy: 0.8908 StD Test Accuracy: 2.220446049250313e-16 Confidence interval at 95% confidence level: 0.8908000000000003, 0.8908000000000003 

Running 1-NN on 2500 subset data
Avg Test Accuracy: 0.9164999999999998 Min Test Accuracy: 0.9165 Max Test Accuracy: 0.9165 StD Test Accuracy: 2.220446049250313e-16 Confidence interval at 95% confidence level: 0.9164999999999998, 0.9164999999999998 

Running 1-NN on 6000 subset data
Avg Test Accuracy: 0.9385000000000001 Min Test Accuracy: 0.9385 Max Test Accuracy: 0.9385 StD Test Accuracy: 1.1102230246251565e-16 Confidence interval at 95% confidence level: 0.9385000000000001, 0.9385000000000001 

Running 1-NN on 10000 subset data
Avg Test Accuracy: 0.9484999999999997 Min Test Accuracy: 0.9485 Max Test Accuracy: 0.9485 StD Test Accuracy: 3.3306690738754696e-16 Confidence interval at 95% confidence level: 0.9484999999999996, 0.9484999999999998

# VAE generated training set performance

Running 1-NN on 1000 VAE generated data

Avg Test Accuracy: 0.6120999999999999
Min Test Accuracy: 0.6121
Max Test Accuracy: 0.6121
StD Test Accuracy: 1.1102230246251565e-16
Confidence interval at 95% confidence level: 0.6120999999999999, 0.6120999999999999

Running 1-NN on 2500 VAE generated data
Avg Test Accuracy: 0.7069999999999997
Min Test Accuracy: 0.707
Max Test Accuracy: 0.707
StD Test Accuracy: 2.220446049250313e-16
Confidence interval at 95% confidence level: 0.7069999999999997, 0.7069999999999997

Running 1-NN on 6000 VAE generated data
Avg Test Accuracy: 0.6977
Min Test Accuracy: 0.6977
Max Test Accuracy: 0.6977
StD Test Accuracy: 0.0
Confidence interval at 95% confidence level: 0.6977, 0.6977

Running 1-NN on 10000 VAE generated data
Avg Test Accuracy: 0.7236999999999998
Min Test Accuracy: 0.7237
Max Test Accuracy: 0.7237
StD Test Accuracy: 2.220446049250313e-16
Confidence interval at 95% confidence level: 0.7236999999999998, 0.7236999999999998

# Other misc logs
## VAE Training loss

Getting class specific data for class label 0 Getting class specific data... Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 122.4089126586914 Loss at 1: 110.86710357666016 Loss at 2: 111.00749206542969 Loss at 3: 102.79061889648438 Loss at 4: 113.28883361816406 Loss at 5: 102.20415496826172 Loss at 6: 111.10794067382812 Loss at 7: 102.75852966308594 Loss at 8: 112.13987731933594 Loss at 9: 101.08644104003906 Loss at 10: 102.69970703125 Loss at 11: 105.51646423339844 Loss at 12: 102.3199691772461 Loss at 13: 104.53943634033203 Loss at 14: 111.3336410522461 Loss at 15: 100.34881591796875 Loss at 16: 97.97409057617188 Loss at 17: 98.98175811767578 Loss at 18: 100.71955871582031

Training completed. Getting class specific data for class label 1 Getting class specific data...

Loss at 19: 95.77108764648438

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 81.46790313720703 Loss at 1: 81.94615936279297 Loss at 2: 79.92033386230469 Loss at 3: 80.2786865234375 Loss at 4: 97.06309509277344 Loss at 5: 79.86027526855469 Loss at 6: 83.53164672851562 Loss at 7: 78.9686508178711 Loss at 8: 81.87531280517578 Loss at 9: 80.21139526367188 Loss at 10: 81.91621398925781 Loss at 11: 77.96463775634766 Loss at 12: 80.647216796875 Loss at 13: 79.50249481201172 Loss at 14: 81.5664291381836 Loss at 15: 80.20169830322266 Loss at 16: 77.74273681640625 Loss at 17: 83.84297180175781 Loss at 18: 80.86901092529297

Training completed. Getting class specific data for class label 2 Getting class specific data...

Loss at 19: 76.99665832519531

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 111.00515747070312 Loss at 1: 119.29170227050781 Loss at 2: 142.10284423828125 Loss at 3: 123.13195037841797 Loss at 4: 109.37509155273438 Loss at 5: 125.89137268066406 Loss at 6: 109.05889892578125 Loss at 7: 104.85855102539062 Loss at 8: 113.73287963867188 Loss at 9: 109.9818115234375 Loss at 10: 104.70372009277344 Loss at 11: 107.85289001464844 Loss at 12: 120.07435607910156 Loss at 13: 118.22438049316406 Loss at 14: 113.3527603149414 Loss at 15: 110.36813354492188 Loss at 16: 107.36387634277344 Loss at 17: 127.86540222167969 Loss at 18: 110.25729370117188

Training completed. Getting class specific data for class label 3 Getting class specific data...

Loss at 19: 110.17372131347656

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 103.89154815673828 Loss at 1: 102.5278549194336 Loss at 2: 98.02315521240234 Loss at 3: 106.32646179199219 Loss at 4: 101.45697021484375 Loss at 5: 103.97869873046875 Loss at 6: 104.4879150390625 Loss at 7: 98.17564392089844 Loss at 8: 97.83837127685547 Loss at 9: 98.1276626586914 Loss at 10: 101.62250518798828 Loss at 11: 97.10814666748047 Loss at 12: 98.94723510742188 Loss at 13: 103.8311767578125 Loss at 14: 93.32845306396484 Loss at 15: 95.08446502685547 Loss at 16: 95.4561767578125 Loss at 17: 93.39474487304688 Loss at 18: 97.16043090820312

Training completed. Getting class specific data for class label 4 Getting class specific data...

Loss at 19: 91.82394409179688

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 98.99583435058594 Loss at 1: 95.54893493652344 Loss at 2: 101.4473648071289 Loss at 3: 105.71363830566406 Loss at 4: 100.44166564941406 Loss at 5: 104.16685485839844 Loss at 6: 88.57695007324219 Loss at 7: 102.79693603515625 Loss at 8: 92.67582702636719 Loss at 9: 91.97683715820312 Loss at 10: 97.1934814453125 Loss at 11: 94.14601135253906 Loss at 12: 90.57453918457031 Loss at 13: 92.8495864868164 Loss at 14: 99.30792999267578 Loss at 15: 98.28964233398438 Loss at 16: 91.95523834228516 Loss at 17: 92.95890808105469 Loss at 18: 90.59234619140625

Training completed. Getting class specific data for class label 5 Getting class specific data...

Loss at 19: 91.48946380615234

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 106.39237213134766 Loss at 1: 101.62786865234375 Loss at 2: 111.33998107910156 Loss at 3: 104.0583267211914 Loss at 4: 103.35270690917969 Loss at 5: 109.78945922851562 Loss at 6: 101.09654235839844 Loss at 7: 107.10713958740234 Loss at 8: 106.05005645751953 Loss at 9: 104.54562377929688 Loss at 10: 105.7917709350586 Loss at 11: 102.22261810302734 Loss at 12: 102.54883575439453 Loss at 13: 98.72271728515625 Loss at 14: 99.66307830810547 Loss at 15: 109.907958984375 Loss at 16: 99.99410247802734 Loss at 17: 102.69688415527344 Loss at 18: 100.53662109375

Training completed. Getting class specific data for class label 6 Getting class specific data...

Loss at 19: 95.2458267211914

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 106.13623809814453 Loss at 1: 110.67214965820312 Loss at 2: 116.06074523925781 Loss at 3: 111.8877182006836 Loss at 4: 108.58922576904297 Loss at 5: 108.62767028808594 Loss at 6: 101.96141052246094 Loss at 7: 104.14747619628906 Loss at 8: 110.42649841308594 Loss at 9: 100.75656127929688 Loss at 10: 111.21807861328125 Loss at 11: 103.2879638671875 Loss at 12: 100.97655487060547 Loss at 13: 97.6056137084961 Loss at 14: 97.9891357421875 Loss at 15: 105.21614837646484 Loss at 16: 100.59447479248047 Loss at 17: 107.43409729003906 Loss at 18: 110.10355377197266

Training completed. Getting class specific data for class label 7 Getting class specific data...

Loss at 19: 95.94866180419922

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 86.07105255126953 Loss at 1: 85.46380615234375 Loss at 2: 88.7225341796875 Loss at 3: 88.83303833007812 Loss at 4: 90.35819244384766 Loss at 5: 93.97811889648438 Loss at 6: 99.46868133544922 Loss at 7: 86.51997375488281 Loss at 8: 85.29087829589844 Loss at 9: 92.21759033203125 Loss at 10: 90.23709106445312 Loss at 11: 84.59526062011719 Loss at 12: 87.423828125 Loss at 13: 81.42411041259766 Loss at 14: 91.52676391601562 Loss at 15: 80.01567077636719 Loss at 16: 83.7529296875 Loss at 17: 84.36988067626953 Loss at 18: 84.50588989257812

Training completed. Getting class specific data for class label 8 Getting class specific data...

Loss at 19: 87.98660278320312

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 130.28814697265625 Loss at 1: 126.7728500366211 Loss at 2: 120.40559387207031 Loss at 3: 129.28416442871094 Loss at 4: 130.6036834716797 Loss at 5: 138.0755615234375 Loss at 6: 132.32723999023438 Loss at 7: 118.65930938720703 Loss at 8: 123.95036315917969 Loss at 9: 117.49718475341797 Loss at 10: 116.79285430908203 Loss at 11: 119.59568786621094 Loss at 12: 118.26148223876953 Loss at 13: 120.05845642089844 Loss at 14: 122.75981140136719 Loss at 15: 121.58854675292969 Loss at 16: 116.27122497558594 Loss at 17: 143.56678771972656 Loss at 18: 116.40228271484375

Training completed. Getting class specific data for class label 9 Getting class specific data...

Loss at 19: 122.87095642089844

Class specific data obtained. Training Variational Autoencoder...

Loss at 0: 100.94534301757812 Loss at 1: 94.13126373291016 Loss at 2: 90.84122467041016 Loss at 3: 102.187255859375 Loss at 4: 105.78821563720703 Loss at 5: 88.86478424072266 Loss at 6: 85.34429168701172 Loss at 7: 86.9412841796875 Loss at 8: 93.36521911621094 Loss at 9: 90.75650024414062 Loss at 10: 85.99443817138672 Loss at 11: 90.0863037109375 Loss at 12: 85.32676696777344 Loss at 13: 91.93643188476562 Loss at 14: 91.98363494873047 Loss at 15: 86.10856628417969 Loss at 16: 89.58153533935547 Loss at 17: 87.67195892333984 Loss at 18: 99.98988342285156

Training completed.

Loss at 19: 85.33061218261719
