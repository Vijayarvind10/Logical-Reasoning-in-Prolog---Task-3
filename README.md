### 1. **Initializing Prolog**

```python

from pyswip import Prolog
prolog = Prolog()

```

The script starts by importing the `Prolog` class from the `pyswip` library and initializing an instance of `Prolog`, allowing us to add facts, rules, and queries directly in Python.

### 2. **Defining the Knowledge Base**

The script then adds facts about different animals, such as the type of animal, number of legs, habitat, and biological traits like fur, egg-laying, and warm-blooded status.

### Examples of Facts

```python

prolog.assertz("animal(elephant)")
prolog.assertz("has_legs(elephant, 4)")
prolog.assertz("lives_in(elephant, land)")
prolog.assertz("has_fur(elephant)")
prolog.assertz("is_warm_blooded(elephant)")

```

In this part:

- `prolog.assertz("animal(elephant)")` adds the fact that an elephant is an animal.
- `has_legs(elephant, 4)` asserts that elephants have four legs.
- `lives_in(elephant, land)` specifies that elephants live on land.
- Similar facts are asserted for other animals (e.g., `tiger`, `crocodile`, `shark`, `sparrow`).

### Adding the Mammal Rule

```python

prolog.assertz("mammal(X) :- has_fur(X), is_warm_blooded(X), \\+ lays_eggs(X)")

```

This rule defines a **mammal** as any animal (`X`) that:

1. Has fur,
2. Is warm-blooded, and
3. Does not lay eggs.

The `\\+` symbol is Prolog’s "not" operator, ensuring that the mammal rule only applies to animals that do not lay eggs.

### 3. **Querying the Knowledge Base**

The script includes a series of queries to retrieve information from the knowledge base. It runs these queries to test if the facts and rules are correctly set up.

### Example Queries

- **Find Mammals**:
    
    ```python
    
    for solution in prolog.query("mammal(X)"):
        print(solution["X"])
    
    ```
    
    This query retrieves all animals that satisfy the mammal rule, printing each mammal in the knowledge base.
    
- **Animals That Live in Water**:
    
    ```python
    
    for solution in prolog.query("lives_in(X, water)"):
        print(solution["X"])
    
    ```
    
    This query finds all animals that have `water` as their habitat.
    
- **Animals with 4 Legs**:
    
    ```python
    
    for solution in prolog.query("has_legs(X, 4)"):
        print(solution["X"])
    
    ```
    
    This query checks for animals that have 4 legs.
    
- **Warm-Blooded Animals Check**:
    
    ```python
    
    for animal in ["elephant", "shark", "sparrow"]:
        result = list(prolog.query(f"is_warm_blooded({animal})"))
        print(f"{animal.capitalize()} is warm-blooded: {bool(result)}")
    
    ```
    
    This part checks if specific animals are warm-blooded. The query is run separately for each animal (`elephant`, `shark`, and `sparrow`), and the result is displayed as `True` or `False`.
    

### 4. **Expected Output**

The queries should yield results based on the facts and rules set in the knowledge base:

- **Mammals**: Animals meeting the mammal criteria (e.g., `elephant`, `tiger`).
- **Water-Dwelling Animals**: Animals that live in water (e.g., `crocodile`, `shark`, `dolphin`, `penguin`).
- **Animals with 4 Legs**: Animals that have 4 legs (e.g., `elephant`, `tiger`, `crocodile`).
- **Warm-Blooded Check**: Verifies warm-blooded status for specific animals.

### Summary

This setup demonstrates how to define facts and rules in Prolog using `pyswip` and retrieve information by running logical queries, making it possible to work with Prolog directly in Python.
