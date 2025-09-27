import java.io.*;
import java.util.Scanner;

public class NotesApp {

// File to store the notes
private static final String FILE_NAME = "notes.txt";

public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    int choice;

    while (true) {
        System.out.println("=== Notes App ===");
        System.out.println("1. Write a Note");
        System.out.println("2. View Notes");
        System.out.println("3. Exit");
        System.out.print("Enter your choice: ");
        choice = scanner.nextInt();
        scanner.nextLine(); // consume the newline character

        switch (choice) {
            case 1:
                writeNote();
                break;
            case 2:
                viewNotes();
                break;
            case 3:
                System.out.println("Goodbye!");
                scanner.close();
                System.exit(0);
            default:
                System.out.println("Invalid choice. Please try again.");
        }
    }
}

// Method to write a note to the file
public static void writeNote() {
    Scanner scanner = new Scanner(System.in);
    System.out.print("Enter your note: ");
    String note = scanner.nextLine();

    try (FileWriter writer = new FileWriter(FILE_NAME, true)) {
        writer.write(note + "\n"); // Write the note to the file, adding a new line after each note
        System.out.println("Note saved!");
    } catch (IOException e) {
        System.out.println("An error occurred while saving the note.");
        e.printStackTrace();
    }
}

// Method to view all saved notes
public static void viewNotes() {
    try (BufferedReader reader = new BufferedReader(new FileReader(FILE_NAME))) {
        String line;
        System.out.println("=== Your Notes ===");
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
    } catch (FileNotFoundException e) {
        System.out.println("No notes found. Please add some notes first.");
    } catch (IOException e) {
        System.out.println("An error occurred while reading the notes.");
        e.printStackTrace();
    }
}
}
