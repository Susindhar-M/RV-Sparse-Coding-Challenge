# RV-Sparse-Coding-Challenge
## Objective
To Implement the `sparse_multiply` function that:
- Scans a row-major matrix A and identifies its non-zero elements
- Extracts them into Compressed Sparse Row (CSR) format using caller-provided buffers
- Computes the matrix-vector product `y = A * x` using the extracted CSR data
- Writes the result directly into a caller-provided output buffer

## What does sparse_multiply do?
It performs matrix-vector multiplication using only the non-zero elements of the matrix, saving time and memory compared to a naive dense approach.

## What is CSR format?
CSR (Compressed Sparse Row) is a format used to store a sparse matrix optimally by only storing its non-zero elements. It uses three arrays:
- `values` - the non-zero elements in row-major order
- `col_indices` - the column index of each non-zero element
- `row_ptrs` - stores where each row starts in the values array (size = rows + 1)

## How the implementation works
1. Scans the matrix row by row
2. For each non-zero element found, appends its value and column index to `values` and `col_indices`
3. Before scanning each row, records the current non-zero count in `row_ptrs`
4. After all rows, appends the total non-zero count as the final `row_ptrs` sentinel
5. Computes `y[i]` for each row by summing `values[k] * x[col_indices[k]]` over that row's non-zeros

## How to compile and run
```bash
gcc -lm -o run challenge.c
./run
```

## Results
100/100 test iterations passed with zero numerical error.
