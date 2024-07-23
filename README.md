# EmployeeRecordSystem
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_NAME_LENGTH 50
#define MAX_DEPARTMENT_LENGTH 50
#define MAX_DESIGNATION_LENGTH 50

// Define the employee structure
struct employee {
    int id;
    char name[MAX_NAME_LENGTH];
    char department[MAX_DEPARTMENT_LENGTH];
    char designation[MAX_DESIGNATION_LENGTH];
    float salary;
};

// Define the linked list node structure
struct node {
    struct employee emp;
    struct node *next;
};

struct node *head = NULL;

// Function prototypes
struct node *createNode(struct employee emp);
void insertNode(struct employee emp);
void search(int id);

int main() {
    // Example usage:
    struct employee emp1 = {1, "John Doe", "HR", "Manager", 60000.0};
    struct employee emp2 = {2, "Jane Smith", "IT", "Developer", 70000.0};
    struct employee emp3 = {3, "Jenny", "HR", "Se.Manager", 80000.0};
    struct employee emp4 = {4, "harry", "HR", "Ju.manager", 50000.0};
    struct employee emp5 = {5, "sheena", "HR", "tester", 90000.0};
    
    insertNode(emp1);
    insertNode(emp2);
    insertNode(emp3);
    insertNode(emp4);
    insertNode(emp5);

    int searchId ;
    printf("enter the search id for the employee:\t");
    scanf("%d",&searchId);
    printf("Searching for employee with ID %d:\n", searchId);
    search(searchId);

    return 0;
}

// Function to create a new node
struct node *createNode(struct employee emp) {
    struct node *new_node = (struct node *)malloc(sizeof(struct node));
    if (new_node == NULL) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    new_node->emp = emp;
    new_node->next = NULL;
    return new_node;
}

// Function to insert a new node into the linked list
void insertNode(struct employee emp) {
    struct node *new_node = createNode(emp);
    if (head == NULL) {
        head = new_node;
    } else {
        new_node->next = head;
        head = new_node;
    }
}

// Function to search for an employee by ID
void search(int id) {
    struct node *ptr = head;
    while (ptr != NULL) {
        if (ptr->emp.id == id) {
            printf("ID: %d\n", ptr->emp.id);
            printf("Name: %s\n", ptr->emp.name);
            printf("Department: %s\n", ptr->emp.department);
            printf("Designation: %s\n", ptr->emp.designation);
            printf("Salary: %.2f\n", ptr->emp.salary);
            return;
        }
        ptr = ptr->next;
    }
    printf("Employee with ID %d not found.\n", id);
}
