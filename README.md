# Bubble-Sort-Quick-Sort
Bubble Sort &amp; Quick Sort
# Student Record Sorting in C (Bubble Sort & Quick Sort)

##  Overview

This program demonstrates sorting of **student records** using **Bubble Sort** and **Quick Sort** algorithms.  
Each student record contains:
- Name
- Roll Number
- Total Marks  

The program dynamically allocates memory for student records and performs sorting by **Roll Number**.  


---
## 📌 Algorithm
Start

Input the number of student records n_vnk.

Allocate memory dynamically for st_vnk[n_vnk].

Assign random name_vnk, roll_no_vnk, and total_marks_vnk to each student.

Print all student records before sorting.

Perform Bubble Sort:

Compare adjacent records by student_roll_no_vnk.

Swap if necessary.

Count the number of swaps.

Print records after Bubble Sort.

Perform Quick Sort:

Choose pivot (last element).

Partition array into smaller and larger elements.

Recursively sort subarrays.

Print records after Quick Sort.

Free dynamically allocated memory.

End.

---

## 📌 Pseudocode
```
START

Input n_vnk
Allocate st_vnk[n_vnk]

FOR i_vnk = 0 to n_vnk-1
st_vnk[i_vnk].student_name_vnk = random name
st_vnk[i_vnk].student_roll_no_vnk = random/assigned roll number
st_vnk[i_vnk].total_marks_vnk = random marks
END FOR

Print all records (Before Sorting)

CALL bubbleSort_vnk(st_vnk, n_vnk)
Print all records (After Bubble Sort)

CALL quickSort_vnk(st_vnk, 0, n_vnk-1)
Print all records (After Quick Sort)

Free memory

END
## 📌 Dry Run Example

### Input:  
### Number of records: 5  

### Randomly generated records:
```
| Roll No | Name  | Total Marks |
|---------|-------|-------------|
| 10      | Abir  | 75          |
| 3       | Priya | 62          |
| 7       | Rohan | 89          |
| 1       | Isha  | 54          |
| 5       | Neha  | 70          |
```
### Bubble Sort:

- Compare adjacent roll numbers:
  - Swap if left > right
- Number of swaps = 4
- Sorted order after Bubble Sort:
```
| Roll No | Name  | Total Marks |
|---------|-------|-------------|
| 1       | Isha  | 54          |
| 3       | Priya | 62          |
| 5       | Neha  | 70          |
| 7       | Rohan | 89          |
| 10      | Abir  | 75          |
```
### Quick Sort:

- Pivot = last element
- Partition array around pivot
- Recursively sort left and right
- Final sorted order (same as Bubble Sort)

---
📌 C++ Program
#include <iostream>
#include <cstdlib>
#include <cstring>
using namespace std;

#define NAME_LEN_vnk 50

struct student_vnk {
    char student_name_vnk[NAME_LEN_vnk];
    int student_roll_no_vnk;
    int total_marks_vnk;
};

void bubbleSort_vnk(student_vnk*, int);
void quickSort_vnk(student_vnk*, int, int);
int partition_vnk(student_vnk*, int, int);
void swapping_vnk(student_vnk*, student_vnk*);

int main() {
    int n_vnk, i_vnk;
    int start_vnk = 0; 

    cout << "Enter the number of records you want: ";
    cin >> n_vnk;

    student_vnk* st_vnk = new student_vnk[n_vnk];

    const char* names_vnk[] = { "Abir","Aarav","Isha","Rohan","Priya","Vikas","Neha","Sahil","Anaya","Dev",
                            "Kriti","Mira","Kabir","Tanvi","Yash","Riya","Arjun","Asha","Nikhil","Pooja",
                            "Kunal","Vishal","Amir","Sharukh","Salman","Mrunal","Kirti" };
    int name_size_vnk = sizeof(names_vnk) / sizeof(names_vnk[0]);

    const int roll_no_vnk[] = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10, 19, 11, 12, 14, 16, 13, 15, 18, 17};
    int roll_size_vnk = sizeof(roll_no_vnk) / sizeof(roll_no_vnk[0]);

    // Fill student records
    for (i_vnk = 0; i_vnk < n_vnk; i_vnk++) {
        strcpy(st_vnk[i_vnk].student_name_vnk, names_vnk[rand() % name_size_vnk]);
        st_vnk[i_vnk].student_roll_no_vnk = roll_no_vnk[i_vnk % roll_size_vnk];
        st_vnk[i_vnk].total_marks_vnk = rand() % 100;
    }

    // Print before sorting
    cout << "\n---- Before Sorting ----\n";
    for (i_vnk = 0; i_vnk < n_vnk; i_vnk++) {
        cout << "Name: " << st_vnk[i_vnk].student_name_vnk
             << " || Roll no: " << st_vnk[i_vnk].student_roll_no_vnk
             << " || Total marks: " << st_vnk[i_vnk].total_marks_vnk << endl;
    }

    cout << "\n---- After Bubble Sort ----\n";
    bubbleSort_vnk(st_vnk, n_vnk);

    cout << "\n---- After Quick Sort ----\n";
    quickSort_vnk(st_vnk, start_vnk, n_vnk-1);
    for (i_vnk = 0; i_vnk < n_vnk; i_vnk++) {
        cout << "Name: " << st_vnk[i_vnk].student_name_vnk
             << " || Roll No: " << st_vnk[i_vnk].student_roll_no_vnk
             << " || Total marks: " << st_vnk[i_vnk].total_marks_vnk << endl;
    }

    delete[] st_vnk;
    return 0;
}

void bubbleSort_vnk(student_vnk* st_vnk, int n_vnk) {
    int i_vnk, j_vnk, count_vnk = 0;
    student_vnk temp_vnk;

    for (i_vnk = 0; i_vnk < n_vnk - 1; i_vnk++) {
        for (j_vnk = 0; j_vnk < n_vnk - i_vnk - 1; j_vnk++) {
            if (st_vnk[j_vnk].student_roll_no_vnk > st_vnk[j_vnk+1].student_roll_no_vnk) {
                temp_vnk = st_vnk[j_vnk];
                st_vnk[j_vnk] = st_vnk[j_vnk+1];
                st_vnk[j_vnk+1] = temp_vnk;
                count_vnk++;
            }
        }
    }

    cout << "Number of swaps: " << count_vnk << endl;
    for (i_vnk = 0; i_vnk < n_vnk; i_vnk++) {
        cout << "Name: " << st_vnk[i_vnk].student_name_vnk
             << " || Roll No: " << st_vnk[i_vnk].student_roll_no_vnk
             << " || Total marks: " << st_vnk[i_vnk].total_marks_vnk << endl;
    }
}

void quickSort_vnk(student_vnk* st_vnk, int start_vnk, int size_vnk){
    if(start_vnk < size_vnk){
        int pivotIdx_vnk = partition_vnk(st_vnk, start_vnk, size_vnk);
        quickSort_vnk(st_vnk, start_vnk, pivotIdx_vnk-1);
        quickSort_vnk(st_vnk, pivotIdx_vnk+1, size_vnk);
    }
}

int partition_vnk(student_vnk* st_vnk, int start_vnk, int size_vnk){
    int idx_vnk = start_vnk-1;
    int pivot_vnk = st_vnk[size_vnk].student_roll_no_vnk;
    for(int j_vnk= start_vnk; j_vnk<size_vnk; j_vnk++){
        if(st_vnk[j_vnk].student_roll_no_vnk <= pivot_vnk){
            idx_vnk++;
            swapping_vnk(&st_vnk[idx_vnk], &st_vnk[j_vnk]);
        }
    }
    idx_vnk++;
    swapping_vnk(&st_vnk[idx_vnk], &st_vnk[size_vnk]);
    return idx_vnk;
}

void swapping_vnk(student_vnk* a_vnk, student_vnk* b_vnk){
    student_vnk temp_vnk = *a_vnk;
    *a_vnk = *b_vnk;
    *b_vnk = temp_vnk;
}

## output
Enter the number of records you want: 5

---- Before Sorting ----
Name: Priya || Roll no: 10 || Total marks: 72
Name: Rohan || Roll no: 3 || Total marks: 88
Name: Isha  || Roll no: 7 || Total marks: 65
Name: Abir  || Roll no: 1 || Total marks: 54
Name: Neha  || Roll no: 5 || Total marks: 90

---- After Bubble Sort ----
Number of swaps: 6
Name: Abir  || Roll No: 1 || Total marks: 54
Name: Rohan || Roll No: 3 || Total marks: 88
Name: Neha  || Roll No: 5 || Total marks: 90
Name: Isha  || Roll No: 7 || Total marks: 65
Name: Priya || Roll No: 10 || Total marks: 72

---- After Quick Sort ----
Name: Abir  || Roll No: 1 || Total marks: 54
Name: Rohan || Roll No: 3 || Total marks: 88
Name: Neha  || Roll No: 5 || Total marks: 90
Name: Isha  || Roll No: 7 || Total marks: 65
Name: Priya || Roll No: 10 || Total marks: 72

## dry run photos
![img Alt](https://github.com/vijay1234nkanade-boop/Bubble-Sort-Quick-Sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2013.06.07_67e447cd.jpg?raw=true)
![img Alt](https://github.com/vijay1234nkanade-boop/Bubble-Sort-Quick-Sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2013.06.08_a12d614f.jpg?raw=true)

![img Alt](https://github.com/vijay1234nkanade-boop/Bubble-Sort-Quick-Sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2013.06.08_7c27fafe.jpg?raw=true)

![img Alt](https://github.com/vijay1234nkanade-boop/Bubble-Sort-Quick-Sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2013.09.52_b581f700.jpg?raw=true)


