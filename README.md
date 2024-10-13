# Continual Learning Strategies on MNIST Benchmark

The goal of Continual Learning is to improve the model based on experience and keep it updated to changes. 

A datastream $S$ is split into experiences. Each experience $e_i$ consists of a large batch of samples $D_i$, where $D_i$ is usually split into $D_i^{train}$ and $D_i^{test}$.

The goal is to optimize the loss computed on the different $D_i^{test}$ over the entire data stream, in order to avoid **Catarstrophic forgetting**. Training on new experiences should not reduce performance on previously learned experiences.

This project uses the standard **MNIST benchmark** to compare different Continual Learning strategies:
- **Naive Strategy (Base Strategy):** simply continue the backpropagation process on the new tasks (prone to forgetting)
- **Cumulative Strategy:** during the training of each task carry on all or part of the training sets of the previous tasks, shuffling them with the data of the current task. Using all the past data is near to the optimal performance we can desire at the end of the task sequence but at the expense of much bigger memory usage.
- **Random Replay Strategy:** uses a fixed-size Random Memory (RM) to store a subset of random previous experiences' data points. During the training on the i-th experience, it trains the model on the i-th training set shuffled with a fixed-size Random Memory (RM). RM contains a random subset of the data points of the previous experiences' training sets. After the training, it randomly substitutes some data points with a random subset of the current experience's training set in RM. This way, RM will be updated for the next experience and maintain an approximately equal number of examples for each experience.
- **Elastic Weights Consolidation (EWC) Strategy:** it is based on the computation of the importance of each weight and a squared regularization loss, penalizing changes in the most important wheights for the previous tasks. The idea is to search the optimal configuration on the overlapping of different tasks’ solution spaces. It has the great advantage of not using any of the previous tasks data.



