
# TODO 
- work on general webscraping of data - try and scrape as many pages from the PSU domain as you can

### UML Design for the System

We'll create the following primary components for UML:

1. **Classes/Entities:**
    
    - `User`: Represents a student using the application.
    - `Course`: Represents a course offered at PSU Abington campus.
    - `Major`: Represents a student's major.
    - `VectorStore`: Represents the vector storage system for course data and market trends.
    - `QueryLog`: Represents cached query results.
2. **Relationships:**
    
    - A `User` can have multiple `Course` entries (many-to-many relationship).
    - A `User` belongs to one `Major` (one-to-many).
    - A `QueryLog` relates to specific queries and may store responses from the LLM and cache status.
    - The `VectorStore` interacts with LangChain for data processing.

#### UML Diagram Description:

```
Classes:
---------
User
- id: UUID
- name: String
- email: String
- major: ForeignKey(Major)
- courses_taken: ManyToManyField(Course)

Major
- id: UUID
- name: String
- department: String

Course
- id: UUID
- title: String
- description: Text
- credits: Integer
- prerequisites: ManyToManyField(Course)

VectorStore
- id: UUID
- data: JSONField
- website: URLField
- last_updated: DateTime

QueryLog
- id: UUID
- query_text: String
- response: JSONField
- user: ForeignKey(User)
- created_at: DateTime
- cache_hit: Boolean

```

### Models.py
```Python
from django.db import models
import uuid

class Major(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    name = models.CharField(max_length=100)
    department = models.CharField(max_length=100)

    def __str__(self):
        return self.name

class Course(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    title = models.CharField(max_length=200)
    description = models.TextField()
    credits = models.PositiveIntegerField()
    prerequisites = models.ManyToManyField('self', blank=True, symmetrical=False)

    def __str__(self):
        return self.title

class User(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    major = models.ForeignKey(Major, on_delete=models.SET_NULL, null=True)
    courses_taken = models.ManyToManyField(Course, blank=True)

    def __str__(self):
        return self.name

class VectorStore(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    data = models.JSONField()
    website = models.URLField()
    last_updated = models.DateTimeField(auto_now=True)

class QueryLog(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    query_text = models.TextField()
    response = models.JSONField()
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)
    cache_hit = models.BooleanField(default=False)
```

### Metadata to save for documents
- name 
- **URL** 
- description 
- id 