# login-and-registration-system
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

bool isRegistered(const string& username) {
    ifstream file("users.txt");
    string fileUsername, filePassword;
    
    while (file >> fileUsername >> filePassword) {
        if (fileUsername == username) {
            return true;
        }
    }

    return false;
}

bool registerUser(const string& username, const string& password) {
    if (isRegistered(username)) {
        cout << "Username already exists. Please choose another.\n";
        return false;
    }

    ofstream file("users.txt", ios::app);
    file << username << " " << password << endl;
    file.close();

    cout << "Registration successful!\n";
    return true;
}

bool loginUser(const string& username, const string& password) {
    ifstream file("users.txt");
    string fileUsername, filePassword;

    while (file >> fileUsername >> filePassword) {
        if (fileUsername == username && filePassword == password) {
            return true;
        }
    }

    return false;
}

int main() {
    int choice;
    string username, password;

    do {
        cout << "\n=== Login and Registration System ===\n";
        cout << "1. Register\n";
        cout << "2. Login\n";
        cout << "3. Exit\n";
        cout << "Choose an option: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter new username: ";
                cin >> username;
                cout << "Enter new password: ";
                cin >> password;
                registerUser(username, password);
                break;

            case 2:
                cout << "Enter username: ";
                cin >> username;
                cout << "Enter password: ";
                cin >> password;
                if (loginUser(username, password)) {
                    cout << "Login successful. Welcome, " << username << "!\n";
                } else {
                    cout << "Invalid username or password.\n";
                }
                break;

            case 3:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid option. Try again.\n";
        }

    } while (choice != 3);

    return 0;
}
