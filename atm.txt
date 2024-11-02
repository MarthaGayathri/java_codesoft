import java.util.Scanner;

// Class to represent the user's bank account
public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        } else {
            System.out.println("Invalid deposit amount. Please enter a positive value.");
        }
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        } else if (amount > balance) {
            System.out.println("Insufficient funds for withdrawal.");
            return false;
        } else {
            System.out.println("Invalid withdrawal amount. Please enter a positive value.");
            return false;
        }
    }
}

// Class to represent the ATM machine
class ATM {
    private BankAccount account;
    private Scanner scanner;

    public ATM(BankAccount account) {
        this.account = account;
        this.scanner = new Scanner(System.in);
    }

    public void start() {
        while (true) {
            displayMenu();
            int choice = getChoice();
            processChoice(choice);
        }
    }

    private void displayMenu() {
        System.out.println("\n--- ATM Menu ---");
        System.out.println("1. Check Balance");
        System.out.println("2. Deposit Money");
        System.out.println("3. Withdraw Money");
        System.out.println("4. Exit");
    }

    private int getChoice() {
        while (true) {
            try {
                System.out.print("Enter your choice: ");
                int choice = Integer.parseInt(scanner.nextLine());
                if (choice >= 1 && choice <= 4) {
                    return choice;
                } else {
                    System.out.println("Invalid choice. Please choose between 1 and 4.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
    }

    private void processChoice(int choice) {
        switch (choice) {
            case 1:
                checkBalance();
                break;
            case 2:
                depositMoney();
                break;
            case 3:
                withdrawMoney();
                break;
            case 4:
                System.out.println("Thank you for using our ATM service.");
                System.exit(0);
                break;
            default:
                // This should not happen due to input validation in getChoice()
                break;
        }
    }

    private void checkBalance() {
        double balance = account.getBalance();
        System.out.printf("Your current balance is: $%.2f%n", balance);
    }

    private void depositMoney() {
        try {
            System.out.print("Enter the amount to deposit: $");
            double amount = Double.parseDouble(scanner.nextLine());
            account.deposit(amount);
            System.out.printf("$%.2f deposited successfully.%n", amount);
        } catch (NumberFormatException e) {
            System.out.println("Invalid input. Please enter a valid number.");
        }
    }

    private void withdrawMoney() {
        try {
            System.out.print("Enter the amount to withdraw: $");
            double amount = Double.parseDouble(scanner.nextLine());
            if (account.withdraw(amount)) {
                System.out.printf("$%.2f withdrawn successfully.%n", amount);
            }
        } catch (NumberFormatException e) {
            System.out.println("Invalid input. Please enter a valid number.");
        }
    }

    public static void main(String[] args) {
        BankAccount userAccount = new BankAccount(1000.0); // Initial balance of $1000
        ATM atmMachine = new ATM(userAccount);
        atmMachine.start();
    }
}