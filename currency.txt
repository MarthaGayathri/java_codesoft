import java.util.Scanner;
import java.text.DecimalFormat;

public class CurrencyConverter {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        DecimalFormat f = new DecimalFormat("##.###");

        System.out.println("*****CURRENCY CONVERTER*****");
        System.out.println("Enter 1: United States Dollar (USD)");
        System.out.println("Enter 2: Euro (EUR)");
        System.out.println("Enter 3: Japanese Yen (JPY)");
        System.out.println("Enter 4: Indian Rupee (INR)");

        System.out.println("\n");
        System.out.println("Enter the base currency:");
        int baseCurrency = scanner.nextInt();

        System.out.println("\n");
        System.out.println("Enter 1: United States Dollar (USD)");
        System.out.println("Enter 2: Euro (EUR)");
        System.out.println("Enter 3: Japanese Yen (JPY)");
        System.out.println("Enter 4: Indian Rupee (INR)");

        System.out.println("\n");
        System.out.println("Enter the target currency:");
        int targetCurrency = scanner.nextInt();

        System.out.println("\n");
        System.out.println("Enter the amount to convert:");
        double amount = scanner.nextDouble();
        scanner.close();

        double convertedAmount = convertCurrency(baseCurrency, targetCurrency, amount);

        if (convertedAmount != 0) {
            System.out.printf("%.2f ", amount);
            printCurrencyName(baseCurrency);
            System.out.printf(" is equal to %.2f ", convertedAmount);
            printCurrencyName(targetCurrency);
            System.out.println();
        } else {
            System.out.println("Failed to convert currency.");
        }
    }

    private static double convertCurrency(int baseCurrency, int targetCurrency, double amount) {
        double exchangeRate = getExchangeRate(baseCurrency, targetCurrency);
        return amount * exchangeRate;
    }

    private static double getExchangeRate(int baseCurrency, int targetCurrency) {
        // Predefined exchange rates for demonstration
        // In a real application, fetch these from an API
        switch (baseCurrency) {
            case 1: // USD
                switch (targetCurrency) {
                    case 1: return 1; // USD to USD
                    case 2: return 0.92; // USD to EUR
                    case 3: return 110.00; // USD to JPY
                    case 4: return 74.50; // USD to INR
                    default: return 0;
                }
            case 2: // EUR
                switch (targetCurrency) {
                    case 1: return 1.09; // EUR to USD
                    case 2: return 1; // EUR to EUR
                    case 3: return 120.00; // EUR to JPY
                    case 4: return 81.00; // EUR to INR
                    default: return 0;
                }
            case 3: // JPY
                switch (targetCurrency) {
                    case 1: return 0.0091; // JPY to USD
                    case 2: return 0.0083; // JPY to EUR
                    case 3: return 1; // JPY to JPY
                    case 4: return 0.067; // JPY to INR
                    default: return 0;
                }
            case 4: // INR
                switch (targetCurrency) {
                    case 1: return 0.013; // INR to USD
                    case 2: return 0.012; // INR to EUR
                    case 3: return 15.00; // INR to JPY
                    case 4: return 1; // INR to INR
                    default: return 0;
                }
            default:
                return 0;
        }
    }

    private static void printCurrencyName(int currencyCode) {
        switch (currencyCode) {
            case 1:
                System.out.print("USD");
                break;
            case 2:
                System.out.print("EUR");
                break;
            case 3:
                System.out.print("JPY");
                break;
            case 4:
                System.out.print("INR");
                break;
            default:
                System.out.print("Unknown Currency");
        }
    }
}