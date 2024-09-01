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

## Experiment {8A}: - Take number of rows, columns and elements from user and display it in the form of matrix.

**Code:-**
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int rows, cols;

    // Input number of rows and columns
    cout << "Enter the number of rows: ";
    cin >> rows;
    cout << "Enter the number of columns: ";
    cin >> cols;

    // Create a 2D vector to store matrix elements
    vector<vector<int>> matrix(rows, vector<int>(cols));

    // Input matrix elements
    cout << "Enter the elements of the matrix:" << endl;
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << "Element [" << i << "][" << j << "]: ";
            cin >> matrix[i][j];
        }
    }

    // Display the matrix
    cout << "The matrix is:" << endl;
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}

**Output:-**

![image](https://github.com/user-attachments/assets/aef344dc-b7c7-4253-a62f-70fced44569c)


## Experiment {8B}: - Take two matrices from user and perform addition and multiplication.

**Code: -**
#include <iostream>
#include <vector>

using namespace std;

void inputMatrix(vector<vector<int>>& matrix, int rows, int cols) {
    cout << "Enter the elements of the matrix:" << endl;
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << "Element [" << i << "][" << j << "]: ";
            cin >> matrix[i][j];
        }
    }
}

void printMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int elem : row) {
            cout << elem << " ";
        }
        cout << endl;
    }
}

vector<vector<int>> addMatrices(const vector<vector<int>>& mat1, const vector<vector<int>>& mat2) {
    int rows = mat1.size();
    int cols = mat1[0].size();
    vector<vector<int>> result(rows, vector<int>(cols));
    
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            result[i][j] = mat1[i][j] + mat2[i][j];
        }
    }
    return result;
}

vector<vector<int>> multiplyMatrices(const vector<vector<int>>& mat1, const vector<vector<int>>& mat2) {
    int rows1 = mat1.size();
    int cols1 = mat1[0].size();
    int rows2 = mat2.size();
    int cols2 = mat2[0].size();
    
    // Check if multiplication is possible
    if (cols1 != rows2) {
        throw invalid_argument("Matrix dimensions do not match for multiplication.");
    }
    
    vector<vector<int>> result(rows1, vector<int>(cols2, 0));
    
    for (int i = 0; i < rows1; ++i) {
        for (int j = 0; j < cols2; ++j) {
            for (int k = 0; k < cols1; ++k) {
                result[i][j] += mat1[i][k] * mat2[k][j];
            }
        }
    }
    return result;
}

int main() {
    int rows1, cols1, rows2, cols2;

    // Input dimensions for the first matrix
    cout << "Enter the number of rows and columns for the first matrix: ";
    cin >> rows1 >> cols1;
    vector<vector<int>> matrix1(rows1, vector<int>(cols1));

    // Input the first matrix
    cout << "Input the first matrix:" << endl;
    inputMatrix(matrix1, rows1, cols1);

    // Input dimensions for the second matrix
    cout << "Enter the number of rows and columns for the second matrix: ";
    cin >> rows2 >> cols2;
    vector<vector<int>> matrix2(rows2, vector<int>(cols2));

    // Input the second matrix
    cout << "Input the second matrix:" << endl;
    inputMatrix(matrix2, rows2, cols2);

    // Matrix Addition
    if (rows1 == rows2 && cols1 == cols2) {
        cout << "Matrix Addition Result:" << endl;
        vector<vector<int>> additionResult = addMatrices(matrix1, matrix2);
        printMatrix(additionResult);
    } else {
        cout << "Matrix Addition is not possible with these dimensions." << endl;
    }

    // Matrix Multiplication
    try {
        if (cols1 == rows2) {
            cout << "Matrix Multiplication Result:" << endl;
            vector<vector<int>> multiplicationResult = multiplyMatrices(matrix1, matrix2);
            printMatrix(multiplicationResult);
        } else {
            cout << "Matrix Multiplication is not possible with these dimensions." << endl;
        }
    } catch (const invalid_argument& e) {
        cout << e.what() << endl;
    }

    return 0;
}

