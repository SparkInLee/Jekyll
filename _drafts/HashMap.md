# HashMap
**Description:** some ideas in reading source of HashMap

1. **Round up to the next highest power of 2** [Reference](http://graphics.stanford.edu/~seander/bithacks.html#RoundUpPowerOf2Float)

```java
	v—;     //asume that the highest set bit is n
	v |= v >> 1;     //set n-1
	v |= v >> 2;     //set [n-3,n-2]
	v |= v >> 4;     //set [n-7,n-4]
	v |= v >> 8;     //set [n-15,n-8]
	v |= v >> 16;     //set [n-16,n-31]
	v++;     //make it power of 2^n+1
```

2. **EnsureCapacity**  
   `(result & ~(capacity-1))==0`
which equals:
   `(result>=0 && result < capacity);`
