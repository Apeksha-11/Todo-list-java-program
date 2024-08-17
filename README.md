import java.util.ArrayList;
import java.util.Scanner;

public class TodoListApp {

    static class Task {
        String description;
        boolean isCompleted;

        Task(String description) {
            this.description = description;
            this.isCompleted = false;
        }

        @Override
        public String toString() {
            return (isCompleted ? "[X] " : "[ ] ") + description;
        }
    }

    private static final ArrayList<Task> tasks = new ArrayList<>();
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        boolean running = true;

        while (running) {
            System.out.println("\nTodo List Application");
            System.out.println("1. Add Task");
            System.out.println("2. Remove Task");
            System.out.println("3. View Tasks");
            System.out.println("4. Mark Task as Completed");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume newline

            switch (choice) {
                case 1:
                    addTask();
                    break;
                case 2:
                    removeTask();
                    break;
                case 3:
                    viewTasks();
                    break;
                case 4:
                    markTaskAsCompleted();
                    break;
                case 5:
                    running = false;
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }

        scanner.close();
    }

    private static void addTask() {
        System.out.print("Enter task description: ");
        String description = scanner.nextLine();
        tasks.add(new Task(description));
        System.out.println("Task added.");
    }

    private static void removeTask() {
        viewTasks();
        System.out.print("Enter task number to remove: ");
        int taskNumber = scanner.nextInt() - 1;
        scanner.nextLine();  // Consume newline

        if (taskNumber >= 0 && taskNumber < tasks.size()) {
            tasks.remove(taskNumber);
            System.out.println("Task removed.");
        } else {
            System.out.println("Invalid task number.");
        }
    }

    private static void viewTasks() {
        if (tasks.isEmpty()) {
            System.out.println("No tasks to display.");
            return;
        }

        System.out.println("\nCurrent Tasks:");
        for (int i = 0; i < tasks.size(); i++) {
            System.out.printf("%d. %s%n", i + 1, tasks.get(i).toString());
        }
    }

    private static void markTaskAsCompleted() {
        viewTasks();
        System.out.print("Enter task number to mark as completed: ");
        int taskNumber = scanner.nextInt() - 1;
        scanner.nextLine();  // Consume newline

        if (taskNumber >= 0 && taskNumber < tasks.size()) {
            tasks.get(taskNumber).isCompleted = true;
            System.out.println("Task marked as completed.");
        } else {
            System.out.println("Invalid task number.");
        }
    }
}
