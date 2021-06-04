#### LinkedList



```java
// reverse a linked list (Recursion)
public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null)
            return head;
        
        ListNode p = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return p;
    }

// no Recursion
public ListNode reverseList(ListNode head) {
        
        ListNode prev = null;
        while(head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        
        return prev;
    }
```



#### ArrayList







#### addAll()



#### convert list to array

```java
List<Integer> list = new ArrayList<>();
list.toArray(new int[4]);
```

```java
List<String> res = new ArrayList<>();
return res.toArray(new String[res.size()]);
```

