# Library Management System

**Lab 3: Final Midterm Project – The Dart App Simulator**

**Developed by:** Jesica Flores  
**Programming Language:** Dart  
**Project Type:** Console-Based Application

## Project Description

The Library Management System is a console-based application developed using Dart. It simulates a simple library where users can view, borrow, and return books.

The application demonstrates Object-Oriented Programming (OOP) concepts and asynchronous programming covered in Weeks 7–11.

## Features

- View all books in the library.
- Borrow a book using its Book ID.
- Return borrowed books.
- Display book information, including title, author, category, and status.
- Support for printed books and e-books.
- Simulated loading of library data.
- Error handling for invalid operations.

## OOP Concepts Implemented

**1. Abstract Class – LibraryItem**

Serves as the base class for library items and defines common properties and methods.

**2. Inheritance – Book and EBook**

The Book class inherits from LibraryItem, while EBook inherits from Book.

**3. Mixin – DisplayInfo**

Provides reusable functionality for displaying book information.

**4. Constructors and Methods**

Classes use constructors to initialize their properties and methods to perform specific operations.

## Asynchronous Programming

The application uses `Future`, `async`, and `await` to simulate loading library data. The `Future.delayed()` method creates a two-second loading delay.

## Error Handling

The application uses `try-catch` to handle errors, including:

- Invalid Book IDs.
- Borrowing an already borrowed book.
- Returning a book that has not been borrowed.
- Empty Book ID inputs.


## Sample Book Records

| Book ID | Title | Category |
|---|---|---|
| B001 | Noli Me Tangere | Printed Book |
| B002 | El Filibusterismo | Printed Book |
| B003 | Introduction to Dart | E-Book |

## Project Information

This project was developed as an individual final midterm requirement for the Dart programming subject. It demonstrates the use of OOP, inheritance, mixins, asynchronous operations, and error handling in a simple library simulation.
