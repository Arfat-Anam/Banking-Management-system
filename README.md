# Banking-Management-system
class Account:
    def __init__(self, name, acc_number, balance=0):
        self.name = name
        self.acc_number = acc_number
        self.balance = balance
        self.transactions = []

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposited: ${amount}")
            print(f"${amount} deposited successfully.")
        else:
            print("Invalid deposit amount.")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient balance.")
        elif amount <= 0:
            print("Invalid withdrawal amount.")
        else:
            self.balance -= amount
            self.transactions.append(f"Withdrawn: ${amount}")
            print(f"${amount} withdrawn successfully.")

    def check_balance(self):
        print(f"Current balance: ${self.balance}")

    def transaction_history(self):
        print("Transaction History:")
        for t in self.transactions:
            print(t)


class BankSystem:
    def __init__(self):
        self.accounts = {}

    def create_account(self, name, acc_number):
        if acc_number in self.accounts:
            print("Account number already exists.")
        else:
            self.accounts[acc_number] = Account(name, acc_number)
            print(f"Account created for {name} with number {acc_number}.")

    def get_account(self, acc_number):
        return self.accounts.get(acc_number, None)


# Sample usage
bank = BankSystem()

while True:
    print("\n--- Banking System Menu ---")
    print("1. Create Account")
    print("2. Deposit")
    print("3. Withdraw")
    print("4. Check Balance")
    print("5. Transaction History")
    print("6. Exit")

    choice = input("Enter your choice: ")

    if choice == '1':
        name = input("Enter your name: ")
        acc_number = input("Enter a new account number: ")
        bank.create_account(name, acc_number)

    elif choice == '2':
        acc_number = input("Enter account number: ")
        account = bank.get_account(acc_number)
        if account:
            amount = float(input("Enter amount to deposit: "))
            account.deposit(amount)
        else:
            print("Account not found.")

    elif choice == '3':
        acc_number = input("Enter account number: ")
        account = bank.get_account(acc_number)
        if account:
            amount = float(input("Enter amount to withdraw: "))
            account.withdraw(amount)
        else:
            print("Account not found.")

    elif choice == '4':
        acc_number = input("Enter account number: ")
        account = bank.get_account(acc_number)
        if account:
            account.check_balance()
        else:
            print("Account not found.")

    elif choice == '5':
        acc_number = input("Enter account number: ")
        account = bank.get_account(acc_number)
        if account:
            account.transaction_history()
        else:
            print("Account not found.")

    elif choice == '6':
        print("Exiting the system.")
        break

    else:
        print("Invalid choice. Try again.")
