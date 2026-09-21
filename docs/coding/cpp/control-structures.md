---
title: Control Structures: Question Bank
---

# Control Structures: Question Bank

## Questions bank:

Find the error in the code below it can be logical or syntax:

```cpp
int main()
{ int n1, n2, n3;
cout << "Enter three integers: ";
cin >> n1 >> n2 >> n3;
if (n1 >= n2 >= n3) cout << "true";
}

//Input
Enter an integer: 0 0 1
```

## Practice Questions

??? question "1. What is the error in `if (n1 >= n2 >= n3)`?"

    A logical error. C++ doesn't chain comparisons: `n1 >= n2` is evaluated first and gives 0 or 1, and that result is then compared with `n3`. With input 0 0 1, `0 >= 0` is 1, and `1 >= 1` is true, so it prints true even though the numbers are not in descending order.

??? question "2. How do you fix it?"

    Compare each pair separately: `if (n1 >= n2 && n2 >= n3)`.
