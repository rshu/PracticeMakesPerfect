



#### Iterate map.keySet()



```java
for (Map.Entry<Character, Integer> entry : map.entrySet()) {
    char key = entry.getKey();
    int value = entry.getValue();
}
```



### TreeMap



#### public K floorKey(K key)

Return the ***greatest key*** less than or equal to giv en key from the parameter.

```java

```

-----



#### public Map.Entry<K, V> floorEntry(K key)

Return the ***key-value mapping*** associated with the greatest key less than or equal to the given key, or null if there is no such key

```java

```

-----



#### public Map.Entry<K, V> lastEntry()

Return a ***key-value mapping*** associated with the greatest key in this map, or null if the map is empty.

```java

```

-----



#### LinkedHashMap

keep the order of insert and traverse

#### ConcurrentHashMap





```java
# get the first entry
Map.Entry<Integer,List<String>> entry = map.entrySet().iterator().next();
Integer key = entry.getKey();
List<String> value = entry.getValue();
```

