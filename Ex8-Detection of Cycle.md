# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List
## DATE: 26-09-2025
## AIM:
To write a program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
## Algorithm
1. Read the list elements, build the linked list, and store each node in an ArrayList for possible cycle creation.
2. Read pos and if it is valid, connect the last node’s next pointer to the node at index pos to form a cycle.
3. To detect a cycle, create an empty HashSet to store visited nodes.
4. Traverse the list; if a node is already in the set, return true because a cycle exists.
5. If traversal reaches null without repeats, return false and print the result.

## Program:
```JAVA
/*
program that detects a cycle in a linked list and returns the node where the cycle begins.
If there is no cycle, the program should return null without modifying the linked list.
Developed by: Prajin S
RegisterNumber: 212223230151
*/
import java.util.*;

public class Solution {

    static class ListNode {
        int val;
        ListNode next;
        ListNode(int val) {
            this.val = val;
            this.next = null;
        }
    }

    public boolean hasCycle(ListNode head) {
       //Type your Code Here
       Set<ListNode> visited = new HashSet<>();
        while (head != null) {
            if (visited.contains(head)) return true;
            visited.add(head);
            head = head.next;
        }
        return false;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();

       // System.out.print("Input: head = ");
        String headInput = sc.nextLine().trim();

        // Remove square brackets and split
        headInput = headInput.replaceAll("\\[|\\]", "");
        if (headInput.isEmpty()) {
            System.out.println("Output: false");
            return;
        }

        String[] values = headInput.split(",");
        int[] nums = Arrays.stream(values).mapToInt(Integer::parseInt).toArray();

        // Build the linked list
        ListNode head = new ListNode(nums[0]);
        ListNode current = head;
        List<ListNode> nodeList = new ArrayList<>();
        nodeList.add(head);

        for (int i = 1; i < nums.length; i++) {
            ListNode node = new ListNode(nums[i]);
            current.next = node;
            current = node;
            nodeList.add(node);
        }

        //System.out.print("pos = ");
        int pos = sc.nextInt();

        // Create cycle if pos is valid
        if (pos >= 0 && pos < nodeList.size()) {
            current.next = nodeList.get(pos);
        }

        boolean result = sol.hasCycle(head);
        System.out.println(result);
    }
}
```

## Output:
<img width="655" height="365" alt="image" src="https://github.com/user-attachments/assets/aeb211ba-2d6b-4d97-a217-4c3908c544cb" />



## Result:
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.
