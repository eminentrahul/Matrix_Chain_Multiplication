# Matrix_Chain_Multiplication

Matrix chain multiplication using dynamic programming
What is matrix multiplication?
Todays problem is not about actually multiplying matrices, but to find out an order in which
we multiply matrices so that number of multiplication done are minimum.

There are two basic properties of a matrix : number of rows and number of columns in matrix. Row and columns are called as dimensions of matrix.
Given N matrices of (MxN dimensions). Find an order in which these matrices are multiplied, so that total number of scalar multiplications are least.
and dimensions of each matrix given in an array P where P[i-1] and P[i] denote rows and column respectively of ith matrix. 
Matrix chain multiplication is a typical problem which is used to explain dynamic programming. Approach learnt here can be easily applied to many other problems.

Before going further, lets understand some points about matrix multiplication
1. Matrix multiplication is associative i.e.  A* (B*C) = (A*B) *C
2. It is not commutative i.e  A * (B*C) not equal to A * (C * B)
3. To multiply two matrices, they should be compatible i.e. no of columns in first matrix should be equal to number of rows of second matrix.
No of columns of first matrix = No. of rows of second matrix

Let’s get back to problem at hand.  Look at this problem as this : Figure out a way to put parenthesis around matrices so that total number of multiplication are least.
Brute force way is to find out every possible combination of parenthesis and check which one is minimum. 
This is approach can be implemented in recursive way, once we put a parenthesis, problem is reduced putting parenthesis
around N-1 matrices to be multiplied. However, code will be exponential in time and hence of no use for every large input.
Let’s see if dynamic programming fits in. We can see that cost of multiplying matrices Ai to Aj  is cost of

Cost (Ai, Aj) = Cost(Ai,Ak) + Cost(Ak+1,Aj )+(P[i-1] * P[k] * P[j])

Idea is to find out K such that cost(Ai, Aj) becomes minimum. If M[i,j] represents the cost to multiply matrix i to matrix j, then,
M[i,j]  = M[i,k] + M[K+1,j] + ((P[i-1] * P[k] * P[j])
When calculating M[i,j]; M[i,k] and M[k+1,j] should be already available. Also, M[i,i] = 0 as cost of multiplying a single matrix will be 0.

Looking at the requirement to calculate M[i,j], it depends on length of chain.
Length of chain from matrix i to matrix j would be i+j-1. We start with length L = 2 and go on to solve the table entry for length N. M[1, N] will give us the final cost. 

We will start with L =2, chain we are considering is of length of 2 as j =  i + L -1  = 1 +2 -1 =2.  We will start with i =1 and loop runs to i = N-L +1 and considering two matrices at time.

Length being considered will vary for L =2 to L = N. Based on L, j will also change and we will be finding minimum cost(i,j) for each i and j. To find minimum cost(i,j), we need to find a K such that expression

Cost (Ai, Aj) = Cost(Ai,Ak) + Cost(Ak+1,Aj )+(P[i-1] * P[k] * P[j])
becomes minimum. This is top down filling of table where M [1, 2] will be filled first and then going up to fill till M [1,N].