**Output: -**
![image](https://github.com/user-attachments/assets/6e5efaa4-ad18-42bf-859d-74e30dbdc76c)

## Experiment {8C}: - Take matrix elements from user and perform addition of diagonal elements

**Code:-**
#include <iostream>
#include <vector>

using namespace std;

// Function to input matrix elements from the user
void inputMatrix(vector<vector<int>>& matrix, int rows, int cols) {
    cout << "Enter the elements of the matrix:" << endl;
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << "Element [" << i << "][" << j << "]: ";
            cin >> matrix[i][j];
        }
    }
}

// Function to print the matrix
void printMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int elem : row) {
            cout << elem << " ";
        }
        cout << endl;
    }
}

// Function to calculate the sum of primary and secondary diagonal elements
pair<int, int> sumDiagonals(const vector<vector<int>>& matrix, int rows, int cols) {
    int primaryDiagonalSum = 0;
    int secondaryDiagonalSum = 0;

    // Sum for primary diagonal
    for (int i = 0; i < rows; ++i) {
        if (i < cols) {
            primaryDiagonalSum += matrix[i][i];
        }
    }

    // Sum for secondary diagonal
    for (int i = 0; i < rows; ++i) {
        if (i < cols) {
            secondaryDiagonalSum += matrix[i][cols - i - 1];
        }
    }

    return {primaryDiagonalSum, secondaryDiagonalSum};
}

int main() {
    int rows, cols;

    // Input matrix dimensions
    cout << "Enter the number of rows and columns for the matrix: ";
    cin >> rows >> cols;

    // Create a matrix
    vector<vector<int>> matrix(rows, vector<int>(cols));

    // Input matrix elements
    inputMatrix(matrix, rows, cols);

    // Print the matrix
    cout << "The matrix is:" << endl;
    printMatrix(matrix);

    // Calculate diagonal sums
    auto [primarySum, secondarySum] = sumDiagonals(matrix, rows, cols);

    // Output diagonal sums
    cout << "Sum of primary diagonal elements: " << primarySum << endl;
    cout << "Sum of secondary diagonal elements: " << secondarySum << endl;

    return 0;
}

**Output:-**
![image](https://github.com/user-attachments/assets/cf683f6c-cc7a-46c0-af76-20d7337b890e)


## Experiment {8D}: - Take matrix elements from user and perform transpose operation on the matrix.

**Code:-**
#include <iostream>
#include <vector>

using namespace std;

// Function to input matrix elements from the user
void inputMatrix(vector<vector<int>>& matrix, int rows, int cols) {
    cout << "Enter the elements of the matrix:" << endl;
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            cout << "Element [" << i << "][" << j << "]: ";
            cin >> matrix[i][j];
        }
    }
}

// Function to print the matrix
void printMatrix(const vector<vector<int>>& matrix) {
    for (const auto& row : matrix) {
        for (int elem : row) {
            cout << elem << " ";
        }
        cout << endl;
    }
}

// Function to transpose the matrix
vector<vector<int>> transposeMatrix(const vector<vector<int>>& matrix, int rows, int cols) {
    vector<vector<int>> transposed(cols, vector<int>(rows)); // Create a transposed matrix

    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            transposed[j][i] = matrix[i][j];
        }
    }
    return transposed;
}

int main() {
    int rows, cols;

    // Input matrix dimensions
    cout << "Enter the number of rows and columns for the matrix: ";
    cin >> rows >> cols;

    // Create a matrix
    vector<vector<int>> matrix(rows, vector<int>(cols));

    // Input matrix elements
    inputMatrix(matrix, rows, cols);

    // Print the original matrix
    cout << "The original matrix is:" << endl;
    printMatrix(matrix);

    // Perform transpose
    vector<vector<int>> transposedMatrix = transposeMatrix(matrix, rows, cols);

    // Print the transposed matrix
    cout << "The transposed matrix is:" << endl;
    printMatrix(transposedMatrix);

    return 0;
}

**Outcome:-**
![image](https://github.com/user-attachments/assets/185cb065-3e8d-42c3-b732-f8d79d882029)


## Conclusion

We learned how to perform matric operation in C++.








