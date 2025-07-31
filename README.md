# ATM-Interface-program
#include <iostream>
using namespace std;

class ATM {
private:
    float balance;
    int pin;

public:
    ATM() {
        balance = 1000.0;  // Initial balance
        pin = 1234;        // Default PIN
    }

    bool login() {
        int userPin, attempts = 0;
        while (attempts < 3) {
            cout << "Enter your 4-digit PIN: ";
            cin >> userPin;
            if (userPin == pin) {
                cout << "Login successful!\n";
                return true;
            } else {
                cout << "Incorrect PIN. Try again.\n";
                attempts++;
            }
        }
        cout << "Too many attempts. Account locked.\n";
        return false;
    }

    void displayMenu() {
        int choice;
        do {
            cout << "\n---- ATM MENU ----\n";
            cout << "1. Check Balance\n";
            cout << "2. Deposit Money\n";
            cout << "3. Withdraw Money\n";
            cout << "4. Change PIN\n";
            cout << "5. Exit\n";
            cout << "Enter your choice: ";
            cin >> choice;

            switch (choice) {
                case 1: checkBalance(); break;
                case 2: deposit(); break;
                case 3: withdraw(); break;
                case 4: changePin(); break;
                case 5: cout << "Thank you for using the ATM.\n"; break;
                default: cout << "Invalid choice. Try again.\n";
            }
        } while (choice != 5);
    }

    void checkBalance() {
        cout << "Your current balance is: ₹" << balance << endl;
    }

    void deposit() {
        float amount;
        cout << "Enter amount to deposit: ₹";
        cin >> amount;
        if (amount > 0) {
            balance += amount;
            cout << "₹" << amount << " deposited successfully.\n";
        } else {
            cout << "Invalid amount.\n";
        }
    }

    void withdraw() {
        float amount;
        cout << "Enter amount to withdraw: ₹";
        cin >> amount;
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "Please collect your cash: ₹" << amount << endl;
        } else {
            cout << "Insufficient balance or invalid amount.\n";
        }
    }

    void changePin() {
        int oldPin, newPin;
        cout << "Enter current PIN: ";
        cin >> oldPin;
        if (oldPin == pin) {
            cout << "Enter new PIN: ";
            cin >> newPin;
            pin = newPin;
            cout << "PIN changed successfully.\n";
        } else {
            cout << "Incorrect current PIN.\n";
        }
    }
};

int main() {
    ATM userATM;
    if (userATM.login()) {
        userATM.displayMenu();
    }
    return 0;
}
