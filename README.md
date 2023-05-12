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
    #this while loop explains the behaviour of merge sort 
    sorted += left_half[i:] 
    sorted += right_half[j:]
    #adding the remaining values from either list in the case that one list is continuously smaller than the other (so the other list is continuously bigger, and we just add them)
    return sorted
    
   # Big - O - notation
  Mathematical notation describing the limiting behaviour of a function as its input/parameter/argument approaches infinity
   - other notations when analyzing complexity of an algorithm 
   - Big Omega
   - Big Theta
   - Big O (tells us worst case scenario performance of our algorithm)
  
  Reasons for big O:
    Algorithm proof
  - proves that algorithm A is better than algorithm B by using Big-O
    Measures performance, run-time, disk usage:
  - our algorithms are designed to solve problems; however, reaching the solutions must not be feasible due to time or disk-space constraints
     Mathematically formalizing our algorithms:
  - different hardware will output different runtimes; therefore, we needed a formal mathematical analysis

Common Big-O notations
- Constant complexity (big O of (1))
- Logarithmic complexity (big O of (log n))
- Linear Complexity (big O of (n))
- Linearithmic Complexity (big O of (n log n))
- Quadratic Complexity (big O of n^2))

MEANING OF ALL BIG O's:
    Big O of (1)
Constant Time algorithms: completes the execution in the same amount of time regardless of its input
Examples:
- accessing a data point in a list with a KNOWN index
- given two numbers, reporting the sum
    Big O of (log n):
Logarithmic Time Algorithm:
if N was the size of the input, the algorithm will take log(n) steps to solve the problem
Most cases will use a log with a base of 2 (NOT TEN)
When the input set is continuously divided by two, it is usually a logarithmic complexity algorithm
Examples:
- binary search
    Big O of (n):
 Linear Time Algorithm: The completion of the algorithm is directly proportional to the size of the input
 Examples:
 - Searching for an item in a list
 - Searching a queue
 - Adding two n-bit integers    
    Big O of (n log n):
Linearithmic Algorithm: The completion of the computation grows in a linear pattern with a rate of change of a logarithm
Examples:
- Heapsort
- Mergesort

    Big O of (n^2):
Quadratic Complex Algorithms: performance is directly proportional to the square of the size of the input data set
Examples:
- Multiple two-n-digit numbers
- bubble, insertion, selection sort

    Big O's of lists and tuples complexities:
- popping (just returning the last digit) is big O notation of 1
- popping, returning a specific digit is a big O notation of n
- appending a value is a big O complexity of 1
- length is complexity of 1
   # Recursion
Recursion: a method to solve computational problem by relying on smaller instances of a solution to a given problem
The logic is that if we have a base case that helps to solves the smaller instance, then the base case solution helps to solve the bigger version of the solution
Basically the function calls itself again and again until the base case is hit
- base case is the simplest solution for the simplest, smallest instance of the problem
    Direct: f only calls f
    Indirect: f calls g in which g calls f (can create longer chains)
        - indirect recustion can be also reffered to as 'mutual recursions'

  # Simplistic sorting algorithms 
 
    Bubble sort: each larger digit is pushed to the right (like bubbles)
    - A sorting algorithm that is based upon comparing pairs of values and swapping their places if necessary
    Overall ideas: 
    - Look at L[i] and if L[i-1], if they are not sorted, swap locations
    - Reap as you increase i and until no swap occurs
    
    Insertion Sort:
    - A sorting algorithm that iterates and sorts from the bottom one element at a time
    Overall ideas:
    - since a singleton list is already sorted, it will grow its 'sorted' list with the next value from the list
    - It grabs the next value, REMOVES IT, and places it in the correct location
    - It does this until the list is fully sorted
   
   def insertion_sort(arr):
   
    for i in range(1, len(arr)): #staring at second element
        # save the current element in a variable called "key"
        key = arr[i]
        
        # set a variable "j" to be the index of the element before the current element
        j = i - 1
        
        # loop backwards through the array, moving elements up by one position
        # until we find an element that is smaller than the key
        while j >= 0 and key < arr[j] #saying that while current is smaller than then the value previous which is not sorted:
            arr[j + 1] = arr[j] #here is where we swap 
            j -= 1 #i increases, j decreases here
        
        # insert the key in its correct sorted position
        arr[j + 1] = key
    
  
    return arr

   
    Selection Sort:
    - a sorting algorithm that uses two lists: sorted list and unsorted list. It brings the values to the sorted list in a sorted way
    Overall Idea:
    - at beginning, sorted list is empty and unsorted list is full
    - choosing the smaller (or largest) value from the unsorted list and append it to the sorted list
    - repeat until unsorted list is empty
  
    Stack and Queue:
    - All STACK and QUEUE operations are big O (1) with space complexity being big O (n)
    - Abstract data type; a mathematical model for data types. this is defined by its behaviour (semantics) from the point of view of a user, of the data, specificaly in terms of possible values, possible operations on data of this type, and behaviour of these operations
        LIFO (last in first out) --> STACK
    - container that holds multiple data
    METHODS:
    - push --> adds element
    - pop --> removes most recent element
    - peek --> looks at the most recent element
        Applications:
    - reverse word
    - 'undo' feature
    - backtracking
    - language processing
    - depth first search
        FIFO (first in first out) --> QUEUE
    - container holds multiple data (like stack)
    METHODS:
    - enqueue --> adds element
    - dequeue --> removes and returns the first/earliest added elementd
    - peek --> look at the first element
        Applications:
    - servering requests on a single shared resource (i/e printer, cpu tasks scheduling)
    - call center phone systems uses queues
    - breadth first search
    - handling of interrupts in real-time systems
    

  # inefficiency of recursive calls
  
 Example being the fibonacci function recusion problem. We have the program running its recursive call time after time because it needs all of the previous values to find the n'th fibonacci number which it calculates many times with each call. This becomes redunant and slows down efficiency. We can reduce the number of function calls and redundant computations by using memory
 
  # best, worst, average cases
  
  INSERTION SORT
best case: O(n)
- even though no swaps are done in the best case, we still need to compare
in the best case, the list is already sorted, and no swaps are needs. In this case, the insertion sort only needs to compare each element once to its predecessor (previous value) and move on to the next element
average case: O(n^2)
- average case being that insertion sort needs to compare and possibly swap each element with its predecessor multiple times to find its correct possition in the sortes list. This results in a quadratic time complexity that grwos witht he square of the input size 
worst case: O(n^2)
- being that the list is in reverse order. all elements need to be swapped 

SELECTION SORT
best case: O (n^2)
in the best case, selection sort needs to traverse the list only once to find the smallest element and swap it with the first element. However, if the list is already sorted, selection sort stilll needs to traverse the list to confirm that it is sorted, resulting in a quadratic time complexity
average case: O (n^2)
average case being that selection sort needs to traversethe list multiple times to find the smallest element and swap it with thenext unsorted element
worst case: O (n^2)
in the worst case, selection sort needs to traverse the list multiple timess to find the smallest element and swap it with the next unsorted element. If the list is sorted in reverse order, selection sort needs to make the maximum nuber of comparisons and swaps, leading to a quadratic complexity

BUBBLE SORT:
best case: O (n)
- best case being that the list is already sorted, no swaps needs. However, we must stil traverse through to confirm it is sorted meaning a complexity of n
average case: O (n^2)
- average case being that bubble sort needs to compare and possibly swap each element with its neighour multiple times to sort the list (because we only swap 2 elements at a time)
worst case: O (n^2)
- worst case is that the list is in reverse order, and the bubble sort needs to make the max number of comparisons and swaps

   
   
  



