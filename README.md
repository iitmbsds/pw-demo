# pw-demo
#include <iostream>
#include <vector>
#include <string>
using namespace std;

// Structure to represent a Student
struct Student {
    int id;
    string name;
    vector<string> enrolledCourses;
};

// Structure to represent a Course
struct Course {
    int id;
    string name;
    string description;
};

// Global vectors to store students and courses
vector<Student> students;
vector<Course> courses;

// Function to add a new student
void addStudent() {
    Student newStudent;
    cout << "Enter Student ID: ";
    cin >> newStudent.id;
    cin.ignore(); // Ignore leftover newline character
    cout << "Enter Student Name: ";
    getline(cin, newStudent.name);
    students.push_back(newStudent);
    cout << "Student added successfully!\n";
}

// Function to add a new course
void addCourse() {
    Course newCourse;
    cout << "Enter Course ID: ";
    cin >> newCourse.id;
    cin.ignore(); // Ignore leftover newline character
    cout << "Enter Course Name: ";
    getline(cin, newCourse.name);
    cout << "Enter Course Description: ";
    getline(cin, newCourse.description);
    courses.push_back(newCourse);
    cout << "Course added successfully!\n";
}

// Function to enroll a student in a course
void enrollStudentInCourse() {
    int studentId, courseId;
    cout << "Enter Student ID: ";
    cin >> studentId;
    cout << "Enter Course ID: ";
    cin >> courseId;

    // Find the student
    for (auto &student : students) {
        if (student.id == studentId) {
            // Find the course
            for (auto &course : courses) {
                if (course.id == courseId) {
                    student.enrolledCourses.push_back(course.name);
                    cout << "Enrolled successfully in course: " << course.name << "\n";
                    return;
                }
            }
            cout << "Course not found!\n";
            return;
        }
    }
    cout << "Student not found!\n";
}

// Function to display all students
void displayStudents() {
    if (students.empty()) {
        cout << "No students available.\n";
        return;
    }
    cout << "List of Students:\n";
    for (auto &student : students) {
        cout << "ID: " << student.id << ", Name: " << student.name << "\n";
        if (!student.enrolledCourses.empty()) {
            cout << "Enrolled Courses: ";
            for (auto &course : student.enrolledCourses) {
                cout << course << " ";
            }
            cout << "\n";
        }
    }
}

// Function to display all courses
void displayCourses() {
    if (courses.empty()) {
        cout << "No courses available.\n";
        return;
    }
    cout << "List of Courses:\n";
    for (auto &course : courses) {
        cout << "ID: " << course.id << ", Name: " << course.name
             << ", Description: " << course.description << "\n";
    }
}

// Main menu
void mainMenu() {
    while (true) {
        cout << "\n--- Educational App ---\n";
        cout << "1. Add Student\n";
        cout << "2. Add Course\n";
        cout << "3. Enroll Student in Course\n";
        cout << "4. Display Students\n";
        cout << "5. Display Courses\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        int choice;
        cin >> choice;

        switch (choice) {
            case 1: addStudent(); break;
            case 2: addCourse(); break;
            case 3: enrollStudentInCourse(); break;
            case 4: displayStudents(); break;
            case 5: displayCourses(); break;
            case 6: cout << "Exiting..."; return;
            default: cout << "Invalid choice. Try again.\n";
        }
    }
}

int main() {
    mainMenu();
    return 0;
}
