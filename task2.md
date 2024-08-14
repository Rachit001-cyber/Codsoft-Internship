//Task2
import java.util.Scanner;

    public class GradeCalculator {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            // Input the number of subjects
            System.out.print("Enter the number of subjects: ");
            int numSubjects = scanner.nextInt();

            // Array to hold marks
            int[] marks = new int[numSubjects];

            // Input marks for each subject
            for (int i = 0; i < numSubjects; i++) {
                System.out.print("Enter marks for subject " + (i + 1) + ": ");
                marks[i] = scanner.nextInt();
            }

            // Calculate total marks
            int totalMarks = 0;
            for (int mark : marks) {
                totalMarks += mark;
            }

            // Calculate average percentage
            double averagePercentage = (double) totalMarks / numSubjects;

            // Determine grade
            String grade;
            if (averagePercentage >= 90) {
                grade = "A+";
            } else if (averagePercentage >= 80) {
                grade = "A";
            } else if (averagePercentage >= 70) {
                grade = "B+";
            } else if (averagePercentage >= 60) {
                grade = "B";
            } else if (averagePercentage >= 50) {
                grade = "C+";
            } else if (averagePercentage >= 40) {
                grade = "C";
            } else {
                grade = "F";
            }

            // Display results
            System.out.println("Total Marks: " + totalMarks);
            System.out.printf("Average Percentage: %.2f%%\n", averagePercentage);
            System.out.println("Grade: " + grade);

            scanner.close();
        }
    }

