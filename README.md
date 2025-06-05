Implements a general-purpose backward chaining inference system for First-Order Logic (FOL). It supports variable-based reasoning, recursive rule application, and unification.

---
Task 7/
    -fol_bc.py        # Main inference engine
    -fol_test.py      # Main script for loading facts/rules and running queries
    -README.md

---

## 🧾 Example Knowledge Base (`fol_test.py`)

```python
kb.add_fact("Parent(John, Mary)")
kb.add_fact("Parent(Mary, Sam)")
kb.add_fact("Female(Mary)")

kb.add_rule("Grandparent(X, Z)", ["Parent(X, Y)", "Parent(Y, Z)"])
kb.add_rule("Grandmother(X, Z)", ["Grandparent(X, Z)", "Female(X)"])
```

---

## ✅ Example Queries & Expected Output

### Query 1: `Grandmother(John, Sam)`
```python
Query: Grandmother(John, Sam)
```

**Expected Output:**
```
Query: Grandmother(John, Sam)
No.
```

**Why?**
- `John` is a grandparent of `Sam` ✔
- But `John` is not female X → rule fails.

---

### Query 2: `Grandmother(Mary, Sam)`
```python
Query: Grandmother(Mary, Sam)
```

**Expected Output:**
```
Query: Grandmother(Mary, Sam)
Yes: Grandmother(Mary, Sam)
```

**Why?**
- `Mary` is a parent of `Sam` - Correct
- `John` is a parent of `Mary` - Correct → so `Mary` is a grandparent of `Sam` - Correct
- `Mary` is female - Correct → passes the `Grandmother` rule.

---

## Note

To reproduce working examples:
- Use the fact/rule setup above.
- Run the query `Grandmother(Mary, Sam)` to see successful inference.
- Try `Grandmother(John, Sam)` to confirm failure handling.
