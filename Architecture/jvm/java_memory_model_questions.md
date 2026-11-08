1. What is operand stack?
2. What does metaspace have?
3. Why is `LongAdder` preferred over `AtomicLong`?
4. How does `Collections.synchronizedList` work?
5. What is `CopyOnWriteArrayList`?
6. How does `ConcurrentHashMap` work?
7. How is distributed invalidation implemented?
8. How is event-driven invalidation implemented?
9. What is `AtomicReference`?

```java
enum State {
  CLOSED,
  OPEN
}

AtomicReference<State> state = new AtomicReference<>();

state.compareAndSet(
  State.CLOSED,
  State.OPEN
};
```

10. What is `AtomicStampedReference`?
	1. Solves the A->B->A problem
		1. Associates a version/stamp with a reference

11. What is `AtomicMarkableReference`?
12. Why is double-checked locking used?

