# Abstract 
![[Screen Shot 2024-09-05 at 3.43.13 PM.png]]
### Difficult to Train LLMs for Time Series
- Completely training an LLM from scratch for time series analysis tasks is difficult. This is due to 
	- large volumes of data
	- large varieties of data 
	- non-stationarity of data (this leads to concept drift)
### Advent of Pre trained LLMs for Time Series
- pretrained LLMs have shown some ability to capture complex dependencies in time series data 

# Introduction 

### Initial Applications of LLMs for tasks involving Time Series Analysis 
- classification 
- forecasting 
- anomaly detection 
### Challenges of Time Series Data 
- data may be univariate or multivariate (changing with respect to 1 or more variables)
- data in time series analysis comes in large volumes 
- Data in the real world exhibits non-stationary properties when it is continuosly accumulated 
	- this means that statistical attributes of the data (mean, variance, auto-correlation) change over time
### The Problem of Concept Drift 
- as the statistical properties of a data set may change over time (non-stationary data), the model will have trouble continuously adapting an re-training 

### Techniques of Applying LLMs to Time Series Analysis 
- direct query 
- tokenization 
- prompt design 
- fine-tuning 
- model integration 

# Background 
LLMs in this paper are categorized into the following categories: 
- embedding-visible LLMs 
- embedding-invisible LLMs

### Embedding Visible LLMs 
open-sourced with their inner state acessible. These are adaptable for various downstream tasks demonstrating impressive capabilities in both few-shot and zero-shot learning settings without the need to be trained from scratch. Examples include 
- T5 
- Flan T5 

### Embedding in-visible LLMs 
these hide their internal states from the public. 
- GPT3/4 
- PaLM 
we are limited to interacting with these through API calls 

# Taxonomy of LLMs in Time Series Analysis 
this section will feature a detailed discussion of existing research that utilizes LLMs for universal time series modeling

### General Pipeline of LLMs 
to adopt LLMs for time series analysis, three primary methods are employed:
- direct querying of LLMs
- Fine-tuning LLMs 
- Incorporating LLMs into models as a means of feature enhancement 

There are specifically three components that can be leveraged to fine-tune LLMs. The input time series is first tokenized into an embedding based on proper tokenization techniques where proper prompts can be adopted to further enhance the time series representation. This lets LLMs to better comprehend prompt-enhanced time series embeddings and be fined tuned for downstream tasks. 

### Direct Query of LLMs 
- **PromptCast** is the first work that directly conducts general time series forecasting in a sentence-to-sentence fashion using pre-trained LLLMs
- it uses prompt based time series forecasting that embeds lag information as well as instructions into the prompts and uses output sentences from the LLMs to conduct forecasting 
### Time Series Tokenization
encodes time series data into string based tokens so that LLMs can seamlessly encode time series as a series of natural language inputs so the LLMs can process them as any other sort of data. This section focuses on the design of tokenization schemes to represent time series data more effectively. 

some specific techniques include **patching tokenization**: 
For a univariate time series in- put with length $L : X_{1D} \in R^{pX n}$ 
he patching operation first repeats the final value in the original univariate time series S times. Then, it unfolds the input univariate time series through a sliding window with the length of patch size P and the stride size of S. Through patching, the univariate time series will be transformed into two-dimensional representations $X_p \in R^{pXn}$ where N is the number of patches with $N = floor(\frac{(L-P)}{2})$  