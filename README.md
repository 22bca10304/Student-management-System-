import java.util.ArrayList;
import java.util.Scanner;

class Student {
    String id;
    String name;
    int age;
    String course;

    Student(String id, String name, int age, String course) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.course = course;
    }

    void display() {
        System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age + ", Course: " + course);
    }
}

public class StudentInfoSystem {
    static ArrayList<Student> students = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        int choice;

        do {
            System.out.println("\n--- Student Information System ---");
            System.out.println("1. Add Student");
            System.out.println("2. Display All Students");
            System.out.println("3. Search Student by ID");
            System.out.println("4. Delete Student by ID");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1 -> addStudent();
                case 2 -> displayStudents();
                case 3 -> searchStudent();
                case 4 -> deleteStudent();
                case 5 -> System.out.println("Exiting... Goodbye!");
                default -> System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 5);
    }

    static void addStudent() {
        System.out.print("Enter ID: ");
        String id = scanner.nextLine();

        System.out.print("Enter Name: ");
        String name = scanner.nextLine();

        System.out.print("Enter Age: ");
        int age = scanner.nextInt();
        scanner.nextLine(); // consume newline

        System.out.print("Enter Course: ");
        String course = scanner.nextLine();

        students.add(new Student(id, name, age, course));
        System.out.println("Student added successfully.");
    }

    static void displayStudents() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
            return;
        }
        for (Student s : students) {
            s.display();
        }
    }

    static void searchStudent() {
        System.out.print("Enter ID to search: ");
        String id = scanner.nextLine();
        boolean found = false;

        for (Student s : students) {
            if (s.id.equalsIgnoreCase(id)) {
                s.display();
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Student not found.");
        }
    }

    static void deleteStudent() {
        System.out.print("Enter ID to delete: ");
        String id = scanner.nextLine();
        boolean removed = students.removeIf(s -> s.id.equalsIgnoreCase(id));

        if (removed) {
            System.out.println("Student deleted successfully.");
        } else {
            System.out.println("Student not found.");
        }
    }
}
