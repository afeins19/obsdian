for websites/companies with large domains (lots of data). A cool commercial service to offer would be a specific and well built vector store. For example - a vector store would be built on all available information from medicare.gov. This vector store would allow other firms/chatbots to use RAG directly instead of having to create their own vector store. 

### Cool initial domains to consider
- education
- government
- private companies 
- private products/commercial stores 

# Input to the platform
- domain or product 

# Output to the platform 
a vector store custom made for them to use 

# Next Steps
- [ ] Build a document store for data on the PSU website 
	- [ ] use web querying to collect every psu page that you want 
	- [ ] setup data structures to organize documents that well be using 
	- [ ] create your own data preprocessing pipeline 
		- [ ] remove common words from text (psu, student, etc.) to remove unecessary clutter 
		- [ ] Analyze some sample pages that passed through your algorithms to make sure that data was collected properly 
- [ ] potentially use caching to minimize querying the model