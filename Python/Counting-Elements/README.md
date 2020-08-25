## Counting Elements

Given an integer array ```arr```, count how many elements ```x``` there are, such that ```x + 1``` is also in ```arr```.

If there are duplicates in ```arr```, count them seperately.

* Example 1:
```
Input: arr = [1,2,3]
Output: 2
Explanation: 1 and 2 are counted cause 2 and 3 are in arr.
```
* Example 2:
```
Input: arr = [1,1,3,3,5,5,7,7]
Output: 0
Explanation: No numbers are counted, cause there's no 2, 4, 6, or 8 in arr.
```
* Example 3:
```
Input: arr = [1,3,2,3,5,0]
Output: 3
Explanation: 0, 1 and 2 are counted cause 1, 2 and 3 are in arr.
```
* Example 4:
```
Input: arr = [1,1,2,2]
Output: 2
Explanation: Two 1s are counted cause 2 is in arr.
```
* Example 5:
```
Input: arr = [1,1,2]
Output: 2
Explanation: Both 1s are counted because 2 is in the array.
```
**Constraints**:

    1 <= arr.length <= 1000
    0 <= arr[i] <= 1000



```{python}
    def countElements(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
```
### Approach 1:

The simplest way of solving this problem is to loop through each integer, x, checking whether or not it should be counted. This requires checking whether or not x + 1 is in arr.

```
define function count_elements(arr):
    count = 0
    for each x in arr:
        if integer_in_array(arr, x + 1):
            count = count + 1
    return count
```

To implement the integer_in_array function in the above algorithm, we can use linear search. To do a linear search, we need to loop through each integer of arr. If we find the integer that we're looking for, then return true. If we get to the end of arr, then we know the integer is not there, and so should return false.

```{python}
define function integer_in_array(arr, target):
    for each x in arr:
        if target is equal to x:
            return true
    return false
```

#### Complexity Analysis

Let N be the length of the input array, arr.

* Time complexity : O(N<sup>2</sup>).

    We loop through each of the N integers x, checking whether or not x + 1 is also in arr. Checking whether or not x + 1 is in arr is done using linear search, which requires checking through all N integers in arr. Because we're doing N operations N times, we get a time complexity of O(N<sup>2</sup>).

* Space complexity : O(1).

    We are only using a constant number of single-value variables (e.g. count), giving us a space complexity of O(1).
    
### Approach 2:

The reason why the algorithm above was so inefficient is because we're performing N linear searches, each with a cost of O(N). When we have an algorithm that is performing many linear searches to check for item existence, we should instead be looking to change the way the data is stored so that the time complexity of doing each search is less.

Recall that looking up items in a HashSet has a cost of O(1). Creating a HashSet from an array of N items has a cost of O(N). We only need to create the HashSet once. After that, we can then replace all O(N) linear searches with O(1) HashSet lookups.

The algorithm below is incorrect since if there were duplicates in arr, then the count returned will be too low!
```
define function count_elements(arr):
    hash_set = a new HashSet
    add all integers of arr to hash_set
    count = 0
    for each x in hash_set:
        if hash_set contains x + 1:
            count = count + 1
    return count
```
Recall that a HashSet removes duplicates. Consider a case like arr = [1, 1, 2]. The HashSet will be {1, 2}. Therefore, the above code will loop over each integer in the HashSet, which is only one copy of 1. Yet arr had two copies of 1.

To fix it, we need to loop over arr, but do the existence checks using the HashSet.
```
define function count_elements(arr):
    hash_set = a new HashSet
    add all integers of arr to hash_set
    count = 0
    for each x in arr:
        if hash_set contains x + 1:
            count = count + 1
    return count
```

#### Complexity Analysis

Let N be the length of the input array, arr.

* Time complexity : O(N).

    Creating a HashSet from N integers takes O(N) time. We then need to loop over each of the N integers like before, except this time we check for x + 1 by seeing if it is in the HashSet; an O(1) operation. This gives us a total time complexity of O(N)+N⋅O(1)=O(N)+O(N)=O(N).

* Space complexity : O(N).

    The HashSet needs to store each unique integer from arr. In the worst case, all the integers in arr will be unique, meaning that the HashSet has a space complexity of O(N).

It's interesting to note that O(N) is an upper bound on the space complexity. If U is the number of unique integers in arr, then the space complexity could more accurately be represented as O(U).
