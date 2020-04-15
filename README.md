# books API

Created to practice Go programming as starting point.

![Golang: Create a Web-View App for any platform - Reza Torkaman ...](https://miro.medium.com/max/3000/1*30aoNxlSnaYrLhBT0O1lzw.png)

## Data source

original data : https://github.com/benoitvallon/100-best-books/blob/master/books.json

***currently used data has some modifications

## Data

A JSON file with array of book objects as sample shown below.

```json
{
  "books": [
  {
    "author": "Chinua Achebe",
    "language": "English",
    "link": "https://en.wikipedia.org/wiki/Things_Fall_Apart",
    "pages": 209,
    "title": "Things Fall Apart"
  }
  ]
}
```



## API Endpoints

### All books

```http
GET http://localhost:8080/all
```

### Sample response

```json
{
    "books": [
        {
            "id": 1,
            "author": "Chinua Achebe",
            "language": "English",
            "link": "https://en.wikipedia.org/wiki/Things_Fall_Apart",
            "pages": 209,
            "title": "Things Fall Apart"
        },
        {
            "id": 3,
            "author": "Dante Alighieri",
            "language": "Italian",
            "link": "https://en.wikipedia.org/wiki/Divine_Comedy",
            "pages": 928,
            "title": "The Divine Comedy"
        }
    ],
    "error": ""
}
```



### Find by title

```http
GET http://localhost:8080/title={title}
```

##### Request String Parameters

| Request String Parameter | Description         | Type   |
| ------------------------ | ------------------- | ------ |
| title                    | part of  book title | String |

*** ordering of letters in parameter should be same as the book title

### Sample request

```http
GET http://localhost:8080/title=Al
```

### Sample response

```json
{
    "books": [
        {
            "id": 1,
            "author": "Chinua Achebe",
            "language": "English",
            "link": "https://en.wikipedia.org/wiki/Things_Fall_Apart",
            "pages": 209,
            "title": "Things Fall Apart"
        }
    ],
    "error": ""
}
```



### Find by author

```http
GET http://localhost:8080/author={author}
```

##### Request String Parameters

| Request String Parameter | Description                | Type   |
| ------------------------ | -------------------------- | ------ |
| author                   | part of book's author name | String |

*** ordering of letters in parameter should be same as the book's author name

### Sample request

```http
GET http://localhost:8080/author=po
```

### Sample response

```json
{
    "books": [
        {
            "id": 73,
            "author": "Edgar Allan Poe",
            "language": "English",
            "link": "https://en.wikipedia.org/wiki/Edgar_Allan_Poe_bibliography#Tales",
            "pages": 842,
            "title": "Tales"
        }
    ],
    "error": ""
}
```



### Find by language

```http
GET http://localhost:8080/lang={language}
```

##### Request String Parameters

| Request String Parameters | Description      | Type   |
| ------------------------- | ---------------- | ------ |
| lang                      | language of book | String |

*** ordering of letters in parameter should be same as the book language

### Sample request

```http
GET http://localhost:8080/lang=norSe
```

### Sample response

```json
{
    "books": [
        {
            "id": 7,
            "author": "Unknown",
            "language": "Old Norse",
            "link": "https://en.wikipedia.org/wiki/Nj%C3%A1ls_saga",
            "pages": 384,
            "title": "Njál's Saga"
        }
    ],
    "error": ""
}
```



### Find by id

```http
GET http://localhost:8080/id={id}
```

##### Request String Parameters

| Request String Parameters | Description | Type    |
| ------------------------- | ----------- | ------- |
| id                        | id of book  | integer |

*** id parameter value should be starting from 1

### Sample request

```http
GET http://localhost:8080/id=33
```

### Sample response

```json
{
    "books": [
        {
            "id": 33,
            "author": "Gustave Flaubert",
            "language": "French",
            "link": "https://en.wikipedia.org/wiki/Madame_Bovary",
            "pages": 528,
            "title": "Madame Bovary"
        }
    ],
    "error": ""
}
```



### Find by page range

```http
GET http://localhost:8080/page/min={min}&max={max}
```

##### Request String Parameters

| Request String Parameter | Description                         | Type    |
| :----------------------- | ----------------------------------- | ------- |
| min                      | minimum number of pages in the book | integer |
| max                      | maximum number of pages in the book | integer |

*** both parameter value should be starting from 1

*** minimum pages should not exceed maximum pages

### Sample request

```http
GET http://localhost:8080/page/min=7&max=70
```

### Sample response

```json
{
    "books": [
        {
            "id": 46,
            "author": "Henrik Ibsen",
            "language": "Norwegian",
            "link": "https://en.wikipedia.org/wiki/A_Doll%27s_House",
            "pages": 68,
            "title": "A Doll's House"
        }
    ],
    "error": ""
}
```



### Add new book

```http
POST http://localhost:8080/book
```

### Sample request

```http
POST http://localhost:8080/book
```

```
{
    "author": "Marguerite Yourcenar",
    "language": "French",
    "link": "https://en.wikipedia.org/wiki/Memoirs_of_Hadrian",
    "pages": 195,
    "title": "Memoirs of Hadrian"
}
```

### Sample response

```json
{
    "id": 103,
    "author": "Marguerite Yourcenar",
    "language": "French",
    "link": "https://en.wikipedia.org/wiki/Memoirs_of_Hadrian",
    "pages": 195,
    "title": "Memoirs of Hadrian"
}
```



### Update a book

```http
PATCH http://localhost:8080/id={id}
```

##### Request String Parameters

| Request String Parameter | Description | Type    |
| ------------------------ | ----------- | ------- |
| id                       | id of book  | integer |

*** id parameter value should exist in the system

### Sample request

```http
PATCH http://localhost:8080/id=103
```

```
{
    "language": "English",
    "link": "https://en.wikipedia.org/wiki/Things_Fall_Apart",
    "pages": 99,
    "title": "Things fall apart"
}
```

### Sample response

```json
{
    "id": 103,
    "author": "Marguerite Yourcenar",
    "language": "English",
    "link": "https://en.wikipedia.org/wiki/Things_Fall_Apart",
    "pages": 99,
    "title": "Things fall apart"
}
```



### Delete a book

```http
DELETE http://localhost:8080/id={id}
```

##### Request String Parameters

| Request String Parameter | Description | Type    |
| ------------------------ | ----------- | ------- |
| id                       | id of book  | integer |

*** id parameter value should exist in the system

### Sample request

```http
DELETE http://localhost:8080/id=103
```

### Sample response

```
Book with id: 103 is deleted
```



## Status code

200 : no error occurred

201 : new book created

400 : bad input 

- non-integer book ID
- negative number or zero entered as book ID
- invalid number of pages for page range
- minimum page number exceed maximum page number

500 : error occurred while processing

*** error details will be returned



## How to run

```go
go run main.go
```

