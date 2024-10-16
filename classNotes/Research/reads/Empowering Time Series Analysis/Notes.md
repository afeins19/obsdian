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
- **PromptCast** is the first work that directly conducts general time series forecasting in a sentence-to-sentence fashion using pre-trained LLMs
- it uses prompt based time series forecasting that embeds lag information as well as instructions into the prompts and uses output sentences from the LLMs to conduct forecasting 
### Time Series Tokenization
encodes time series data into string based tokens so that LLMs can seamlessly encode time series as a series of natural language inputs so the LLMs can process them as any other sort of data. This section focuses on the design of tokenization schemes to represent time series data more effectively. 

some specific techniques include **patching tokenization**: 
For a univariate time series in- put with length $L : X_{1D} \in R^{pX n}$ 
he patching operation first repeats the final value in the original univariate time series S times. Then, it unfolds the input univariate time series through a sliding window with the length of patch size P and the stride size of S. Through patching, the univariate time series will be transformed into two-dimensional representations $X_p \in R^{pXn}$ where N is the number of patches with $N = floor(\frac{(L-P)}{2})$  

### Prompt Design 
- One of the main features of PromptCast is that it also develops template-based prompts for LLM time series forecasting. 
- Some other methods enrich the prompt design by incorporating LLM-generated or gathered background information which highlights the importance of context-inclusive prompts in real-world applications 
-  Time-LLM (Jin et al., 2024) adds statistical information of the time series data to the time series 

compared with fixed and non-trainable prompts, a soft and trainable prompt makes it easier for LLMs to understand and alight with the input. 

Prefix soft prompts are the task-specific embedding vectors, learned based on a loss from the LLM's output and the ground truth 

###### Notable Works in Prompt Design Techniques
- from LLMs’ output and the ground truth. TEST (Sun et al., 2024) initializes the soft prompts with uniform distributions, text embedding of the downstream task labels, or the most common words from the vocabulary.
- TEMPO (Cao et al., 2024) selects highly representative soft prompts from key-value pools
- S^2 IP-LLM (Pan etal., 2024) does prompt design by choosing the most similar semantic anchors derived from pre-trained word embedding for fine-tuning through a similarity score matching mechanism 


---> For Meeting 2 

# Current Applications 
these LLMS have been used to perform analysis in a few fields (traffic, electricity, business, illness etc.) 

The tasks that these LLMs perform may be:
- Classification 
- imputation 
- anomaly detection 

The key sort of mundane similarity between all of these is that they operate on **structured time series data**. 

### Event Sequence Data 
Models such as **LAMP** integrates an event prediction model with an LLM that performs abductive reasoning (reasoning about what the simplest and most likely cause of some event is). In the LAMP framework, event candidate predictions are generated from historical event data using a pre-trained base event sequence model. Then an LLM is prompted to suggest possible event causes. 

The LLM is instruction-tuned with some expert-annotated examples too. For retrieval of relevant events, these events will be constructed as embeddings and matched against past events based on cosine similarity scores. 

**Cosine Similarity**
![[Pasted image 20240912150119.png]]

After this and lastly, an energy function with a continuous-time transformer learns to rank predictions with scores and output the event with the strongest retrieved evidence.

**The proposed framework outperforms state-of-the-art event sequence models on real-world benchmark**

### Finance 

##### Yu et al model 
focuses on a stock return prediction task by incorporating multi-modal data including the historical stock price. It takes in: 
- Historical stock price
- Company profiles/descriptions
- Summarized news from GPT-4 

This paper tests both zero shot and one shot quieries on GPT-4 and isntruction based fine tuning on Open LLaMA. **The Results indicate that fine-tuned LLMs are capable of making decisions by analyzing multi-modal financial data thereby extracting meaningful insights and yielding explainable forecasts.** 

###### Lopez-Lira Experiment 
 Similarly, a model from Lopez-Lira and Tang directly queries ChatGPT and other large language models for stock market return predictions by using news headlines. A linear regression of the next day’s stock return is conducted on the recom- mendation score. A positive correlation between the scores and subsequent returns is observed, showing the potential of LLMs to comprehend and forecast financial time series.

