### LLLMs 

### General Reading on LLMS
- [x] "Enhancing Financial Time Series Forecasting with Deep Learning and Language Models"
### GPT (Generative Pre-trained Transformers) 
- [ ] “Attention is All You Need” by Vaswani et al.
### BERT (Bidirectional Encoder Representations from TRansformers)
- [ ] "BERT for Time Series Analysis: An Application to Supply Chain Risk Management"

# SOTA of LLMs for Time Series Analysis 
1. **Cross-Modality Adaptation**: Recent studies have focused on adapting LLMs to time series analysis by using techniques like multimodal fine-tuning and model reprogramming. This involves initially pre-training LLMs on large textual or other data and then adapting them to understand and forecast time series data. For instance, the Time-LLM model uses a two-stage process, starting with supervised pre-training on time series followed by task-specific fine-tuning, achieving SOTA performance without altering the core architecture of the LLM​([ar5iv](https://ar5iv.org/abs/2310.01728)).
    
2. **Challenges and Motivations**: The integration of LLMs in time series analysis is primarily motivated by the ability of LLMs to capture complex dependencies within data. However, challenges include the non-stationarity of time series data, which can impede model re-training and adaptation, and the high variability in time series data, which complicates the training of general-purpose models from scratch​([IJCAI](https://www.ijcai.org/proceedings/2024/895)