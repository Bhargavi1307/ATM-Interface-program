#include <iostream>
using namespace std;

class ATM {
private:
    double balance;
    int pin;

public:
    ATM() {
        balance = 1000.0;  // initial balance
        pin = 1234;        // default PIN
    }

    bool verifyPIN() {
        int enteredPIN;
        int attempts = 0;

        while (attempts < 3) {
            cout << "Enter your 4-digit PIN: ";
            cin >> enteredPIN;

            if (enteredPIN == pin) {
                cout << "Access granted.\n";
                return true;
            } else {
                attempts++;
                cout << "Incorrect PIN. Attempts left: " << (3 - attempts) << endl;
            }
        }

        cout << "Too many incorrect attempts. Exiting...\n";
        return false;
    }

    void checkBalance() {
        cout << "Your current balance is: ₹" << balance << endl;
    }

    void deposit() {
        double amount;
        cout << "Enter amount to deposit: ₹";
        cin >> amount;
        if (amount > 0) {
            balance += amount;
            cout << "Amount deposited successfully!" << endl;
        } else {
            cout << "Invalid amount!" << endl;
        }
    }

    void withdraw() {
        double amount;
        cout << "Enter amount to withdraw: ₹";
        cin >> amount;
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "Please collect your cash!" << endl;
        } else {
            cout << "Insufficient balance or invalid amount!" << endl;
        }
    }

    void showMenu() {
        if (!verifyPIN()) return;  // if PIN fails, exit menu

        int choice;
        do {
            cout << "\n====== ATM Menu ======" << endl;
            cout << "1. Check Balance" << endl;
            cout << "2. Deposit Money" << endl;
            cout << "3. Withdraw Money" << endl;
            cout << "4. Exit" << endl;
            cout << "Choose an option (1-4): ";
            cin >> choice;

            switch (choice) {
                case 1: checkBalance(); break;
                case 2: deposit(); break;
                case 3: withdraw(); break;
                case 4: cout << "Thank you for using the ATM. Goodbye!" << endl; break;
                default: cout << "Invalid choice. Try again!" << endl;
            }
        } while (choice != 4);
    }
};

int main() {
    ATM atm;
    atm.showMenu();
    return 0;
}
