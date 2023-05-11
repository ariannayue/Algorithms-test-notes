# Algorithms-test-notes
# Linear Search (sequential search)
way to find items in a list. goes through each value in the list and returning the index of when that value is found
- Complexity of Lineary Search --> big O of (n) 
- At worst, the last object will be the target or the target won't exist
- Best performance : big O(1) # first item
- Average Performance : O(n/2) #somewhere in the middle of the set, still linear complexity
- Wost case : big O(n)

# Binary Search
A searching algoritm that is designed to search from a sorted list
Idea:
- compares the target with the middle most value
- If not found, it eliminates the half where the target cannot exist
Cons:
- database must be comparable and sortable
Algorithm:
let A be array, n be the length of A, T be the target
1. set left = 0 (first value) and right = n-1 (last value)
2. while left <= Right
3. set middle to the floor of (left + right) / 2
4. if A[middle] < T, set Left = middle + 1 (the very left most value because our number is to the right of our previous middle) and go to step 2 
5. if A[middle] > T, set Right = middle - 1 and go to step 2 # meaning that our number was left
6. if A [middle] == T, return Middle as search is done 
Complexity: Big O Notation --> O(log n)

# Merge Sort
A comparison-based algorithm that sorts a given dataset. It is classified as a 'divide and conquer' algorithm
1. Top-down implementation
2. Bottom-up Implementation

Complexity of merge sort: O(n log n) 
Concept:
- dividing the unsorted list into n sublists, each containing 1 element (a list of 1 element is considered sorted)
- repeatedly merging sublists to produce new sorted sublists until there is only 1 sublist remaining (which would be our sorted list)


def merge_sort(arr):
    if len(arr) <= 1: #is said to be sorted if the length of the list is 1 or less
        return arr
    
    mid = len(arr) // 2
    left_half = arr[:mid]
    right_half = arr[mid:]

    left_half = merge_sort(left_half) #our recursive call
    right_half = merge_sort(right_half) #our recursive call

    return merge(left_half, right_half) #our second function


def merge(left_half, right_half):
    sorted = []
    i = 0
    j = 0
    
    while i < len(left_half) and j < len(right_half):
        if left_half[i] < right_half[j]:#comparing index by index of each list and adding the smaller one to the sorted list 
            sorted.append(left_half[i])
            i += 1
        else:
            sorted.append(right_half[j])
            j += 1
    
    sorted += left_half[i:] 
    sorted += right_half[j:]
    #adding the remaining values from either list in the case that one list is continuously smaller than the other (so the other list is continuously bigger, and we just add them)
    return sorted


