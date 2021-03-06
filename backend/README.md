# Full Stack Trivia API Backend

## Setting up the Backend

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM used to handle the lightweight sqlite database.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension used to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

## API Reference

### Endpoints

#### GET /categories
- Returns a list of categories, success value, and total number of categories

> Example : `curl http://127.0.0.1:5000/categories`

```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true, 
  "total_categories": 6
}
```

#### GET /questions
- Returns a list of questions, categories, the current category id, success value, and total number of questions
- Question results are paginated in groups of 10. Include a request argument to choose page number, starting from 1. 

> Example : `curl http://127.0.0.1:5000/questions`

```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "current_category": null, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },

    ...

  ], 
  "success": true, 
  "total_questions": 19
}
```

#### DELETE /question/{question_id}
 - Deletes the question of the given ID if it exists. Returns the id of the deleted question, success value, total number of questions, and question list based on the current page number.
> Example : `curl -X DELETE http://127.0.0.1:5000/questions/19?page=2`

```
{
  "deleted": 19, 
  "questions": [
    
    ...
    
    {
      "answer": "One", 
      "category": 2, 
      "difficulty": 4, 
      "id": 18, 
      "question": "How many paintings did Van Gogh sell in his lifetime?"
    }, 
    {
      "answer": "The Liver", 
      "category": 1, 
      "difficulty": 4, 
      "id": 20, 
      "question": "What is the heaviest organ in the human body?"
    }, 

    ...

  ], 
  "success": true, 
  "total_questions": 18
}
```

#### POST /questions
- Creates a new question using the submitted question, answer, difficulty, and category.
- Returns the id of the created question, success value, total number of questions, and list of questions.
> Example: `curl http://127.0.0.1:5000/books?page=3 -X POST -H "Content-Type: application/json" -d '{"question":"Why did the chicken cross the road?","answer":"To get to the other side.","difficulty":1,"category":"4"}'`

```
{
  "created": 24, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Tom Cruise", 
      "category": 5, 
      "difficulty": 4, 
      "id": 4, 
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    }, 

    ...

  ], 
  "success": true, 
  "total_questions": 19
}
```

#### POST /questions/search
- Returns a list of questions based on a search term (returning any questions for whom the search term is a substring of the question), current category id, success value, and total number of questions that match the given search term.
> Example: `curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d '{"searchTerm":"title"}'`

```
{
  "current_category": null, 
  "questions": [
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": 5, 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }
  ], 
  "success": true, 
  "total_questions": 2
}
```

#### GET /categories/{category_id}/questions
- Returns a list of questions for a given category (returning any questions for the category id), current category id, success value, and total number of questions in the category.
> Example : `curl http://localhost:5000/categories/5/questions`
```
{
  "current_category": "5", 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": "5", 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Tom Cruise", 
      "category": "5", 
      "difficulty": 4, 
      "id": 4, 
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": "5", 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }
  ], 
  "success": true, 
  "total_questions": 3
}
```

#### POST /quizzes
- Takes in a category and a list of previous question ids. Returns a question from the specified category that is not within the the list of previous question ids, a new list of previous question ids appended with the id of the returned question, and a success value.
- If no questions from the category are left the same list of previous questions is returned and a question with value null.
> Example: `curl http://127.0.0.1:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_questions":[],"quiz_category":{"type":"Science","id":"0"}}'`
```
{
  "previous_questions": [
    22
  ], 
  "question": {
    "answer": "Blood", 
    "category": 1, 
    "difficulty": 4, 
    "id": 22, 
    "question": "Hematology is a branch of medicine involving the study of what?"
  }, 
  "success": true
}
```


## Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "Bad Request"
}
```
The API will return three error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable
- 500: Internal Server Error
