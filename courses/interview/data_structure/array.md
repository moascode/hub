# Array

- Ordered data structure by insertion
- In Java, arrays are static, it has fixed size
- Last element of the array is always n-1
- Insertion from an array at any given position i
  - Shift starting from end to i
  - insert at i

  ```java
    // Insert n into index i after shifting elements to the right.
    // Assuming i is a valid index and arr is not full.
    public void insertMiddle(int[] arr, int i, int n, int length) {
        // Shift starting from the end to i.
        for (int index = length - 1; index > i - 1; index--) { //index >= i
            arr[index + 1] = arr[index]; //copy n-1 to n position
        }
        // Insert at i
        arr[i] = n;
    }
  ```

- Deletion from an array at any given position i
  - Shift starting from i + 1 to end
  - set n-1 to 0
  
  ```java
    // Remove value at index i before shifting elements to the left.
    // Assuming i is a valid index.
    public void removeMiddle(int[] arr, int i, int length) {
        // Shift starting from i + 1 to end.
        for (int index = i + 1; index < length; index++) {
            arr[index - 1] = arr[index]; //copy i to i+1
        }
        // No need to 'remove' arr[i], since we already shifted
        arr[length-1] = 0
    }
    //int[] arr = {2,3,4,5};
    //removeMiddle(arr, 2, 4);
    //2 3 5 0 
  ```

## Time Complexity

- Reading: O(1)
- Insertion: O(n), If inserting at the end of the array O(1)
- Deletion: O(n), If deleting at the end of the array O(1)
