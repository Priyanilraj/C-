#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Account class to manage individual accounts
class Account {
private:
    string accountNumber;
    string accountHolder;
    double balance;

public:
    // Constructor
    Account(string accNo, string holder, double initialBalance)
        : accountNumber(accNo), accountHolder(holder), balance(initialBalance) {}

    // Display account details
    void displayDetails() {
        cout << "\nAccount Number: " << accountNumber << endl;
        cout << "Account Holder: " << accountHolder << endl;
        cout << "Balance: " << balance << endl;
    }

    // Deposit amount
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "\nDeposit Successful. New Balance: " << balance << endl;
        } else {
            cout << "\nInvalid deposit amount." << endl;
        }
    }

    // Withdraw amount
    void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            cout << "\nWithdrawal Successful. New Balance: " << balance << endl;
        } else {
            cout << "\nInvalid withdrawal amount or insufficient funds." << endl;
        }
    }

    // Get account number (for searching)
    string getAccountNumber() {
        return accountNumber;
    }
};

// Bank class to manage multiple accounts
class Bank {
private:
    vector<Account> accounts;

public:
    // Create a new account
    void createAccount() {
        string accNo, holder;
        double initialBalance;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        cout << "Enter Account Holder Name: ";
        cin.ignore();
        getline(cin, holder);
        cout << "Enter Initial Balance: ";
        cin >> initialBalance;

        accounts.emplace_back(accNo, holder, initialBalance);
        cout << "\nAccount Created Successfully!" << endl;
    }

    // Find account by account number
    Account* findAccount(string accNo) {
        for (auto& account : accounts) {
            if (account.getAccountNumber() == accNo) {
                return &account;
            }
        }
        return nullptr;
    }

    // Deposit to an account
    void depositToAccount() {
        string accNo;
        double amount;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        Account* account = findAccount(accNo);

        if (account) {
            cout << "Enter Amount to Deposit: ";
            cin >> amount;
            account->deposit(amount);
        } else {
            cout << "\nAccount not found." << endl;
        }
    }

    // Withdraw from an account
    void withdrawFromAccount() {
        string accNo;
        double amount;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        Account* account = findAccount(accNo);

        if (account) {
            cout << "Enter Amount to Withdraw: ";
            cin >> amount;
            account->withdraw(amount);
        } else {
            cout << "\nAccount not found." << endl;
        }
    }

    // Display account details
    void displayAccountDetails() {
        string accNo;

        cout << "\nEnter Account Number: ";
        cin >> accNo;
        Account* account = findAccount(accNo);

        if (account) {
            account->displayDetails();
        } else {
            cout << "\nAccount not found." << endl;
        }
    }
};

int main() {
    Bank bank;
    int choice;

    do {
        cout << "\n========== Bank Management System ==========" << endl;
        cout << "1. Create Account" << endl;
        cout << "2. Deposit" << endl;
        cout << "3. Withdraw" << endl;
        cout << "4. Display Account Details" << endl;
        cout << "5. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            bank.createAccount();
            break;
        case 2:
            bank.depositToAccount();
            break;
        case 3:
            bank.withdrawFromAccount();
            break;
        case 4:
            bank.displayAccountDetails();
            break;
        case 5:
            cout << "\nExiting the system. Thank you!" << endl;
            break;
        default:
            cout << "\nInvalid choice. Please try again." << endl;
        }
    } while (choice != 5);

    return 0;
}
