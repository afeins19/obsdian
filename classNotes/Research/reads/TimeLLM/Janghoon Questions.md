 

# Please draw a block diagram for patch embedder in the figure-2. Find out the input shape and output shape of this patch encoder[![](https://github.com/KimMeen/Time-LLM/raw/main/figures/method-detailed-illustration.png)](https://github.com/KimMeen/Time-LLM/blob/main/figures/method-detailed-illustration.png)
**Input Embedding** - each input channel $X^i$ extracted from the time series (the model looks at each univariate time series channel separately). These channels are first normalized with RevIN. then each channel $X^i$ is divided into **consecutive overlapped or non-overlapped patches** with the total number of input patches equaling:

$$
P = ⌊\frac{t-L_p}{S}⌋ + 2
$$
where S denotes the Stride length 




3. Try to find out how outputs with each patch are used for a long sequence to find the output for a long sequence. Did it take majority decision or averaging from each output?
4. Try to find what kind of text will be inserted as input to Patch Program in figure-2. I mean what words or word will be converted to word embeddings? What is the size of the words? Is linear block applied to each word embedding separately or is it linear layer where multiple word embeddings are input?
5. Try to understand the multi-head attention. What are Q, K, and V?
6. In figure-3, patch-as-prefix and prompt as prefix are illustrated. However, while patch as prefix take LLM output directly, prompt as prefix requires additional layer to create the final output. Please find out why they have different architecture just depending on the input composition
7. Verify that first LLM output tensors and Patch Reprogram output are simply concatenated and they are inserted as input to the second LLM as if they are embedding of tokens
8. Think about the network structure if we replace LLM with PLM (pretrained language model) such as BERT