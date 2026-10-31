# Join Strategies in PySpark: Broadcast Hash Join vs. Sort-Merge Join

## 1. Overview of Join Implementations in Spark

Selecting the appropriate join strategy is a critical performance differentiator in data engineering interviews.

```
                          [ Join Evaluation ]
                                   |
                   Is one table smaller than threshold?
                                (<= 10 MB)
                               /          \
                             YES           NO
                             /              \
             [ Broadcast Hash Join ]    Are join keys sortable?
                                        /                   \
                                      YES                    NO
                                      /                       \
                            [ Sort-Merge Join ]       [ Shuffle Hash Join ]
```

---

## 2. Broadcast Hash Join (BHJ) / Map-Side Join

### Mechanism:
1. The Driver collects the smaller DataFrame into memory.
2. The Driver broadcasts the entire small DataFrame to all executor nodes via efficient BitTorrent-like peer-to-peer protocols.
3. Ea