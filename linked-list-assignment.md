# Linked List Implementation Assignment
**Course:** CS505.2025.T1  
**Student Name:** Wael Mohamed Abo-Samra  
**Student ID:** 202300451  
**Submitted to:** Dr. Mostafa Ezzat  

## LinkedListBasic.h
```cpp

#ifndef LINKED_LIST_BASIC_H
#define LINKED_LIST_BASIC_H

template <typename T>
class LinkedList {
private:
    struct Node {
        T data;
        Node* next;
        Node(const T& value) : data(value), next(nullptr) {}
    };
    Node* head;
    int size;

public:
    LinkedList() : head(nullptr), size(0) {}
    
    ~LinkedList() {
        while (head != nullptr) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }

    void insertAtBeginning(const T& data) {
        Node* newNode = new Node(data);
        newNode->next = head;
        head = newNode;
        size++;
    }

    void insertAtEnd(const T& data) {
        Node* newNode = new Node(data);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = newNode;
        }
        size++;
    }

    void deleteNode(const T& data) {
        if (head == nullptr) return;
        
        if (head->data == data) {
            Node* temp = head;
            head = head->next;
            delete temp;
            size--;
            return;
        }

        Node* current = head;
        while (current->next != nullptr && current->next->data != data) {
            current = current->next;
        }

        if (current->next != nullptr) {
            Node* temp = current->next;
            current->next = temp->next;
            delete temp;
            size--;
        }
    }

    void printList() const {
        Node* current = head;
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }

    bool isEmpty() const {
        return head == nullptr;
    }

    int length() const {
        return size;
    }
};
#endif

```

## 2. main.cpp

```cpp
#include <iostream>
#include "LinkedListBasic.h"

int main() {
    LinkedList<int> list;
    
    std::cout << "Testing insertions..." << std::endl;
    list.insertAtBeginning(1);
    list.insertAtEnd(2);
    list.insertAtEnd(3);
    
    std::cout << "Initial list: ";
    list.printList();
    
    std::cout << "Deleting node with value 2..." << std::endl;
    list.deleteNode(2);
    
    std::cout << "After deletion: ";
    list.printList();
    
    std::cout << "List length: " << list.length() << std::endl;
    std::cout << "Is list empty? " << (list.isEmpty() ? "Yes" : "No") << std::endl;
    
    return 0;
}
```

