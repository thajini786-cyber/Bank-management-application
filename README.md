
#include <iostream>
#include <string>
using namespace std;

class Book
{
public:
    int bookId;
    string title;
    string author;
    bool issued;

    void addBook()
    {
        cout << "Enter Book ID: ";
        cin >> bookId;
        cin.ignore();

        cout << "Enter Book Title: ";
        getline(cin, title);

        cout << "Enter Author Name: ";
        getline(cin, author);

        issued = false;
    }

    void displayBook()
    {
        cout << "\nBook ID : " << bookId;
        cout << "\nTitle   : " << title;
        cout << "\nAuthor  : " << author;

        if (issued)
            cout << "\nStatus  : Issued";
        else
            cout << "\nStatus  : Available";

        cout << "\n";
    }
};

int main()
{
    Book books[100];
    int count = 0;
    int choice;

    do
    {
        cout << "\n===== LIBRARY MANAGEMENT SYSTEM =====";
        cout << "\n1. Add Book";
        cout << "\n2. Display Books";
        cout << "\n3. Issue Book";
        cout << "\n4. Return Book";
        cout << "\n5. Search Book";
        cout << "\n6. Exit";

        cout << "\nEnter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            books[count].addBook();
            count++;
            cout << "Book Added Successfully!\n";
            break;

        case 2:
            if (count == 0)
            {
                cout << "No books available.\n";
            }
            else
            {
                for (int i = 0; i < count; i++)
                {
                    books[i].displayBook();
                }
            }
            break;

        case 3:
        {
            int id;
            cout << "Enter Book ID to Issue: ";
            cin >> id;

            bool found = false;

            for (int i = 0; i < count; i++)
            {
                if (books[i].bookId == id)
                {
                    found = true;

                    if (!books[i].issued)
                    {
                        books[i].issued = true;
                        cout << "Book Issued Successfully!\n";
                    }
                    else
                    {
                        cout << "Book already issued.\n";
                    }
                }
            }

            if (!found)
                cout << "Book not found.\n";

            break;
        }

        case 4:
        {
            int id;
            cout << "Enter Book ID to Return: ";
            cin >> id;

            bool found = false;

            for (int i = 0; i < count; i++)
            {
                if (books[i].bookId == id)
                {
                    found = true;

                    if (books[i].issued)
                    {
                        books[i].issued = false;
                        cout << "Book Returned Successfully!\n";
                    }
                    else
                    {
                        cout << "Book was not issued.\n";
                    }
                }
            }

            if (!found)
                cout << "Book not found.\n";

            break;
        }

        case 5:
        {
            string searchTitle;
            cin.ignore();

            cout << "Enter Book Title to Search: ";
            getline(cin, searchTitle);

            bool found = false;

            for (int i = 0; i < count; i++)
            {
                if (books[i].title == searchTitle)
                {
                    books[i].displayBook();
                    found = true;
                }
            }

            if (!found)
                cout << "Book not found.\n";

            break;
        }

        case 6:
            cout << "Exiting Program...\n";
            break;

        default:
            cout << "Invalid Choice!\n";
        }

    } while (choice != 6);

    return 0;
}
