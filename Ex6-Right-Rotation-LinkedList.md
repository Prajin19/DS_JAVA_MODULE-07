# Ex6 Right Rotation LinkedList
## DATE: 26-09-2025
## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Read n and build the linked list by inserting nodes one by one.
2. Read k and call the rotate function to rotate the list.
3. In rotate, find the length of the list and connect the last node to the head to form a circular list.
4. Compute the effective rotation using k % length, move to the new tail, and set the next node as the new head.
5. Break the circular link, return the new head, and display the rotated list.

## Program:
```JAVA
/*
Program to  Right Rotation LinkedList
Developed by: Prajin S
RegisterNumber: 212223230151
*/
import java.util.Scanner;
public class RotateLinkedList {
    public static Node rotate(Node head, int k) {
       //Type your code here
       if(head==null || head.next==null || k==0)
       return head;
       
       Node temp=head;
       int l=1;
       while(temp.next!=null){
           temp=temp.next;
           l++;
       }
       temp.next=head;
       k%=l;
       int st=l-k;
       Node newtail=temp;
       for(int i=1;i<=st;i++)
       newtail=newtail.next;
       Node newHead=newtail.next;
       newtail.next=null;
       return newHead;
       
    }
    public static void display(Node head) {
        Node current = head;
        System.out.print("LinkedList: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Node head = null, tail = null;
        int n = scanner.nextInt();
        for (int i = 0; i < n; i++) {
            Node newNode = new Node(scanner.nextInt());
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        int k = scanner.nextInt();
        head = rotate(head, k);
        display(head);
        scanner.close();
    }
}
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

```

## Output:
<img width="863" height="324" alt="image" src="https://github.com/user-attachments/assets/d4cb65fa-f995-4bfd-8b20-1e5bf35aca2f" />



## Result:
Thus, the C program to perfom right rotation on linked list is implemented successfully.
