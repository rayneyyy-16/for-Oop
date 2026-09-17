import java.util.Scanner;

public class Canteen {

    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);

        // Menu items
        String[] items = {
            "Burger",
            "Fries",
            "Chicken",
            "Spaghetti",
            "Soft Drink"
        };

        // Prices of menu items
        double[] prices = {
            80.00,
            50.00,
            120.00,
            90.00,
            30.00
        };

        int totalQuantity = 0;
        double totalAmount = 0.00;
        boolean isStudent = false;
        String orderAgain;

        System.out.println("==================================");
        System.out.println("       CANTEEN ORDERING SYSTEM");
        System.out.println("==================================");

        // Display menu
        System.out.println("\nMENU");
        for (int i = 0; i < items.length; i++) {
            System.out.printf("%d. %-15s PHP %.2f%n",
                    i + 1, items[i], prices[i]);
        }

        // Ask customer status
        System.out.print("\nAre you a student? (Y/N): ");
        String studentAnswer = input.nextLine();

        if (studentAnswer.equalsIgnoreCase("Y")) {
            isStudent = true;
        }

        do {

            System.out.println("\n----------------------------------");
            System.out.print("Enter item number (1-5): ");
            int itemNumber = input.nextInt();

            System.out.print("Enter quantity (1-10): ");
            int quantity = input.nextInt();

            // Validate order
            if (itemNumber < 1 || itemNumber > 5 ||
                    quantity < 1 || quantity > 10) {

                System.out.println("\nInvalid order!");
                System.out.println(
                    "Item number must be from 1 to 5 and quantity must be from 1 to 10."
                );

                input.nextLine();

                System.out.print("\nDo you want to order again? (Y/N): ");
                orderAgain = input.nextLine();

                continue;
            }

            // Calculate order amount
            double orderAmount = prices[itemNumber - 1] * quantity;

            totalQuantity += quantity;
            totalAmount += orderAmount;

            System.out.println("\nOrder added successfully!");
            System.out.println("Item: " + items[itemNumber - 1]);
            System.out.println("Quantity: " + quantity);
            System.out.printf("Amount: PHP %.2f%n", orderAmount);

            input.nextLine();

            System.out.print("\nDo you want to order again? (Y/N): ");
            orderAgain = input.nextLine();

        } while (orderAgain.equalsIgnoreCase("Y"));

        // Compute deduction
        double deductionRate = 0.00;

        if (isStudent && totalAmount >= 500) {
            deductionRate = 0.15;
        } else if (isStudent) {
            deductionRate = 0.10;
        } else if (totalAmount >= 500) {
            deductionRate = 0.05;
        }

        double totalDeduction = totalAmount * deductionRate;
        double finalAmount = totalAmount - totalDeduction;

        // Final receipt
        System.out.println("\n==================================");
        System.out.println("          ORDER SUMMARY");
        System.out.println("==================================");

        System.out.println("Total Quantity: " + totalQuantity);
        System.out.printf("Total Amount: PHP %.2f%n", totalAmount);
        System.out.printf("Deduction: PHP %.2f%n", totalDeduction);
        System.out.printf("Final Amount to Pay: PHP %.2f%n", finalAmount);

          System.out.println("==================================");
        System.out.println("       Thank you for ordering!");
        System.out.println("==================================");

        input.close();
    }
}
