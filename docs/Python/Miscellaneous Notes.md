### \_\_repr\_\_ and \_\_str\_\_ methods

Two dunder (double underscore) methods that are very similar and often confused are **repr** and **str**. They both return a string representation of an object.  In this example, they are functionally very similar, both returning a string about the person object. Both attributes name and age are included.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"I'm {self.name}, and I'm {self.age} years old."

    def __repr__(self):
        return f"{type(self).__name__}(name='{self.name}', age={self.age})"
```

Though functionally similar, the difference is who they are intended for. **repr** is meant to be an unambiguous string representation of an object for developers to debug and/or recreate the object if necessary. **str**  is used for a user friendly printed representation of an object for end-users. The focus here is on readability.

Just remember **repr** is for developers and **str** is for customers.

By default, printing an object will use the str method, unless there is none, in which case it will fall back to the repr method. if there is neither a repr nor a str method, it will print the memory address.

### lamda

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author  
book_details = [
	("It", "Stephen King", 1138),
	("A Tale of Two Cities", "Charles Dickens", 304),
	("Going Postal", "Terry Pratchett", 484)
]

books = []

for details in book_details:
    books.append(Book(*details))

sorted_books = sorted(books, key=lambda book: book.title)
```
In this example, there is a list of book objects called `books` created from information in a list of tuples `book_details`. An additional list is created called `sorted_books` that makes reference to the same objects in the previous list, but orders them based on the book title of each object. **lambda** is used as a concise, inline key for sorting. It provides a anonymous function without the need for a `def` keyword, such as the following.

```python
def get_title(book):
    return book.title

sorted_books = sorted(books, key=get_title)
```

