mport java.io.*;
import java.util.Scanner;

public class FileOperationsDemo 
{
    private static final String FILE_NAME = "file_operations.txt";

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("File Operations Menu:");
        System.out.println("1. Write to File");
        System.out.println("2. Read from File");
        System.out.println("3. Modify File");
        System.out.print("Choose an option (1, 2, or 3): ");
        int choice = scanner.nextInt();
        scanner.nextLine(); // Consume the newline

        switch (choice) {
            case 1:
                writeToFile(scanner);
                break;
            case 2:
                readFromFile();
                break;
            case 3:
                modifyFile(scanner);
                break;
            default:
                System.out.println("Invalid choice! Please try again.");
        }

        scanner.close();
    }

    /**
     * Writes user-provided content to a file.
     * This will overwrite the existing content in the file.
     */
    private static void writeToFile(Scanner scanner) {
        System.out.println("\n--- Write to File ---");
        System.out.print("Enter the content to write into the file: ");
        String content = scanner.nextLine();

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(FILE_NAME))) {
            writer.write(content);
            System.out.println("Content successfully written to " + FILE_NAME);
        } catch (IOException e) {
            System.out.println("Error writing to the file: " + e.getMessage());
        }
    }

    /**
     * Reads and displays the content of the file.
     */
    private static void readFromFile() {
        System.out.println("\n--- Read from File ---");

        try (BufferedReader reader = new BufferedReader(new FileReader(FILE_NAME))) {
            String line;
            System.out.println("Contents of the file:");
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("The file " + FILE_NAME + " does not exist. Please create it first.");
        } catch (IOException e) {
            System.out.println("Error reading from the file: " + e.getMessage());
        }
    }

    /**
     * Appends user-provided content to the existing file.
     */
    private static void modifyFile(Scanner scanner) {
        System.out.println("\n--- Modify File ---");
        System.out.print("Enter the content to append to the file: ");
        String content = scanner.nextLine();

        try (BufferedWriter writer = new BufferedWriter(new FileWriter(FILE_NAME, true))) {
            writer.newLine(); // Adds a new line before appending content
            writer.write(content);
            System.out.println("Content successfully appended to " + FILE_NAME);
        } catch (IOException e) {
            System.out.println("Error modifying the file: " + e.getMessage());
        }
    }
}
