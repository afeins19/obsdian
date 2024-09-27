TimeLLM is a framework to adapt large language models for time series problems.

# Key Features of the Framework
- **reprogramming** - repurposing LLMs for time series analysis **without** changing the underlying model. This means that the model sees the data as any other general language input 

- **Idea** - a framework which applies reprogramming the input time series into "text prototype representations" that are more "natural" for the llm. TimeLLM also applies declarative prompts (domain expert knowledge and task instructions) to guide the reasoning of the LLM

- It consistently exceeds state of the art performance in mainstream forecasting tasks - especially few-shot and zero-shot inputs. (those that the model has little or no experience with)

- It "freezes" the language model during training? 

# Related work
![Refer to caption](https://ar5iv.labs.arxiv.org/html/2310.01728/assets/x1.png)
this describes how different reprogramming LLMs is in comparison of other methods. 

### Task Specific Learning 
most other time series forecasting models are designed for specific domains. 

**Examples**
- ARIMA for example is designed for univariate time series forecasting 
- LSTM (long short term memory) networks for sequence modeling (Hochreiter & Schmidhuber, [1997](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib15))
- Temporal convolutional neuralnetworks 
- transformers (https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib45)

These are generally thought to perform well on longer temporal dependencies within their domains but do not do a great job of generalizing.

### In-Modality Adaptation 
it turns out that pre-training somewhat generic models and then fine-tuning them for their specific tasks is an effective approach. The main benefit of this is that it removes the need to train them from scratch which is pretty costly. This research has created the time series pre-trained model or **TSPM**. These models can be trained using the classical techniques: 
-  supervised (Fawaz et al., [2018](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib12))
- self-supervised learning (Zhang et al., [2022b](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib55); Deldari et al., [2022](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib9); Zhang et al., [2023](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib53)).

The paper seems to imply this kind of general time series training leads to some gain in understanding of representing input time series.
The key limitation with **in-modality** adaptation is that the model can only really be expected to operate on similar domains. 

The article states that:
	"The development of TSPTMs leverages the success of pre-training and fine-tuning in NLP and CV but remains limited on smaller scales due to data sparsity."

### Cross-Modality Adaptation
this builds on in-modality adaptation. The paper describes transfering knowledge from pre trained foundation models in NLP and CV to time series modeling. This is done through techniques like 
- multimodal fine-tuning (Yin et al., [2023](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib51))
- model reprogramming (Chen, [2022](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib7))

**Examples of Cross-Modality Adaptations**
- Voice2Series (Yang et al., [2021](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib50)) - adapts an acoustic model from the task of speech recognition to time series classification by editing a time series into a format the model can process.

### LLM4TS
- from Chang et al. ([2023](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib6))

this model performs time series forecasting using LLMs and outlines a 2-stage process for doing so. 
1. Supervised pre-training on time series first
2. followed by task specific fine tuning 

### Zhou et al. ([2023a](https://ar5iv.labs.arxiv.org/html/2310.01728#bib.bib58)) (LLM that doesn't alter the LLMs self attention and feed-forward components)

# How Does TimeLLM differ?
TimeLLM differs from these approaches because:
- it doesn't edit the input time-series directly 
- it doesn't fine-tune the backbone LLM 

Crucially, TimeLLM applies **reprogramming** time series data with the source data modality and combine it with prompting. 

![Refer to caption](https://ar5iv.labs.arxiv.org/html/2310.01728/assets/x2.png)

instead of directly inputs into the pretrained llm body, it first tokenizes it and embeds it via a "patch reprograming". The patch embeddings are then combined with condensed text prototypes to "align the two modalities". 

Additional prompt prefixes are added to the input to direct the transformation of the input patches. I think this sort of steers the attention of the body model towards the target?

# Reprogramming
the conversion of data from a source domain to a format thats readable by the target domain

time series data (source) -> text (domain of LLM)

### Purpose
the idea behind this is to use the pre existing trained model without having to train from scratch. We just encode the input data into a new representation 

### How its Done
the process of reprograming input data between domains:

**normalization** 
(commonly instance norm) to prevent large values from dominating. The instance norm
normalizes each sample (instance) independently by its own mean and standard deviation.
$$\hat X = \frac{X - \mu_x}{\sqrt{\sigma^2+\epsilon}}$$
**Patching** 
the data is then chunked into patches to serve as a reasonable input to the LLM. We basically apply some sort of quantization on the time series and break it into uniform pieces to be fed into the llm.

the patch is then embedded into a **vector** which represents the main features of the particular patch. These patches are also combined with **text prototypes** - representations that already exist in the 
LLM's Vocabulary.


# TimeLLM Methodology
give some historical observations 
$$X \in \mathbb{R}^{N \times T}$$
where N are 1 dimension variables across T time step. The aim is to reprogram the LLM to understand a time series and accurately forecast ahead by H future time steps denoted by:
$$\hat Y \in \mathbb{R}^{N \times H}$$
we then compare this to the actual target result and try to minimize the MSE given by
$$\frac{1}{H} \sum_{h=1}^H||\hat Y_h - Y_h||_F^2$$
this is pretty standard NN stuff at the end of the day
# Look into
- byte-pair embedding -> used to build up a dictionary 
- outlier detection 