<div id="top"></div>

# Linked List

<details>

<summary>Table of contents</summary>

- [Floyd’s Cycle Detection Algorithm](#floyds-cycle-detection-algorithm)

</details>

## Floyd’s Cycle Detection Algorithm

- **Purpose:** Detect if a linked list contains a cycle (loop) using two pointers — a slow one and a fast one.
- **Working:**
  - slow moves one node at a time.
  - fast moves two nodes at a time.
  - If there’s a cycle, both pointers will meet at some node inside the cycle.
  - If there's no cycle, fast will reach the end (null).

- **Logic**
```
public boolean hasCycle(ListNode head) {
        ListNode slow_p = head, fast_p = head;
        while(fast_p != null && fast_p.next != null) {
            slow_p = slow_p.next;
            fast_p = fast_p.next.next;
            if(slow_p == fast_p)return true;
        }
        return false;
    }
```

<p align="right">(<a href="#top">back to top</a>)</p>

<hr/>

