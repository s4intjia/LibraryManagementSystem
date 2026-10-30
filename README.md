
import 'dart:io';

// ABSTRACT CLASS
abstract class LibraryItem {
  String id;
  String title;
  bool isBorrowed;

  LibraryItem({required this.id, required this.title, this.isBorrowed = false});

  String get category;

  void borrow() {
    if (isBorrowed) {
      throw Exception('This book is already borrowed.');
    }
    isBorrowed = true;
  }

  void returnBook() {
    if (!isBorrowed) {
      throw Exception('This book has not been borrowed.');
    }
    isBorrowed = false;
  }
}

// MIXIN
mixin DisplayInfo on LibraryItem {
  void displayInfo() {
    print('------------------------------');
    print('Book ID: $id');
    print('Title: $title');
    print('Category: $category');
    print('Status: ${isBorrowed ? "Borrowed" : "Available"}');
  }
}

// BOOK CLASS
class Book extends LibraryItem with DisplayInfo {
  String author;

  Book({required String id, required String title, required this.author})
    : super(id: id, title: title);

  @override
  String get category => 'Printed Book';

  void displayAuthor() {
    print('Author: $author');
  }
}

// EBOOK CLASS
class EBook extends Book {
  double fileSizeMB;

  EBook({
    required String id,
    required String title,
    required String author,
    required this.fileSizeMB,
  }) : super(id: id, title: title, author: author);

  @override
  String get category => 'E-Book';

  @override
  void displayInfo() {
    super.displayInfo();
    print('Author: $author');
    print('File Size: $fileSizeMB MB');
  }
}

// LIBRARY CLASS
class Library {
  List<Book> books = [];

  Future<void> loadBooks() async {
    try {
      print('\nLoading library data...');

      await Future.delayed(Duration(seconds: 2));

      books.addAll([
        Book(id: 'B001', title: 'Noli Me Tangere', author: 'Jose Rizal'),
        Book(id: 'B002', title: 'El Filibusterismo', author: 'Jose Rizal'),
        EBook(
          id: 'B003',
          title: 'Introduction to Dart',
          author: 'Dart Developers',
          fileSizeMB: 5.5,
        ),
      ]);

      print('Library data loaded successfully!\n');
    } catch (error) {
      print('Error loading library data: $error');
    }
  }

  void displayBooks() {
    print('\n========== BOOK LIST ==========');

    if (books.isEmpty) {
      print('No books available.');
      return;
    }

    for (Book book in books) {
      book.displayInfo();

      if (book is! EBook) {
        book.displayAuthor();
      }

      print('------------------------------');
    }
  }

  Book? findBook(String id) {
    for (Book book in books) {
      if (book.id.toLowerCase() == id.toLowerCase()) {
        return book;
      }
    }
    return null;
  }

  void borrowBook(String id) {
    Book? book = findBook(id);

    if (book == null) {
      throw Exception('Book ID not found.');
    }

    book.borrow();
    print('\nSuccessfully borrowed: ${book.title}');
  }

  void returnBook(String id) {
    Book? book = findBook(id);

    if (book == null) {
      throw Exception('Book ID not found.');
    }

    book.returnBook();
    print('\nSuccessfully returned: ${book.title}');
  }
}

// MAIN FUNCTION
Future<void> main() async {
  Library library = Library();

  await library.loadBooks();

  bool isRunning = true;

  while (isRunning) {
    print('\n================================');
    print('     LIBRARY MANAGEMENT SYSTEM');
    print('================================');
    print('1. View All Books');
    print('2. Borrow a Book');
    print('3. Return a Book');
    print('4. Exit');
    print('================================');

    stdout.write('Enter your choice: ');

    String? choice = stdin.readLineSync();

    try {
      switch (choice) {
        case '1':
          library.displayBooks();
          break;

        case '2':
          stdout.write('Enter Book ID to borrow: ');
          String? borrowId = stdin.readLineSync();

          if (borrowId == null || borrowId.trim().isEmpty) {
            throw Exception('Book ID cannot be empty.');
          }

          library.borrowBook(borrowId.trim());
          break;

        case '3':
          stdout.write('Enter Book ID to return: ');
          String? returnId = stdin.readLineSync();

          if (returnId == null || returnId.trim().isEmpty) {
            throw Exception('Book ID cannot be empty.');
          }

          library.returnBook(returnId.trim());
          break;

        case '4':
          print('\nThank you for using the Library Management System!');
          isRunning = false;
          break;

        default:
          print('\nInvalid choice. Please select 1-4.');
      }
    } catch (error) {
      print('\nError: $error');
    }
  }
}
