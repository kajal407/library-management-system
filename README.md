# library-management-system
A console base library management system in C++ using file handling.
#include <iostream>
#include <vector>
using namespace std;

class Book {
public:
    int id;
    string title;
    string author;
    bool available;

    Book(int i, string t, string a) {
        id = i;
        title = t;
        author = a;
        available = true;
    }
};

class Member {
public:
    int id;
    string name;
    int issuedBook;

    Member(int i, string n) {
        id = i;
        name = n;
        issuedBook = -1;
    }
};

vector<Book> books;
vector<Member> members;

void addBook() {
    int id;
    string title, author;

    cout << "Enter Book ID: ";
    cin >> id;
    cin.ignore();

    cout << "Enter Title: ";
    getline(cin, title);

    cout << "Enter Author: ";
    getline(cin, author);

    books.push_back(Book(id, title, author));
    cout << "Book added successfully\n";
}

void addMember() {
    int id;
    string name;

    cout << "Enter Member ID: ";
    cin >> id;
    cin.ignore();

    cout << "Enter Member Name: ";
    getline(cin, name);

    members.push_back(Member(id, name));
    cout << "Member registered\n";
}

void issueBook() {
    int bookId, memberId;

    cout << "Enter Book ID: ";
    cin >> bookId;

    cout << "Enter Member ID: ";
    cin >> memberId;

    for (auto &b : books) {
        if (b.id == bookId && b.available) {
            for (auto &m : members) {
                if (m.id == memberId) {
                    b.available = false;
                    m.issuedBook = bookId;
                    cout << "Book issued successfully\n";
                    return;
                }
            }
        }
    }

    cout << "Book not available or member not found\n";
}

void returnBook() {
    int bookId;

    cout << "Enter Book ID to return: ";
    cin >> bookId;

    for (auto &b : books) {
        if (b.id == bookId) {
            b.available = true;
            cout << "Book returned successfully\n";
            return;
        }
    }

    cout << "Book not found\n";
}

void searchBook() {
    string keyword;
    cin.ignore();

    cout << "Enter title or author to search: ";
    getline(cin, keyword);

    for (auto b : books) {
        if (b.title == keyword || b.author == keyword) {
            cout << "Book ID: " << b.id << endl;
            cout << "Title: " << b.title << endl;
            cout << "Author: " << b.author << endl;
            cout << "Available: " << (b.available ? "Yes" : "No") << endl;
        }
    }
}

int main() {
    int choice;

    do {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n";
        cout << "2. Add Member\n";
        cout << "3. Issue Book\n";
        cout << "4. Return Book\n";
        cout << "5. Search Book\n";
        cout << "6. Exit\n";

        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addBook(); break;
            case 2: addMember(); break;
            case 3: issueBook(); break;
            case 4: returnBook(); break;
            case 5: searchBook(); break;
        }

    } while (choice != 6);

    return 0;
}
