# Ex7 Removal of Nodes with a Specific Value from a Linked List
## DATE: 26-09-2025
## AIM:
To write a java  program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm
1. Read the list elements as a comma-separated string, convert them into an integer array, and build the linked list.
2. Read the value val that needs to be removed from the list.
3. Create a sentinel node pointing to the head to simplify deletions, especially at the head.
4. Traverse the list using two pointers; if a node’s value equals val, bypass it by linking prev.next to curr.next, otherwise move prev forward.
5. Return sentinel.next as the new head and print the resulting list.

## Program:
```JAVA
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: Prajin S
RegisterNumber: 212223230151
*/
import java.util.*;

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}

class Solution {
    public ListNode removeElements(ListNode head, int val) {
        //Type your code here
        ListNode sentinel = new ListNode(0);
        sentinel.next = head;

        ListNode prev = sentinel, curr = head;
        while (curr != null) {
            if (curr.val == val)
                prev.next = curr.next;
            else
                prev = curr;
            curr = curr.next;
        }
        return sentinel.next;
    }
}

public class Main {

    public static ListNode buildList(int[] arr) {
        if (arr.length == 0) return null;
        ListNode head = new ListNode(arr[0]);
        ListNode current = head;
        for (int i = 1; i < arr.length; i++) {
            current.next = new ListNode(arr[i]);
            current = current.next;
        }
        return head;
    }

    public static String listToString(ListNode head) {
        List<Integer> result = new ArrayList<>();
        while (head != null) {
            result.add(head.val);
            head = head.next;
        }
        return result.toString(); 
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

     
        String input = scanner.nextLine().replaceAll("\\s", "");
        int[] nums = Arrays.stream(input.split(",")).mapToInt(Integer::parseInt).toArray();

       
       
        int val = scanner.nextInt();

        ListNode head = buildList(nums);
        Solution solution = new Solution();
        ListNode updated = solution.removeElements(head, val);

        System.out.println(listToString(updated));

        scanner.close();
    }
}

```

## Output:
<img width="707" height="363" alt="image" src="https://github.com/user-attachments/assets/04758175-c1db-4720-b1ad-50919529c038" />



## Result:
The java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.
