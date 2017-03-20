Lectures 3 and 4 were not done through slideshows, as they introduced the mathematical foundation of neural networks. As such, they were done on the blackboard.

Lecture 3 introduced neural networks through a simple example:

We want a simple network to learn the identity function f(X) = X.
Our network architecture consists of one scalar input, one neuron in the single hidden layer, and one output scalar.  This means that our weights and biases are scalars as well.  Initially, the network does not have an activation function for the hidden layer.
This network configuration gives the formula Y = W2( W1×X + B1 ) + B2.
For the sake of example, the weights and biases are initialized to integers that do not give the identity function (which would be weights of 1, biases of 0).
The error function in question is MSE, but without the summation, as we are working with scalars.  
Error(Y) = square(X - W2( W1×X + B1 ) + B2).  
We want the identity function, which would just give X.  So this formula is simply the square of difference between the result we achieved vs. the true answer of Y=X.
Using simple gradient descent, we find the partial derivatives w.r.t. the weights and biases.
We then use the formula Theta_i_new = Theta_i - learning_rate × d(Error(Y))/dTheta_i, where Theta_i is any of the parameters in question.  For the sake of example, learning_rate is given a clean, small value.  
We calculate the new weights and biases and find that our next iteration of the neural network has less error!

The rest of lecture was spent talking about activation functions, such as sigmoid (which is out of fashion now), tanh, relu, etc.
