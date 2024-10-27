import java.util.Scanner;

public class GradeCalculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Input number of subjects
        System.out.print("Enter the number of subjects: ");
        int numSubjects = scanner.nextInt();

        // Initialize variables to store total marks and subject names
        int[] marks = new int[numSubjects];
        String[] subjectNames = new String[numSubjects];

        // Input marks for each subject
        for (int i = 0; i < numSubjects; i++) {
            System.out.print("Enter name of Subject " + (i + 1) + ": ");
            subjectNames[i] = scanner.next();
            System.out.print("Enter marks obtained in " + subjectNames[i] + " (out of 100): ");
            marks[i] = scanner.nextInt();
        }

        // Calculate total marks
        int totalMarks = calculateTotalMarks(marks);

        // Calculate average percentage
        double averagePercentage = calculateAveragePercentage(totalMarks, numSubjects);

        // Assign grade based on average percentage
        String grade = assignGrade(averagePercentage);

        // Display results
        displayResults(totalMarks, averagePercentage, grade);
    }

    private static int calculateTotalMarks(int[] marks) {
        int total = 0;
        for (int mark : marks) {
            total += mark;
        }
        return total;
    }

    private static double calculateAveragePercentage(int totalMarks, int numSubjects) {
        return ((double) totalMarks / numSubjects);
    }

    private static String assignGrade(double averagePercentage) {
        if (averagePercentage >= 90) {
            return "A";
        } else if (averagePercentage >= 80) {
            return "B";
        } else if (averagePercentage >= 70) {
            return "C";
        } else if (averagePercentage >= 60) {
            return "D";
        } else {
            return "F";
        }
    }

    private static void displayResults(int totalMarks, double averagePercentage, String grade) {
        System.out.println("\nResults:");
        System.out.println("Total Marks: " + totalMarks);
        System.out.printf("Average Percentage: %.2f%%\n", averagePercentage);
        System.out.println("Grade: " + grade);
    }
}