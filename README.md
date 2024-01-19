import java.util.ArrayList;
import java.util.Scanner;

public class TaskListApp {
    public static void main(String[] args) {
        TaskList taskList = new TaskList();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            menu();
            int choice = getUserChoice(scanner);

            switch (choice) {
                case 1:
                    taskList.add(getTaskName(scanner));
                    break;
                case 2:
                    if (!taskList.isEmpty()) {
                        taskList.listoutTasks();
                        int taskNumber = getUserInput(scanner, "Enter the task number from 1 to 4 only to remove the task: ");
                        if (taskList.isValidTaskNumber(taskNumber)) {
                            taskList.remove(taskNumber);
                        } else {
                            System.out.println("Invalid task number please enter valid number");
                        }
                    } else {
                        System.out.println("No tasks to be removed.");
                    }
                    break;
                case 3:
                    if (!taskList.isEmpty()) {
                        taskList.listoutTasks();
                    } else {
                        System.out.println("No tasks to be listed.");
                    }
                    break;
                case 4:
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again and enter correct option.");
            }
        }
    }

    private static void menu() {
        System.out.println("Task List Applications:");
        System.out.println("1. Add the Task");
        System.out.println("2. Removing the Task");
        System.out.println("3. Listing the Tasks");
        System.out.println("4. Quit option");
        System.out.print("Select an option: ");
    }

    private static int getUserChoice(Scanner scanner) {
        return scanner.nextInt();
    }

    private static String getTaskName(Scanner scanner) {
        System.out.print("Enter task name: ");
        return scanner.next();
    }

    private static int getUserInput(Scanner scanner, String prompt) {
        System.out.print(prompt);
        return scanner.nextInt();
    }
}

class TaskList {
    private ArrayList<String> tasks = new ArrayList<>();

    public void add(String name) {
        tasks.add(name);
        System.out.println("Task added successfully.");
    }

    public void remove(int taskNumber) {
        tasks.remove(taskNumber - 1);
        System.out.println("Task removed successfully.");
    }

    public void listoutTasks() {
        for (int j = 0; j < tasks.size(); j++) {
            System.out.println((j + 1) + ". " + tasks.get(j));
        }
    }

    public boolean isEmpty() {
        return tasks.isEmpty();
    }

    public boolean isValidTaskNumber(int taskNumber) {
        return taskNumber >= 1 && taskNumber <= tasks.size();
    }
}

