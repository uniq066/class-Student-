# class-Student-

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm> // Для сортировки
using namespace std;

class Student {
private:
    string name;      // Имя студента
    int age;          // Возраст студента
    float gpa;        // Средний балл
    string major;     // Специальность

public:
    // Конструктор по умолчанию
    Student() : name("Unknown"), age(0), gpa(0.0), major("Undeclared") {}

    // Конструктор с параметрами
    Student(string n, int a, float g, string m) : name(n), age(a), gpa(g), major(m) {}

    // Методы доступа
    string getName() const { return name; }
    int getAge() const { return age; }
    float getGPA() const { return gpa; }
    string getMajor() const { return major; }

    void setName(string n) { name = n; }
    void setAge(int a) { age = a; }
    void setGPA(float g) { gpa = g; }
    void setMajor(string m) { major = m; }

    // Метод для получения статуса студента на основе GPA
    string getStatus() const {
        if (gpa >= 3.5) return "Honor Student";
        else if (gpa >= 2.0) return "Regular Student";
        else return "At Risk";
    }

    // Метод для вывода информации о студенте
    void display() const {
        cout << "Name: " << name << ", Age: " << age << ", GPA: " << gpa 
             << ", Major: " << major << ", Status: " << getStatus() << endl;
    }
};

// Функция для отображения меню
void displayMenu() {
    cout << "Menu:" << endl;
    cout << "1. Add empty student" << endl;
    cout << "2. Add student with data" << endl;
    cout << "3. Edit student data" << endl;
    cout << "4. Display all students" << endl;
    cout << "5. Sort students by GPA" << endl;
    cout << "6. Exit" << endl;
}

int main() {
    vector<Student> students; // Массив объектов Student
    int choice;

    do {
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: { // Добавление пустого студента
                students.push_back(Student());
                cout << "Empty student added." << endl;
                break;
            }
            case 2: { // Добавление студента с данными
                string name, major;
                int age;
                float gpa;
                cout << "Enter name: ";
                cin >> name;
                cout << "Enter age: ";
                cin >> age;
                cout << "Enter GPA: ";
                cin >> gpa;
                cout << "Enter major: ";
                cin >> major;
                students.push_back(Student(name, age, gpa, major));
                cout << "Student added." << endl;
                break;
            }
            case 3: { // Редактирование данных студента
                int index;
                cout << "Enter student index to edit (0 to " << students.size() - 1 << "): ";
                cin >> index;
                if (index >= 0 && index < students.size()) {
                    string name, major;
                    int age;
                    float gpa;
                    cout << "Enter new name: ";
                    cin >> name;
                    cout << "Enter new age: ";
                    cin >> age;
                    cout << "Enter new GPA: ";
                    cin >> gpa;
                    cout << "Enter new major: ";
                    cin >> major;
                    students[index].setName(name);
                    students[index].setAge(age);
                    students[index].setGPA(gpa);
                    students[index].setMajor(major);
                    cout << "Student data updated." << endl;
                } else {
                    cout << "Invalid index." << endl;
                }
                break;
            }
            case 4: { // Вывод информации обо всех студентах
                for (const auto& student : students) {
                    student.display();
                }
                break;
            }
            case 5: { // Сортировка студентов по GPA
                sort(students.begin(), students.end(), [](const Student  &a, const Student &b) {
                    return a.getGPA() < b.getGPA(); // Сортировка по возрастанию GPA
                });
                cout << "Students sorted by GPA." << endl;
                break;
            }
            case 6: // Завершение работы программы
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 6);

    return 0;
}
```
