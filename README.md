#include <iostream>
#include <vector>
#include <string>

class Student {
public:
    int rollNumber;
    std::string name;
    int age;
    std::string grade;

    Student(int roll, std::string name, int age, std::string grade) {
        this->rollNumber = roll;
        this->name = name;
        this->age = age;
        this->grade = grade;
    }

    void display() {
        std::cout << "Roll Number: " << rollNumber << std::endl;
        std::cout << "Name: " << name << std::endl;
        std::cout << "Age: " << age << std::endl;
        std::cout << "Grade: " << grade << std::endl;
    }
};

class StudentManagementSystem {
private:
    std::vector<Student> students;

public:
    void addStudent(int roll, std::string name, int age, std::string grade) {
        Student newStudent(roll, name, age, grade);
        students.push_back(newStudent);
        std::cout << "Student added successfully!" << std::endl;
    }

    void displayAllStudents() {
        for (Student student : students) {
            student.display();
            std::cout << "--------------------------" << std::endl;
        }
    }

    void deleteStudent(int roll) {
        for (auto it = students.begin(); it != students.end(); ++it) {
            if (it->rollNumber == roll) {
                students.erase(it);
                std::cout << "Student deleted successfully!" << std::endl;
                return;
            }
        }
        std::cout << "Student with Roll Number " << roll << " not found." << std::endl;
    }

    void updateStudent(int roll, std::string name, int age, std::string grade) {
        for (auto &student : students) {
            if (student.rollNumber == roll) {
                student.name = name;
                student.age = age;
                student.grade = grade;
                std::cout << "Student updated successfully!" << std::endl;
                return;
            }
        }
        std::cout << "Student with Roll Number " << roll << " not found." << std::endl;
    }
};

int main() {
    StudentManagementSystem sms;
    int choice;

    while (true) {
        std::cout << "\nStudent Management System" << std::endl;
        std::cout << "1. Add Student" << std::endl;
        std::cout << "2. Display All Students" << std::endl;
        std::cout << "3. Delete Student" << std::endl;
        std::cout << "4. Update Student" << std::endl;
        std::cout << "5. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        if (choice == 5) {
            break;
        }

        int roll;
        std::string name;
        int age;
        std::string grade;

        switch (choice) {
            case 1:
                std::cout << "Enter Roll Number: ";
                std::cin >> roll;
                std::cout << "Enter Name: ";
                std::cin.ignore();
                std::getline(std::cin, name);
                std::cout << "Enter Age: ";
                std::cin >> age;
                std::cout << "Enter Grade: ";
                std::cin.ignore();
                std::getline(std::cin, grade);
                sms.addStudent(roll, name, age, grade);
                break;
            case 2:
                sms.displayAllStudents();
                break;
            case 3:
                std::cout << "Enter Roll Number to delete: ";
                std::cin >> roll;
                sms.deleteStudent(roll);
                break;
            case 4:
                std::cout << "Enter Roll Number to update: ";
                std::cin >> roll;
                std::cout << "Enter new Name: ";
                std::cin.ignore();
                std::getline(std::cin, name);
                std::cout << "Enter new Age: ";
                std::cin >> age;
                std::cout << "Enter new Grade: ";
                std::cin.ignore();
                std::getline(std::cin, grade);
                sms.updateStudent(roll, name, age, grade);
                break;
            default:
                std::cout << "Invalid choice. Please try again." << std::endl;
        }
    }

    return 0;
}
