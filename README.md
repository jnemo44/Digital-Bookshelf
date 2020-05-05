# Requests-Lab
Used for API module of FSND

## Getting Started:
This is an API written to access and store books on a virtual bookshelf. Each book has a title,author, and rating along with an auto generated id.
Base URL: http://127.0.0.1:5000/

## Error Handling:
Standard HTTP response codes. But these errors are returned as JSON objects in the following format.
{
    "success":False,
    "error":400,
    "message":"bad request"
}

The API will return these three types when failures occur.

400 - Bad request from the client
404 - Resource not found!
422 - Unprocessable

## Endpoint Library:

# GET /books
As a GET request this endpoint returns a list of all the books on the bookshelf. The list is paginated and is a JSON object that looks like this.
Sample: curl http://127.0.0.1:5000/books

{
    "books": [
    {
      "author": "author1", 
      "id": 1, 
      "rating": 1, 
      "title": "title1"
    },
    {
      "author": "author2", 
      "id": 2, 
      "rating": 1, 
      "title": "title2"
    }] 
    "total_books":2
    "success":True
}

# PATCH /books/{book_id}
As a PATCH method this endpoint will expect the user to pass a new rating in the request for a specific book id.
Sample: curl http://127.0.0.1:5000/books/15 -X PATCH -H "Content-Type: application/json" -d '{"rating":"1"}'


{
    "success":True,
    "book_updated":book_id
}

# DELETE /books/{book_id}
Deletes the passed book_id from the bookshelf and returns the following.
Sample: curl -X DELETE http://127.0.0.1:5000/books/16?page=2
{
    "success":True,                     
    "deleted_book_id":book_id,
    "books": list of books,
    "total_books":# of books
}

# POST/books
As a POST method this endpoint will do one of two things.
1. If a search_term is passed in the body of the request the endpoint will perform a search using the search_term and return the results in the following response format.
Sample: curl http://127.0.0.1:5000/books -X POST -H "Content-Type: application/json" -d '{"search":"t"}'

Will return books with "t" in the title.

{
    'success':True,
    'total_books':# of search results,
    'books':list of books as search results
}

2. If no search_term is passed the endpoint will assume a book is being added to the bookshelf and will expect a title,author, and rating to be passed as a JSON object in the body of the request. THe following will be delivered if the book is added successfully.
Sample: curl http://127.0.0.1:5000/books?page=3 -X POST -H "Content-Type: application/json" -d '{"title":"The Ocean Blue", "author":"Blue Sky", "rating":"5"}'

{
    'success': True,
    'created': book.id,
    'current_books':list of books,
    'total_books':# of books on the shelf
}
