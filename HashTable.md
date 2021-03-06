# Step-by-step Implementation of (basic) Hash Table

## 1. Define HashNode

A HashNode holds a single key-value pair. A constructor is used to initialize key and value.

``` java
// HashNode.java

public class HashNode {
    int key; // It is not necessary that key and value
    int value; // must be integers.

    HashNode(int k, int v) {
        key = k;
        value = v;
    }
}
```

## 2. Define a Hash Table

A HashTable contains an array of HashNode. The size of the the array is initialized to a large enough value and is usually a prime number.

``` java
// HashNode.java  -- remains same as above
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
    }
}
```

## 3. Define a hash function

The purpose of hash function is to take the key as a parameter, apply some computation and return a number within the range 0 ... SIZE-1. The function should be good enough to return indices that uniformly distribute over the range 0 and SIZE-1. Essentially, the goal is to minimize collisions.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) {
        return (x*x*x + 3*x*x + 1) % SIZE;
    }
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
    }
}
```

## 4. Implement put method

The put method inserts a <key,value> pair to the hash table.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) { ... }
    
    // Add a key-value pair to the hash table
    public void put(int k, int v) {
        int index = hash(k);
        HashNode hn = new HashNode(k,v);
        harr[index] = hn;
    }    
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
        
        h.put(10, 100);
        h.put(8, 64);
        h.put(6, 36);
    }
}
```

## 5. Implement get method

The put method inserts a <key,value> pair to the hash table.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) { ... }
    public void put(int k, int v) { ... }
    
    // Retrieve a value from hashtable based on a key
    public int get(int k) {
        HashNode n = harr[hash(k)];
        if ( n == null)  // k is not present
            return Integer.MAX_VALUE;
        else
            return n.value;
    }    
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
        
        h.put(10, 100);
        h.put(8, 64);
        h.put(6, 36);
        
        System.out.println( h.get(10) );  // prints 100
        System.out.println( h.get(50) );  // prints invalid value -2147483648
    }
}
```

## 6. Implement contains method

The contains method checks if an entry with key k is present in the hash table. If so, it returns true. Otherwise false.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) { ... }
    public void put(int k, int v) { ... }
    public int get(int k) { ... }
    
    // Check if the hashtable contains key k
    public boolean contains(int k) {
        if ( harr[hash(k)] != null )
            return true;
        else
            return false;
    }
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
        
        h.put(10, 100);
        h.put(8, 64);
        h.put(6, 36);
        
        if ( h.contains(10) )
            System.out.println( h.get(10) );   // prints 100
        if ( h.contains(50) )
            System.out.println( h.get(50) );  // Statement not reached
    }
}
```

## 7. Implement remove method

Given a key k, the remove method deletes the corresponding entry from the hash table.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) { ... }
    public void put(int k, int v) { ... }
    public int get(int k) { ... }
    public boolean contains(int k) { ... }
    
    // Remove a key-value pair from hashtable given a key
    public void remove(int k) {
        int index = hash(k);
        harr[index] = null;
    }
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
        
        h.put(10, 100);
        h.put(8, 64);
        h.put(6, 36);
        
        if ( h.contains(10) )
            System.out.println( h.get(10) );   // prints 100
        if ( h.contains(50) )
            System.out.println( h.get(50) );  // Statement not reached
            
        h.remove(6);
    }
}
```

## 8. Implement print method

The print method prints the <key, value> pairs in the hash table. It scans through the harr from 0 and SIZE-1 and if the entry is not null, it prints the key and value of the entry.

``` java
// HashNode.java  -- remains same
```

``` java
// HashTable.java

public class HashTable {
    int SIZE = 997;   // typically a large enough prime number
    HashNode[] harr = new HashNode[SIZE];
    
    public int hash(int x) { ... }
    public void put(int k, int v) { ... }
    public int get(int k) { ... }
    public boolean contains(int k) { ... }
    public void remove(int k) { ... }
    
    // Print the entries in the hashtable
    public void print() {
        for (int i=0; i<harr.length; i++) {
            if ( harr[i] != null )
                System.out.println(harr[i].key 
                        + " : " + harr[i].value 
                        + " stored at index " + hash(harr[i].key));
        }
}
```

``` java
// HashDriver.java

public class HashDriver {
    public static void main(String[] args) {
        HashTable h = new HashTable();
        System.out.println(h.hash(101));  // prints 97
        System.out.println(h.hash(102));  // prints 706
        System.out.println(h.hash(103));  // prints 936
        
        h.put(10, 100);
        h.put(8, 64);
        h.put(6, 36);
        
        if ( h.contains(10) )
            System.out.println( h.get(10) );   // prints 100
        if ( h.contains(50) )
            System.out.println( h.get(50) );  // Statement not reached
        
        h.print();  // prints 3 entries (10, 100) (8, 64) and (6, 36) in arbitrary order
        h.remove(6);
        h.print();  // prints 3 entries (10, 100) (8, 64) in arbitrary order
    }
}
```

