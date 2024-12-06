
# Scope of the Model
We must first create a set of questions that we expect the model to be able to answer. 

For a initial implementation our model should be able to answer the following questions:

- "I am majoring in supply chain, I am in my sophomore year and I have taken <course_1, course_2,...,course_n>. What are courses I should take next semester?"

- "What are the basic pre-requisite courses required to take a 400-level class in supply chain?"
	- *answering questions like this will just require traversing a graph database (tree) and collecting all pre-reqs (Neo4j is a langchain integrated db)*. For now, stick to the initial version and apply this only if the current approach doesnt work. 

- "What classes will set me up for the current supply chain market given industry trends?"



# 1. Define Data Sources
we should first get the main data sources that will be used to get information about each course on campus.

### (1) List of majors
https://www.abington.psu.edu/academics/majors-at-abington

### (2) Undergraduate Course Catalog
https://bulletins.psu.edu/university-course-descriptions/undergraduate/

### (3) Gen-Ed
https://gened.psu.edu/faculty-staff/advising-resources

# 2. Scraping  & Preprocessing
- **Libraries**: BeautifulSoup, NLTK 
### (1) Scraping 

When Scraping, we should try and find a site with the largest amount of relevant information. This way, we wont have to set up a scraper for every kind of site layout. from the previous section, the undergraduate course catalog seems like a promising site to use 

### (2) Preprocessing

1. **Text Extraction**: create functions to handle pulling the raw text out of the html 
2. **Tokenization**: tokenize words while dropping things like punctuation and newline characters 
3. **Stopword Removal**: drop words that are common to all documents and those that are there for just grammar purposes. 
4. **Normalize**: make all the text lowercase and remove any weird characters or leftover artifacts 
5. **Lemmatization/Stemming**: convert words to their root form to ensure commonality across documents  

# 3. Data Structuring 
- **Libraries**: HuggingFace, BERT, ChromaDB, OpenAI

store the data in a json that will contain some information about the course along with some metadata. First we will save a bunch of these general data objects that will hold both the meta data and functions for converting them into embeddable documents.
### (1) Create Data Object 
```json 
{ 
	"course_name": "CS101", 
	"course_description": "Computers...", 
	"prerequisites": ["None"], 
	"credits": 3, 
	"major": "Computer Science",
	"url" : "http...",
	"last_updated" : '01/23/45'
}
```


### (2) Create Vector String
we will use the above data objects to create a string that will be passed into an embedding model.

```python 
course: dict() = DataObject('CS101') 

data_to_be_vectorized = "".join([str(k+' : '+v+'.') for k,v in course.items()])

```
*this should create a condensed string with the metadata and course description text.*

### (3) Vectorization
Convert this string into a vector for embedding in the db. Using a transformer like BERT we can use a pre-trained vectorizer to create this embeddings.
```Python 
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased') 
model = BertModel.from_pretrained('bert-base-uncased')
```

### (4) Store Vector and Meta Data
```Python 
import chromadb

# setup chroma 
client = chromadb.Client()

# setup collection for courses
collection = client.create_collection("courses")

# insert the data
collection.add(
    documents=[course_text],  # keep raw text 
    metadatas=[{
        "course_name": course_data["course_name"],
        "major": course_data["major"],
        "credits": course_data["credits"]
    }],  
    embeddings=[embedding]  # save embeddings
)
```
