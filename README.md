#include <iostream>
#include <string>
#include <fstream>
#include<algorithm>

using namespace std;

class Student {
    string name;
    float marks[5]; // Modified for 5 subjects
    float total;
    float average;
    float percentage;

public:
    string getName() const { return name; }
    void setName(const string& newName) { name = newName; }

    void getdata() {
        cout << "Enter student name: ";
        cin >> name;
        for (int i = 0; i < 5; i++) {
            string subject;
            if (i == 0) subject = "Maths";
            else if (i == 1) subject = "AEC";
            else if (i == 2) subject = "DT";
            else if (i == 3) subject ="A&DC";
            else if (i == 4) subject ="OOP";
            // Add more subjects as needed

            cout << "Enter marks in " << subject << ": ";
            cin >> marks[i];
        }
    }

    void calculate() {
        total = 0;
        for (int i = 0; i < 5; i++) {
            total += marks[i];
        }
        average = total / 5; 
        percentage = (total / (5 * 100)) * 100; 
    }

    float getPercentage() const {
        return percentage;
    }

    void display(int rank) const {
        cout << "Student Name: " << name << endl;
        for (int i = 0; i < 5; i++) {
            string subject;
            if (i == 0) subject = "Maths";
            else if (i == 1) subject = "AEC";
            else if (i == 2) subject = "DT";
            else if (i == 3) subject ="A&DC";
            else if (i == 4) subject ="OOP";
            // Add more subjects as needed

            cout << subject << " Marks: " << marks[i] << endl;
        }
        cout << "Total Marks: " << total << endl;
        cout << "Average Marks: " << average << endl;
        cout << "Percentage: " << percentage << "%" << endl;
        cout << "Rank: " << rank << endl;
    }

    void store(ofstream& file, int rank) const {
        file << "Student Name: " << name << "\n";
        for (int i = 0; i < 5; i++) {
            string subject;
            if (i == 0) subject = "Maths";
            else if (i == 1) subject = "AEC";
            else if (i == 2) subject = "DT";
            else if (i == 3) subject ="A&DC";
            else if (i == 4) subject ="OOP";
                        // Add more subjects as needed

            file << subject << " Marks: " << marks[i] << "\n";
        }
        file << "Total Marks: " << total << "\n";
        file << "Average Marks: " << average << "\n";
        file << "Percentage: " << percentage << "%" << "\n";
        file << "Rank: " << rank << "\n\n";
    }
};

int main() {
    int n = 3; // Number of students

    Student students[n];

    for (int i = 0; i < n; i++) {
        students[i].getdata();
        students[i].calculate();
    }

    // Sorting students based on their percentage
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (students[j].getPercentage() > students[i].getPercentage()) {
                swap(students[i], students[j]);
            }
        }
    }

    ofstream file("results.txt");

    for (int i = 0; i < n; i++) {
        students[i].display(i + 1);
        students[i].store(file, i + 1);
    }

    file.close();

    return 0;
}

