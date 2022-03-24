---
layout: "post"
title: "Java - adding element at beginning ArrayList vs LinkedList"
categories: "java data structure"
permalink: "/:categories/:year/:month/:day/:title.html"
---

This program tests the performance of ArrayList vs LinkedList by adding elements at beginning of the list:
```
import java.util.ArrayList;
import java.util.LinkedList;

public class ArrayListVsLinkedList {

    private static final int TEST_SIZE = 500000;

    public static void main(String[] args) {

        ArrayList<Integer> arrayList = new ArrayList<>();
        long startTime = System.currentTimeMillis();
        for (int i = 0; i < TEST_SIZE; ++i) {
            arrayList.add(0,i);
        }
        System.out.println("Time taken for adding Integer to the beginning of ArrayList: " + (System.currentTimeMillis() - startTime));

        LinkedList<Integer> linkedList = new LinkedList<>();
        startTime = System.currentTimeMillis();
        for (int i = 0; i < TEST_SIZE; ++i) {
            linkedList.addFirst(i);
        }
        System.out.println("Time taken for adding Integer to the beginning of LinkedList: " + (System.currentTimeMillis() - startTime));
    }
}

```

Execute the program:
```
Time taken for adding Integer to the beginning of ArrayList: 23349
Time taken for adding Integer to the beginning of LinkedList: 107
```

It took longer time for adding elements at the beginning of an ArrayList since the java will need to shift all the existing elements in the ArrayList to the right!
