The following is a write-up that I made to respond to a student's question regarding backpropagation through convolutional layers.

.

.

.

Hi all,

While we were talking about convolutional networks last class, I realized that I don't really understand myself how the gradients are taken through the convolutions and max pooling layers.  So this is an update in case you were curious about the answer to that question.  I brush over many of the technical aspects, which can be found [here](https://grzegorzgwardys.wordpress.com/2016/04/22/8/) and [here](https://www.slideshare.net/kuwajima/cnnbp).

For the convolutions, remember that each neuron in a convolutional layer receives signals from all of the neurons in its respective 'filter square' in the previous layer.  That is the image we saw in slide 9 of the [powerpoint](https://github.com/Andrew-Draganov/Neural-Networks-in-Application/blob/master/Slide%20Shows/6%20-%20Convolutional%20Networks.pdf) where a square from one layer passes info to a long block in the next.  So each neuron in that 'long block' has weights to every neuron in its respective square.  Functionally, this is the same backpropagation we saw for traditional feed forward network in previous lectures.  Each neuron in layer 1 is connected to a set of neurons in layer 2, and each neuron in layer 2 is connected to a set of neurons in layer 1.

So in the convolutional case, a neuron in layer 1 has weights to all of the depths of the 'long blocks' (plural!) that are connected to it in layer 2.  So when we backpropagate to neurons in layer 1, we sum the (gradients × weights) to all of the neurons in layer 2.  The difference, however, is that the number of gradients summed will be different for various neurons due to the convolutional geometry. The reasons why are outside the scope of this class, but are explained neatly [here](https://grzegorzgwardys.wordpress.com/2016/04/22/8/).  Just know that the gradients through convolutions work in a similar way, in that you take the sum of all of the (gradients × weights) a neuron is connected to.  This is what I guessed in class, but my thoughts weren't substantiated by evidence.

My guess was 100% wrong, however, when I spoke of taking gradients through max pooling.  For 2x2 max pooling, we only pass the most activated neuron through, thus reducing our network size.  I said that the gradient would be taken on the maximum, but then applied equally to everything in the square it was taken from.  To be honest, now that I think about it, this makes little intuitive sense.

Let's say we are doing max pooling with a 2x2 filter size and have the following activated neurons:

2   5

8   3

The 8 would get passed through to the next layer.  Now let's increase the 3 by 4 to get 7.  Our result that gets passed through is still 8.  At the limit definition of a derivative, this means that a very small change in the number 3 corresponds to no change in our output.  For this reason, the derivatives going to everything but the maximum must be zero.  As such, many of the gradients passing backwards through a convnet will be zero.

This gives us two advantages.  For one, our computational load is significantly smaller.  More importantly, however, we also allow variety within neighboring neurons.  If the gradients were applied equally to the whole max-pooling section, then they would have no opportunity to learn differences between one another.  When they are always modified by the same amounts, then their difference at initialization would stay for the rest of the networks' training.  As such, applying the max-pooling gradients selectively means that we achieve specialization within those max-pooling squares.

 

Best,

Andrew
