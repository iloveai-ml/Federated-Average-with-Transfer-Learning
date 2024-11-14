# Summary

This notebook is an implementation of the paper titled "Communication-Efficient Learning of Deep Networks from Decentralized Data" (https://arxiv.org/abs/1602.05629)

This paper introduces a methodology for Federated Learning (FL) that enables training deep learning models across multiple devices while keeping data localized. The authors propose the FederatedAveraging algorithm, which combines local stochastic gradient descent (SGD) with model averaging at a central server. Below is a detailed explanation of the methodology utilized in this research.

## Methodology Overview

### Federated Learning Framework

The authors define Federated Learning as a decentralized approach where:

1. Data remains on devices: Each participating device (client) has its local dataset, which is never uploaded to a central server.

2. Model updates are shared: Instead of sending raw data, clients compute updates to the global model based on their local data and send only these updates to the server.

### FederatedAveraging Algorithm

The core of the methodology is the FederatedAveraging algorithm, which consists of the following steps:

1. Client Selection: In each communication round, a random subset of clients is selected to participate in the training process. This helps manage communication costs and ensures efficiency.

2. Model Downloading: The server sends the current global model parameters to the selected clients.

3. Local Training: Each client performs several iterations of local SGD on its dataset to compute an update to the model parameters. This local training is crucial as it allows clients to leverage their unique data distributions.
 
4. Model Uploading: After local training, each client sends its model update back to the server.

5. Model Aggregation: The server aggregates all received updates by averaging them to form an updated global model.
 
6. Iteration: This process repeats for multiple communication rounds until convergence or until a predefined stopping criterion is met.



### Handling Non-IID and Unbalanced Data

The authors address two significant challenges in FL:

1. Non-IID Data: The data across clients may not be identically distributed, meaning each client's dataset may represent different user behaviors and preferences.

2. Unbalanced Data: Some clients may have significantly more data than others, leading to potential biases in model updates.

To mitigate these issues, FederatedAveraging effectively utilizes local updates that reflect individual client distributions while maintaining robustness through model averaging.

### Communication Efficiency

The methodology emphasizes reducing communication rounds, which are a primary constraint in FL due to limited bandwidth on mobile devices. The authors demonstrate that by increasing local computation (e.g., more SGD iterations per client before sending updates), they can significantly decrease the number of required communication rounds—reporting reductions by factors of 10 to 100 compared to traditional synchronized SGD approaches.

### Empirical Evaluation

The paper includes extensive empirical evaluations across various datasets and model architectures, showing that:

1. The FederatedAveraging algorithm performs well even with unbalanced and non-IID data distributions.

2. It achieves competitive accuracy while significantly reducing communication overhead compared to conventional methods.

## Conclusion

The proposed FederatedAveraging algorithm represents a significant advancement in enabling efficient federated learning on decentralized data while addressing privacy concerns and communication constraints inherent in mobile device environments. This methodology not only enhances model performance but also adheres to principles of data minimization and privacy preservation.
