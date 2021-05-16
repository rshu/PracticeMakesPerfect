template

第一种方法是用 `数组` 存储子节点

```java
class TrieNode {
    // change this value to adapt to different cases
    public static final int N = 26;
    public TrieNode[] children = new TrieNode[N];
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: root.children[c - 'a']
 */
```



第二种方法是使用 `Hashmap` 来存储子节点

```java
class TrieNode {
    public Map<Character, TrieNode> children = new HashMap<>();
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: root.children.get(c)
 */
```



