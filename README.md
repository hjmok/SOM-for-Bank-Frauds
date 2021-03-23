# SOM-for-Bank-Frauds

For this project, a Self Organizing Map performs unsupervised learning to find customers at a bank that most likely commited credit approval fraud.


## Dataset and Library
Minisom was used as the main module for this model as it contained the prebuilt functions necessary to create the SOM model.

The dataset contains information on 690 customers, including their customerID, 14 non-specific columns, and Credit Approval Class (1 for approved, 0 for denied). The lack of titles makes SOM useful since it can find clusters without the context of what the information is. Please find the dataset from the University of California Irvine Machine Learning Repository:

https://archive.ics.uci.edu/ml/datasets/statlog+(australian+credit+approval)

## Self Organizing Maps Overview
SOM is an unsupervised learning algorithm, as there are no labels on the dataset. SOM reduces dimensionality of a multi-column dataset by clustering similar data points. Moreover, since no backpropagation occurs, the weights of a neuron in SOM are different than ANN neurons. Rather than multiplying the weights to an input and passing through an activation function like in an ANN, SOM neurons use weights as a coordinate, which captures a characteristic of the node itself. As such, there is no activation function. Instead, these coordinates (weights) are used to calculate the distance.

The algorithm starts with a grid composed of nodes. The algorithm selects random nodes and computes the distances from these nodes to the neurons using the weights. The neuron with the minimum calculated distance is selected, now called the winning node. The winning node then updates its own weight, as well as the weights of the nodes around it within its own radius. These weights continually update, pulling the neighbouring nodes closer to the winning node and reducing the radius, as seen in the center image below. The algorithm continues to do this until convergence occurs and the radius stops reducing, eventually causing most nodes to be associated with a specific cluster.

Please read the following paper for more details:
https://sci2s.ugr.es/keel/pdf/algorithm/articulo/1990-Kohonen-PIEEE.pdf


## SOM Model
For Bank Credit approval, rules and guidelines are followed when determining if a customer can be approved for a loan. However, frauds do not follow these rules as the approval is going to those who should be denied. As such, a SOM can be used by finding the outlier nodes that did not fall under any cluster. Thus, the customers that got approved in these outlier nodes are frauds, whereas the correct action took place for the ones who were denied.

The SOM used a 12x12 grid with default radius of 1 and learning rate of 0.5. Moreover, the input length was 15, which encompassed all the rows excluding the Credit Approval Class. Normally, the customer ID would be excluded in analysis. However, in a SOM, the IDs influence are negligible since the values are similar, so they would all cluster together. In addition, the customer IDs were kept so that the ones that acted as frauds can easily be identified at the end.

## Results
In the grid plot, the legend goes from black to white for the lowest to highest Mean Interneuron Distances. As such, white nodes are the outliers because they do not belong to any cluster since their distance are farthest from any winning node. The outlier white nodes appear to be in coordinate (3,1) and (10,10).

In addition, the red circles indicate that the customer got denied, whereas the green squares means they got approved. There are no customers in coordinate (10,10), so all the potential frauds lie in (3,1). As seen on the right image, 23 potential frauds are within outlier. More importantly, 15 out of the 23 customers got approved.

To further validate this model, the SOM can be rerun several times then have the customer IDs compared to see if any consistently reappearing. Furthermore, the customer IDs can thus be used to investigate the specifics of this customer and how they got approved.

For the resulting image, please visit: https://hjmok.github.io/josephmok_portfolio/#/SOM
