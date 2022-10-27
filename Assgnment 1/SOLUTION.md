# Benchmarking Randomized Quicksort

## Implementation of Randomized Quicksort that returns the average of comparisons out of 100 runs on the same input of 100 numbers.

```
import random

""" Implementation of Randomized Quicksort """

comparisons = 0


def quicksort(arr, l, r):
    global comparisons
    if l < r:
        p = random.randint(l, r)
        pivot_element = arr[p]
        s1 = []
        s2 = []
        for i in range(l, r + 1):
            comparisons += 1
            if arr[i] < arr[p]:
                s1.append(arr[i])
            if arr[i] > arr[p]:
                s2.append(arr[i])
        arr = quicksort(s1, 0, len(s1) - 1) + \
            [pivot_element] + quicksort(s2, 0, len(s2) - 1)
        return arr
    return [arr[0]] if len(arr) else []


if __name__ == '__main__':

    # Generating a list containing numbers from 1 to 100
    arr = [i + 1 for i in range(100)]

    # Randomly Shuffling the List
    random.shuffle(arr)

    expected_comparison = 0
    for i in range(len(arr) - 1):
        for j in range(i + 1, len(arr)):
            expected_comparison += (2)/(j - i + 1)
    print(
        f"Theoretical Prediction of Expected Number of Comparison E[X]: {expected_comparison}")
    comparisons_list = []
    for _ in range(100):
        comparisons = 0
        quicksort(arr, 0, len(arr) - 1)
        comparisons_list.append(comparisons)
    print(
        f"Average Comparison From Experiment E[X̅]: {sum(comparisons_list) / 100}")
```

## Output

```
Theoretical Prediction of Expected Number ofComparison E[X]: 647.8502585632009
Average Comparison From Experiment E[X̅]: 696.9
```

## Comparison With Theoretical Prediction

From the code output, it looks like the average number of comparisons in Randomized Quicksort implementation is a bit higher than our theoretical prediction.
