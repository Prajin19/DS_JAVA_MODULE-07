# Flattening a Nested List Using an Iterator
## DATE: 26-09-2025
## AIM:
To design and implement a class NestedIterator that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (next() and hasNext()).
## Algorithm
1. Read the nested list string input and parse it using a stack-based parser to build a NestedInteger structure.
2. In the NestedIterator constructor, call flattenList to recursively traverse the NestedInteger list.
3. During flattenList, if an element is an integer, add it to the integers list; otherwise recursively flatten its inner list.
4. Use position to track iteration; next() returns integers[position++] and hasNext() checks if position is less than the list size.
5. Iterate using the iterator, collect all integers in a list, and print the final flattened output.

## Program:
```JAVA
/*
Program to find Flattening a Nested List Using an Iterator
Developed by: Prajin S
RegisterNumber: 212223230151
*/
import java.util.*;

public class NestedIterator implements Iterator<Integer> {
    private List<Integer> integers = new ArrayList<>();
    private int position = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flattenList(nestedList);
    }

    private void flattenList(List<NestedInteger> nestedList) {
        for (NestedInteger element : nestedList) {
            if (element.isInteger()) {
                integers.add(element.getInteger());
            } else {
                flattenList(element.getList());
            }
        }
    }

    @Override
    public Integer next() {
        return integers.get(position++);
    }

    @Override
    public boolean hasNext() {
        return position < integers.size();
    }

    // Parse string into NestedInteger structure
    public static List<NestedInteger> parse(String s) {
        Stack<List<NestedInteger>> stack = new Stack<>();
        List<NestedInteger> curr = new ArrayList<>();
        int num = 0;
        boolean hasNum = false;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '[') {
                stack.push(curr);
                curr = new ArrayList<>();
            } else if (c == ']') {
                if (hasNum) {
                    curr.add(new SimpleNestedInteger(num));
                    hasNum = false;
                    num = 0;
                }
                List<NestedInteger> completed = curr;
                curr = stack.pop();
                curr.add(new SimpleNestedInteger(completed));
            } else if (c == ',') {
                if (hasNum) {
                    curr.add(new SimpleNestedInteger(num));
                    hasNum = false;
                    num = 0;
                }
            } else if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
                hasNum = true;
            }
        }
        return curr;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();

        List<NestedInteger> nestedList = parse(input);

        NestedIterator iterator = new NestedIterator(nestedList);
        List<Integer> output = new ArrayList<>();
        while (iterator.hasNext()) {
            output.add(iterator.next());
        }

        System.out.println(output);
    }
}

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class SimpleNestedInteger implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    public SimpleNestedInteger(Integer value) {
        this.value = value;
        this.list = null;
    }

    public SimpleNestedInteger(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    @Override
    public boolean isInteger() {
        return value != null;
    }

    @Override
    public Integer getInteger() {
        return value;
    }

    @Override
    public List<NestedInteger> getList() {
        return list;
    }
}

```

## Output:
<img width="736" height="278" alt="image" src="https://github.com/user-attachments/assets/a1f4f64a-ec07-45f8-9817-1d727e4e755c" />


## Result:
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
