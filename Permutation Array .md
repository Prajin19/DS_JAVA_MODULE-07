# Ex9 Finding the Longest Length of Nested Set in a Permutation Array
## DATE: 26-09-2025
## AIM:
To write a program that finds the length of the longest set s[k] defined as s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … },where the iteration stops before a duplicate element occurs.

The task is to return the maximum size among all such sets.
## Algorithm
1. Read the input array, remove formatting characters, split it by commas, and convert each part into an integer to form nums.
2. Create a visited array of the same size to track which indices have been visited.
3. Loop through each index; if it is not visited, start following the chain nums[i], nums[nums[i]], and so on.
4. Mark each visited index as true and count how many elements are traversed until a repeat is encountered.
5. Track and update the maximum chain length found and finally return and print that maximum length.

## Program:
```JAVA
/*
Program to find the Longest Length of Nested Set in a Permutation Array
Developed by: Prajin S
RegisterNumber: 212223230151
*/
import java.util.*;
public class ArrayNestingMain {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine().trim();
        input = input.replace("nums =", "").replace("[", "").replace("]", "").trim();
        String[] parts = input.split(",");
        int[] nums = new int[parts.length];

        for (int i = 0; i < parts.length; i++) {
            nums[i] = Integer.parseInt(parts[i].trim());
        }
        Solution sol = new Solution();
        int result = sol.arrayNesting(nums);
        System.out.println(result);
        sc.close();
    }
}
class Solution {
    public int arrayNesting(int[] nums) {
      int n=nums.length;
      boolean[] visited=new boolean[n];
      int maxlen=0;
      for(int i=0;i<n;i++)
      {
          if(!visited[i])
          {
              int count=0;
              int j=i;
              while(!visited[j])
              {
                  visited[j]=true;
                  j=nums[j];
                  count++;
              }
          maxlen=Math.max(maxlen,count);
          }
      }
      return maxlen;
    }
}


```

## Output:
<img width="628" height="280" alt="image" src="https://github.com/user-attachments/assets/aa5e4344-bc61-4867-912f-47db7b9a85f5" />



## Result:
The program successfully computes the longest length of the nested set s[k] for the given permutation array.
