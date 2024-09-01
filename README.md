# Experiment-8
## Theory: -
### 2D Arrays (Matrices) in C++: Theory

A 2D array, often referred to as a matrix, is a collection of elements arranged in rows and columns. In C++, a 2D array is essentially an array of arrays. Here's a detailed breakdown of 2D arrays in C++:

#### Definition and Declaration

1. **Definition:**
   A 2D array is defined as an array where each element is itself an array. This allows you to store data in a tabular format.

2. **Declaration:**
   You declare a 2D array by specifying the type of its elements, followed by the array name and the dimensions. For example:
   ```cpp
   type arrayName[rows][columns];
   ```
   - `type` specifies the data type of the elements (e.g., `int`, `float`, `char`).
   - `rows` specifies the number of rows.
   - `columns` specifies the number of columns.

   **Example:**
   ```cpp
   int matrix[3][4]; // A 2D array with 3 rows and 4 columns
   ```

#### Initialization

1. **Static Initialization:**
   You can initialize a 2D array at the time of declaration:
   ```cpp
   int matrix[3][4] = {
       {1, 2, 3, 4},
       {5, 6, 7, 8},
       {9, 10, 11, 12}
   };
   ```

2. **Partial Initialization:**
   If you provide fewer elements than the size of the array, the remaining elements are initialized to zero:
   ```cpp
   int matrix[2][3] = {
       {1, 2},    // Last element is initialized to 0
       {4}        // The remaining elements are initialized to 0
   };
   ```

#### Accessing Elements

- **Syntax:**
  To access an element in a 2D array, you use the row and column indices:
  ```cpp
  matrix[rowIndex][columnIndex];
  ```
  **Example:**
  ```cpp
  int value = matrix[1][2]; // Accesses the element in the 2nd row, 3rd column
  ```

#### Iterating Through a 2D Array

- **Using Nested Loops:**
  To process each element, you typically use nested `for` loops:
  ```cpp
  for (int i = 0; i < rows; ++i) {
      for (int j = 0; j < columns; ++j) {
          std::cout << matrix[i][j] << " ";
      }
      std::cout << std::endl;
  }
  ```


### Key Points

1. **Memory Layout:**
   - In memory, a 2D array is stored as a contiguous block of memory. Elements are stored in row-major order, meaning that the elements of each row are stored next to each other.

2. **Dynamic Allocation:**
   - If the size of the matrix is not known at compile time, you can use dynamic memory allocation with pointers and the `new` keyword. For instance:
     ```cpp
     int** matrix;
     int rows = 3, columns = 3;
     matrix = new int*[rows];
     for (int i = 0; i < rows; ++i) {
         matrix[i] = new int[columns];
     }
     // Remember to free the allocated memory using delete
     ```

3. **Limitations:**
   - The size of a static 2D array must be known at compile time. Dynamic allocation provides flexibility but requires manual memory management.

By understanding these concepts, you can effectively work with 2D arrays in C++, allowing you to handle matrix-like data structures for various applications.



