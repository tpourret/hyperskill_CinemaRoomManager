package cinema;
import java.util.Scanner;

public class Cinema {
    private static Scanner scanner = new Scanner(System.in);
    private static char[][] cinema;
    private static int rows;
    private static int seats;

    public static void main(String[] args) {
        try {
            setupCinema();
            menu();
        } finally {
            scanner.close(); // Ensure the scanner is closed after use
        }
    }

    // CINEMA SETUP
    private static void setupCinema() {
        System.out.println("Enter the number of rows:");
        rows = scanner.nextInt();

        System.out.println("Enter the number of seats in each row:");
        seats = scanner.nextInt();

        cinema = initializeCinema(rows, seats);
    }

    private static char[][] initializeCinema(int rows, int seats) {
        char[][] cinema = new char[rows][seats];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < seats; j++) {
                cinema[i][j] = 'S';
            }
        }
        return cinema;
    }

    // MENU
    private static void menu() {
        boolean menu = true;
        while (menu) {
            printMenu();
            switch (scanner.nextInt()) {
                case 1:
                    printCinema(cinema, rows, seats);
                    break;
                case 2:
                    buyATicket(cinema, rows, seats);
                    break;
                case 3:
                    printStatistics(cinema, rows, seats);
                    break;
                case 0:
                    menu = false;
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    private static void printMenu() {
        System.out.print(
                "1. Show the seats\n" +
                "2. Buy a ticket\n" +
                "3. Statistics\n" +
                "0. Exit\n");
    }

    // PRINT CINEMA
    private static void printCinema(char[][] cinema, int rows, int seats) {
        System.out.println("Cinema:");
        System.out.print("  ");
        for (int i = 1; i <= seats; i++) {
            System.out.print(i + " ");
        }
        System.out.println();

        for (int i = 0; i < rows; i++) {
            System.out.print((i + 1) + " ");
            for (int j = 0; j < seats; j++) {
                System.out.print(cinema[i][j] + " ");
            }
            System.out.println();
        }
    }

    // BUY A TICKET
    private static void buyATicket(char[][] cinema, int rows, int seats) {
        boolean ticketPurchased = false;
        while (!ticketPurchased) {
            System.out.println("Enter a row number:");
            int row = scanner.nextInt();

            System.out.println("Enter a seat number in that row:");
            int seat = scanner.nextInt();

            if (row < 1 || row > rows || seat < 1 || seat > seats) {
                System.out.println("Wrong input!");
            } else if (isSeatPurchased(cinema, row, seat)) {
                System.out.println("That ticket has already been purchased!");
            } else {
                int ticketPrice = calculateTicketPrice(rows, seats, row);
                System.out.println("Ticket price: $" + ticketPrice);
                cinema[row - 1][seat - 1] = 'B';
                printCinema(cinema, rows, seats);
                ticketPurchased = true;
            }
        }
    }

    private static int calculateTicketPrice(int rows, int seats, int row) {
        int totalSeats = rows * seats;
        if (totalSeats <= 60) {
            return 10;
        } else {
            int frontHalf = rows / 2;
            return row <= frontHalf ? 10 : 8;
        }
    }

    private static boolean isSeatPurchased(char[][] cinema, int row, int seat) {
        return cinema[row - 1][seat - 1] == 'B';
    }

    // PRINT STATISTICS
    private static void printStatistics(char[][] cinema, int rows, int seats) {
        int purchasedTickets = 0;
        int currentIncome = 0;
        int totalIncome = 0;
        int totalSeats = rows * seats;

        if (totalSeats <= 60) {
            totalIncome = totalSeats * 10;
        } else {
            int frontHalf = rows / 2;
            totalIncome = (frontHalf * seats * 10) + ((rows - frontHalf) * seats * 8);
        }

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < seats; j++) {
                if (cinema[i][j] == 'B') {
                    purchasedTickets++;
                    currentIncome += calculateTicketPrice(rows, seats, i + 1);
                }
            }
        }

        double percentage = (double) purchasedTickets / totalSeats * 100;

        System.out.println("Number of purchased tickets: " + purchasedTickets);
        System.out.printf("Percentage: %.2f%%\n", percentage);
        System.out.println("Current income: $" + currentIncome);
        System.out.println("Total income: $" + totalIncome);
    }
}
