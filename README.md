class Customer:
    def __init__(self, name, account_number, password, balance):
        self.name = name
        self.account_number = account_number
        self.password = password
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposit of ₹ {amount} successful. New balance: ₹ {self.balance}")
        else:
            print("Invalid deposit amount. Please enter a positive value.")

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            print(f"Withdraw of ₹ {amount} successful.\nNew balance: ₹ {self.balance}")
        else:
            print("Insufficient funds or invalid withdrawal amount.")

    def get_balance(self):
        return self.balance


class Bank:
    def __init__(self):
        self.customers = {}

    def create_account(self, name, account_number, password, initial_balance):
        if account_number not in self.customers:
            new_customer = Customer(name, account_number, password, initial_balance)
            self.customers[account_number] = new_customer
            print("Account created successfully.")
        else:
            print("Account number already exists. Please choose a different account number.")

    def view_balance(self, account_number):
        if account_number in self.customers:
            customer = self.customers[account_number]
            print(f"Name: {customer.name}")
            print(f"Account Number: {customer.account_number}")
            print(f"Current balance: ₹ {customer.balance}")
        else:
            print("Account number not found.")

    def transaction(self, account_number, transaction_type, amount):
        if account_number in self.customers:
            customer = self.customers[account_number]
            if transaction_type == 'deposit':
                customer.deposit(amount)
            elif transaction_type == 'withdraw':
                customer.withdraw(amount)
            else:
                print("Invalid transaction type. Please choose 'deposit' or 'withdraw'.")
        else:
            print("Account number not found.")


if __name__ == "__main__":
    bank = Bank()

    while True:
