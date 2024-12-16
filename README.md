**# Linked-List-03**#include <stdio.h>
#include <stdlib.h>
// Define the Node structure for a doubly linked list
struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
};
// Define the DoublyLinkedList structure
struct DoublyLinkedList {
    struct Node* head;
    struct Node* tail;
};
// Function to initialize a new doubly linked list
void initList(struct DoublyLinkedList* list) {
    list->head = NULL;
    list->tail = NULL;
}
// Function to insert a node at the head of the list
void insertAtHead(struct DoublyLinkedList* list, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->prev = NULL;
    newNode->next = list->head;

    if (list->head != NULL) {
        list->head->prev = newNode;
    }
 list->head = newNode;
    if (list->tail == NULL) {
        list->tail = newNode;
    }
}
// Function to insert a node at the tail of the list
void insertAtTail(struct DoublyLinkedList* list, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = NULL;
    newNode->prev = list->tail;

    if (list->tail != NULL) {
        list->tail->next = newNode;
    }
    list->tail = newNode;
    if (list->head == NULL) {
        list->head = newNode;
    }
}
// Function to delete a node from the head of the list
void deleteFromHead(struct DoublyLinkedList* list) {
    if (list->head == NULL) {
        printf("The list is already empty.\n");
        return;
    }
    struct Node* temp = list->head;
    list->head = list->head->next;
    if (list->head != NULL) {
        list->head->prev = NULL;
    }
   free(temp);
   // If the list becomes empty after deletion, update the tail
    if (list->head == NULL) {
        list->tail = NULL;
    }
}
// Function to delete a node from the tail of the list
void deleteFromTail(struct DoublyLinkedList* list) {
    if (list->tail == NULL) {
        printf("The list is already empty.\n");
        return;
    }
   struct Node* temp = list->tail;
    list->tail = list->tail->prev;

    if (list->tail != NULL) {
        list->tail->next = NULL;
    }
   free(temp);
   // If the list becomes empty after deletion, update the head
    if (list->tail == NULL) {
        list->head = NULL;
    }
}
// Function to print the entire doubly linked list
void printList(struct DoublyLinkedList* list) {
    struct Node* temp = list->head;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}
int main() {
    struct DoublyLinkedList list;
    initList(&list);
    // Insert elements at the head and tail of the list
    insertAtHead(&list, 5);
    insertAtHead(&list, 10);
    insertAtTail(&list, 15);
    insertAtTail(&list, 20);
    printf("List: ");
    printList(&list);
// Delete elements from the head and tail of the list
    deleteFromHead(&list);
    deleteFromTail(&list);
    printf("List after deletions: ");
    printList(&list);
    return 0;
}
