Java.lang.Math.ceil(double a)

#### public static double ceil(double a)

Return the smallest(closest to negative infinity) double valut that is greater than or equal to the argument and is equal to a mathematical integer.

e.g.,

```java
Math.ceil(125.9) // 126.0
Math.ceil(0.4873) // 1.0
```



##### check if is Prime Number

```java
private boolean isPrime(int n) {
        if (n <= 1)
            return false;
        
        if (n <= 3)
            return true;
        
        if (n % 2 == 0 || n % 3 == 0)
            return false;
        
        for (int i = 5; i * i <= n; i = i + 6) {
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
        }
        
        return true;
    }
```

