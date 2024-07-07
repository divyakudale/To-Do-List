#include <iostream>
#include <vector>

struct Task {
    std::string description;
    bool completed;
};

// Function prototypes
void addTask(std::vector<Task>& taskList, const std::string& description);
void viewTasks(const std::vector<Task>& taskList);
void markAsCompleted(std::vector<Task>& taskList, int taskIndex);
void removeTask(std::vector<Task>& taskList, int taskIndex);

int main() {
    std::vector<Task> taskList;
    int choice;

    do {
        std::cout << "TODO LIST MANAGER" << std::endl;
        std::cout << "1. Add Task" << std::endl;
        std::cout << "2. View Tasks" << std::endl;
        std::cout << "3. Mark Task as Completed" << std::endl;
        std::cout << "4. Remove Task" << std::endl;
        std::cout << "5. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::string taskDescription;
                std::cout << "Enter task description: ";
                std::cin.ignore(); // Clear the input buffer
                std::getline(std::cin, taskDescription);
                addTask(taskList, taskDescription);
                break;
            }

            case 2:
                viewTasks(taskList);
                break;

            case 3: {
                int index;
                std::cout << "Enter the index of the task to mark as completed: ";
                std::cin >> index;
                markAsCompleted(taskList, index);
                break;
            }

            case 4: {
                int index;
                std::cout << "Enter the index of the task to remove: ";
                std::cin >> index;
                removeTask(taskList, index);
                break;
            }

            case 5:
                std::cout << "Exiting the program. Goodbye!" << std::endl;
                break;

            default:
                std::cout << "Invalid choice. Please enter a valid option." << std::endl;
        }

    } while (choice != 5);

    return 0;
}

void addTask(std::vector<Task>& taskList, const std::string& description) {
    Task newTask{description, false};
    taskList.push_back(newTask);
    std::cout << "Task added successfully!" << std::endl;
}

void viewTasks(const std::vector<Task>& taskList) {
    if (taskList.empty()) {
        std::cout << "No tasks to display. Add tasks first." << std::endl;
        return;
    }

    std::cout << "TODO LIST" << std::endl;
    std::cout << "--------------------------------------" << std::endl;
    for (size_t i = 0; i < taskList.size(); ++i) {
        std::cout << i + 1 << ". ";
        std::cout << taskList[i].description;
        if (taskList[i].completed) {
            std::cout << " [Completed]";
        }
        std::cout << std::endl;
    }
    std::cout << "--------------------------------------" << std::endl;
}

void markAsCompleted(std::vector<Task>& taskList, int taskIndex) {
    if (taskIndex >= 1 && taskIndex <= static_cast<int>(taskList.size())) {
        taskList[taskIndex - 1].completed = true;
        std::cout << "Task marked as completed!" << std::endl;
    } else {
        std::cout << "Invalid task index. Please enter a valid index." << std::endl;
    }
}

void removeTask(std::vector<Task>& taskList, int taskIndex) {
    if (taskIndex >= 1 && taskIndex <= static_cast<int>(taskList.size())) {
        taskList.erase(taskList.begin() + taskIndex - 1);
        std::cout << "Task removed successfully!" << std::endl;
    } else {
        std::cout << "Invalid task index. Please enter a valid index." << std::endl;
    }
}