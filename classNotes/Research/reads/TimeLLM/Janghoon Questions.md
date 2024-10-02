 

# Please draw a block diagram for patch embedder in the figure(2).  Find out the input shape and output shape of this patch encoder![](https://github.com/KimMeen/Time-LLM/raw/main/figures/method-detailed-illustration.png)

### Input Embedding 

each input channel $X^i$ extracted from the time series (the model looks at each uni variate time series channel separately). These channels are first normalized with RevIN. then each channel $X^i$ is divided into **consecutive overlapped or non-overlapped patches** with the total number of input patches equaling:
$$
P = ⌊\frac{T-L_p}{S}⌋ + 2
$$
where S denotes the Stride length. (I don't know where the $+2$ comes from)

### Embedded Space 
In general we have an input $(n_{channels}, \;T)$ where n denotes the number of uni variate channels and T represents the number of time steps. Since we have P - patches with length $L_p$ then the sort of internal size of the patch will be $(P, L_p)$. 

This is the point where the raw input data is converted to some representation in of prototypes. 

### Output
The patches are then passed into the Patch Embedder that maps each data point at each time step to some **prototype** -> this results in the dimensionality reduction of the raw input data. The output depends on the size of the prototype space (a latent space that represents condensed knowledge and meaningful relationships that the model has learned):

The input is a univariate channel denoted by: 
$$
X_{P}^{(i)} \in \mathbb{R}^{P \times L_{p}}
$$
Using the prototypes in the patch embedder, the data is embedded **linearly** into the space of the patch embedder denoted by:
$$
\hat{X}_{P}^{(i)} \in \mathbb{R}^{P \times d_{m}}
$$
where $d_{m}$ is the size of the vector after passing through the embedding layer. As I understand it, the embedding layer maps certain inputs to the lower dimension of the prototype space. 

**In the end, we have a vector output that is a  series of patches constructed from some combination of prototypes**

##### Prototypes
These are essentially representations of data in the latent space which is derived from the input tokens. This is how the model condenses the "knowledge" it gains from the input data. The latent space contains some kinds of abstractions to map terms with similar semantics together into the same prototype? 
![[Pasted image 20241001225039.png]]


# Try to find out how outputs with each patch are used for a long sequence to find the output for a long sequence. Did it take majority decision or averaging from each output?

if we have a long sequence of input data (many time steps), is the output of the patching operation pushed through an averaging function or a majority vote from patches used?

In my understanding, they don't really seem to use either method. Instead the section called *patch reprogramming* states that it uses its concept of **reprogramming**. Using the Query, Key, and Value Matrices the model will assign importance to the inputs based on operations on these objects **(QNOTE TO SELF - STUDY UP ON THESE CONCEPTS)**

1. Try to find what kind of text will be inserted as input to Patch Program in figure-2. I mean what words or word will be converted to word embeddings? What is the size of the words? Is linear block applied to each word embedding separately or is it linear layer where multiple word embeddings are input?
2. Try to understand the multi-head attention. What are Q, K, and V?
3. In figure-3, patch-as-prefix and prompt as prefix are illustrated. However, while patch as prefix take LLM output directly, prompt as prefix requires additional layer to create the final output. Please find out why they have different architecture just depending on the input composition
4. Verify that first LLM output tensors and Patch Reprogram output are simply concatenated and they are inserted as input to the second LLM as if they are embedding of tokens
5. Think about the network structure if we replace LLM with PLM (pretrained language model) such as BERT