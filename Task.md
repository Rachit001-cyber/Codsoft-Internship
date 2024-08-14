//Task1
import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {

    private static final int MAX_ATTEMPTS = 10;
    private static final int LOWER_BOUND = 1;
    private static final int UPPER_BOUND = 100;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int totalRounds = 0;
        int totalWins = 0;
        String playAgain = "y";

        while (playAgain.equalsIgnoreCase("y")) {
            totalRounds++;
            if (playRound(scanner, random)) {
                totalWins++;
            }

            System.out.print("Would you like to play another round? (y/n): ");
            playAgain = scanner.next();
        }

        System.out.println("Game over! You played " + totalRounds + " rounds and won " + totalWins + " of them.");
        System.out.println("Your score: " + totalWins + "/" + totalRounds);
        scanner.close();
    }

    private static boolean playRound(Scanner scanner, Random random) {
        int numberToGuess = random.nextInt(UPPER_BOUND - LOWER_BOUND + 1) + LOWER_BOUND;
        int attemptsLeft = MAX_ATTEMPTS;
        int attemptCount = 0;

        System.out.println("Guess the number between " + LOWER_BOUND + " and " + UPPER_BOUND + ".");

        while (attemptsLeft > 0) {
            System.out.print("You have " + attemptsLeft + " attempts left. Enter your guess: ");
            int userGuess;

            try {
                userGuess = scanner.nextInt();
            } catch (Exception e) {
                System.out.println("Please enter a valid integer.");
                scanner.next(); // Clear the invalid input
                continue;
            }

            attemptCount++;
            attemptsLeft--;

            if (userGuess < numberToGuess) {
                System.out.println("Too low!");
            } else if (userGuess > numberToGuess) {
                System.out.println("Too high!");
            } else {
                System.out.println("Congratulations! You guessed the number in " + attemptCount + " attempts.");
                return true; // User guessed correctly
            }
        }

        System.out.println("Sorry, you're out of attempts. The number was " + numberToGuess + ".");
        return false; // User failed to guess correctly
    }
}

