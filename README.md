//CBTCIP
/*
This project based on an ATM Interface System. It consists of five different classes and is a console-based application.
 When the system starts the user is prompted with user id and user pin.
 On entering the details successfully, then ATM functionalities are unlocked.
 The project allows to perform following operations:
1) Transaction History
2) Withdraw
3) Deposit
4) Transfer
5) Exit
 */
import java.util.Scanner;

class BankAccount {
    private String name;
    private String userName;
    private String password;
    private float balance = 100000f;
    private int transactions = 0;
    private StringBuilder transactionHistory = new StringBuilder();
    public void register(Scanner scanner) {
        System.out.println("=== Registration ===");
        System.out.print("Enter Your Name: ");
        this.name = scanner.nextLine();
        System.out.print("Enter Your Username: ");
        this.userName = scanner.nextLine();
        System.out.print("Enter Your Password: ");
        this.password = scanner.nextLine();
        System.out.println("Registration Successful!");
        login(scanner);
    }

    public void login(Scanner scanner) {
        System.out.println("\n=== Login ===");
        System.out.print("Enter Your Username: ");
        String enteredUsername = scanner.nextLine();
        System.out.print("Enter Your Password: ");
        String enteredPassword = scanner.nextLine();

        if (enteredUsername.equals(userName) && enteredPassword.equals(password)) {
            showMenu(scanner);
        } else {
            System.out.println("Invalid username or password. Please try again.");
        }
    }
    private void showMenu(Scanner scanner) {
        while (true) {
            System.out.println("\n=== ATM Menu ===");
            System.out.println("1. Withdraw");
            System.out.println("2. Deposit");
            System.out.println("3. Transfer");
            System.out.println("4. Check Balance");
            System.out.println("5. Transaction History");
            System.out.println("6. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); 
            switch (choice) {
                case 1:
                    withdraw(scanner);
                    break;
                case 2:
                    deposit(scanner);
                    break;
                case 3:
                    transfer(scanner);
                    break;
                case 4:
                    checkBalance();
                    break;
                case 5:
                    showTransactionHistory();
                    break;
                case 6:
                    System.out.println("Exiting ATM. Thank you!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
    private void withdraw(Scanner scanner) {
        System.out.print("Enter amount to withdraw: ");
        float amount = scanner.nextFloat();

        if (amount > 0 && amount <= balance) {
            transactions++;
            balance -= amount;
            transactionHistory.append(amount).append(" Rs Withdrawed\n");
            System.out.println("Withdraw Successful!");
        } else {
            System.out.println("Invalid amount or insufficient balance!");
        }
    }

    private void deposit(Scanner scanner) {
        System.out.print("Enter amount to deposit: ");
        float amount = scanner.nextFloat();

        if (amount > 0 && amount <= 100000f) {
            transactions++;
            balance += amount;
            transactionHistory.append(amount).append(" Rs deposited\n");
            System.out.println("Deposit Successful!");
        } else {
            System.out.println("Invalid amount or exceeding limit!");
        }
    }

    private void transfer(Scanner scanner) {
        System.out.print("Enter recipient's name: ");
        String recipient = scanner.nextLine();
        System.out.print("Enter recipents bank account no: ");
        int Raccount = scanner.nextInt();
        System.out.print("Enter amount to transfer: ");
        float amount = scanner.nextFloat();
        

        if (amount > 0 && amount <= 50000f && amount <= balance) {
            transactions++;
            balance -= amount;
            transactionHistory.append(amount).append(" Rs transferred to ").append(recipient).append("\n");
            System.out.println("Transfer Successful!");
        } else {
            System.out.println("Invalid amount, exceeding limit, or insufficient balance!");
        }
    }
    private void checkBalance() {
        System.out.println("Your Balance: " + balance + " Rs");
    }
    private void showTransactionHistory() {
        System.out.println("=== Transaction History ===");
        System.out.println(transactionHistory.toString());
    }
}
public class ATM {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        BankAccount bankAccount = new BankAccount();

        System.out.println("------------Welcome to the ATM System----------");
        bankAccount.register(scanner);
    }
}
