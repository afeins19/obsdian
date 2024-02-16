
# Dependencies 
- Plots
- Flux.Data
- Flux
- Statistics
- LinearAlgebra
- CUDA
- Serialization
- DataFrames 

# Structs 

##### Questions:
- what is dev in ModelParams? 

## ModelParams 
- **`layers::Vector`** - a vector containing data about the layers of the neural network (how many neurons are in each layer)
- **`η::Float64`** - eta, represents the learning rate hyperparameter (i think)
- **epochs::Int** - determines the number of training cycles
- **`batchsize::Int`** - represents the number of training samples used in a single training cylce. this hyperparameter controls how data is divided (batched)
- **`lossfunc::Function`** - the function that well use to evaluate our models error 
- **`dev`** - takes in the device that will run the model (well use the gpu usually)

# Functions

##### Questions: 
- is the hidden layer just 1 layer of neurons in this function? 
- Will we try to setup a hyperparameter in the future to maybe change the number of neurons in the hidden layer? 

## build_ae_layers()
- layer_sizes - determines the number of neurons within each layer 
- activation - activation function which outputs values between -1 and 1. (set to **tanh** by default) 
```julia 
function build_ae_layers(layer_sizes, activation = tanh)    
    decoder = Chain([Dense(layer_sizes[i+1], layer_sizes[i], activation)
                    for i = length(layer_sizes)-1:-1:1]...)    
                    
    encoder = Chain([Dense(layer_sizes[i], layer_sizes[i+1], activation)
                    for i = 1:length(layer_sizes)-1]...)
                    
    Chain(encoder = encoder, decoder = decoder) # connects the enocder with the decoder 
end
```

**Chain()** - a function from Flux. Its chains together multiple NN layers into a single model. Chain allows us to immediately pass data through all layers of the neural network. the output of one network gets sent to the next automatically 

**Dense()** - takes in 3 parameters Dense(<output_dimension>, <input_dimension>, <activation_function>). Dense() is a single layer of neurons within our network. Each Neuron in a dense layer wheights the sum of all its inputs, adds a bias, and passes this whole thing through an activation function. Dense layers are **fully connected** I'm pretty sure. 
### Decoder 
the decoder is a chain of dense layers. layer_sizes is an array containing the size of each layer at the i-th index with larger layer sizes at the beginning. Since the Decoder takes inputs from the hidden layer (of a smaller dimension) and blows them up to the original dimension, we start from the end of layer_sizes for input and connect the layer to the next largest dimensioned layer. the decoder effectively reverses the dimensionality reduction done by the encoder
### Encoder 
just like the decoder, this is a chain of dense layers. We construct it in the opposite way of the decoder. We start with the input layer (first index of layer_sizes) and connect each subsequent layer to the next one with a smaller dimension. This occurs until we reach the end of layer_sizes which connects to the hidden layer.  