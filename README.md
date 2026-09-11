mport java.util.Scanner;

public class Canteen {

    public static void main(String[] args) {

        // Scanner allows us to get input from the user
        Scanner input = new Scanner(System.in);

        // --------------------------------------------------
        // 1. CANTEEN MENU
        // --------------------------------------------------

        // Array containing the names of the food items
        String[] items = {
            "Burger",
            "Pizza",
            "Pasta",
            "Sandwich",
            "Milk Tea"
        };

        // Array containing the prices of the food items
        // The price at index 0 belongs to the item at index 0
        double[] prices = {
            80.00,
            120.00,
            100.00,
            70.00,
            90.00
        };

        // --------------------------------------------------
        // 2. VARIABLES FOR THE CUSTOMER'S PURCHASE
        // --------------------------------------------------

        // Keeps track of the total number of items purchased
        int totalQuantity = 0;

        // Keeps track of the total price before discount
        double totalAmount = 0.00;

        // Stores whether the customer is a student
        char student = 'N';

        // Controls whether the customer wants to order again
        char orderAgain = 'Y';

        // --------------------------------------------------
        // 3. DISPLAY THE MENU
        // --------------------------------------------------

        System.out.println("=================================");
        System.out.println("          CANTEEN MENU");
        System.out.println("=================================");

        // Loop through the menu and display every item
        for (int i = 0; i < items.length; i++) {

            System.out.printf(
                "%d. %-10s $%.2f%n",
                i + 1,
                items[i],
                prices[i]
            );
        }

        System.out.println("=================================");

        // --------------------------------------------------
        // 4. ORDERING LOOP
        // --------------------------------------------------
        // The loop continues while the customer enters Y
        // when asked if they want to order again.

        while (orderAgain == 'Y' || orderAgain == 'y') {

            System.out.print("\nEnter item number: ");
            int itemNumber = input.nextInt();

            System.out.print("Enter quantity: ");
            int quantity = input.nextInt();

            System.out.print("Are you a student? (Y/N): ");
            student = input.next().charAt(0);

            // --------------------------------------------------
            // 5. VALIDATE THE ORDER
            // --------------------------------------------------
            // A valid item number must be from 1 to 5.
            // The quantity must be from 1 to 10.

            if (itemNumber < 1 || itemNumber > 5 ||
                quantity < 1 || quantity > 10) {

                // Display an error message
                System.out.println(
                    "Invalid order! Please enter a valid item and quantity."
                );

                // "continue" skips the rest of this order
                // and goes back to the beginning of the loop.
                continue;
            }

            // --------------------------------------------------
            // 6. CALCULATE THE ORDER SUBTOTAL
            // --------------------------------------------------

            // Arrays start at index 0.
            // Therefore, item number 1 uses index 0,
            // item number 2 uses index 1, and so on.

            double subtotal = prices[itemNumber - 1] * quantity;

            // Add this order's subtotal to the customer's
            // total purchase.
            totalAmount = totalAmount + subtotal;

            // Add the quantity to the total number of items.
            totalQuantity = totalQuantity + quantity;

            // Display the subtotal for this order
            System.out.printf("Subtotal: $%.2f%n", subtotal);

            // --------------------------------------------------
            // 7. ASK IF THE CUSTOMER WANTS ANOTHER ORDER
            // --------------------------------------------------

            System.out.print("Do you want to order again? (Y/N): ");
            orderAgain = input.next().charAt(0);
        }

        // --------------------------------------------------
        // 8. CALCULATE THE DISCOUNT
        // --------------------------------------------------

        // This variable stores the discount percentage.
        // Example:
        // 0.10 = 10%
        // 0.05 = 5%
        // 0.15 = 15%

        double discountRate = 0.00;

        // If the customer is a student AND
        // the total purchase is $500 or more,
        // they receive a 15% discount.
        if ((student == 'Y' || student == 'y') &&
            totalAmount >= 500) {

            discountRate = 0.15;
        }

        // If the customer is a student but
        // the purchase is below $500,
        // they receive a 10% discount.
        else if (student == 'Y' || student == 'y') {

            discountRate = 0.10;
        }

        // If the customer is not a student but
        // the purchase is $500 or more,
        // they receive a 5% discount.
        else if (totalAmount >= 500) {

            discountRate = 0.05;
        }

        // If none of the conditions are true,
        // the discount remains 0%.

        // --------------------------------------------------
        // 9. CALCULATE FINAL AMOUNTS
        // --------------------------------------------------

        // Calculate how much money is deducted.
        double totalDeduction = totalAmount * discountRate;

        // Subtract the discount from the original total.
        double finalAmount = totalAmount - totalDeduction;

        // --------------------------------------------------
        // 10. DISPLAY FINAL RECEIPT
        // --------------------------------------------------

        System.out.println("\n=================================");
        System.out.println("          FINAL RECEIPT");
        System.out.println("=================================");

        System.out.println(
            "Total quantity of items purchased: " + totalQuantity
        );

        System.out.printf(
            "Total amount before deductions: $%.2f%n",
            totalAmount
        );

        System.out.printf(
            "Total deduction: $%.2f%n",
            totalDeduction
        );

        System.out.printf(
            "Final amount to pay: $%.2f%n",
            finalAmount
        );

        System.out.println("=================================");

        // Close the Scanner when we are finished using it
        input.close();
    }
}
