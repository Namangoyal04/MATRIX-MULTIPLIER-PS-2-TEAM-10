MATRIX MULTIPLICATION ACCELERATOR:-

This project implements an efficient matrix multiplication accelerator for binary matrices with 4-bit values as inputs. The design is implemented using Verilog HDL         and operates with a gate-level description. The accelerator can process two input matrices of maximum size 3x3, with a total maximum of 18 inputs, each being 4             bits.

PROJECT SPECIFICATION :-

 1. Input Data Handling: The accelerator takes inputs in a serial manner taking one input at each positive clockedge over a
     maximum of 18 clock cycles, as first for Matrix A and then for matrix B ,so this way maximum 18 inputs will be stored in 
     a registers .
      
 2. Output Data Handling: It produces outputs in a serialized fashion, providing one output at a time,hence producing maximum
     of 9 outputs each at positive clock edge.
    
 3. Efficiency: The primary objective is to design a matrix multiplication accelerator that minimizes the number of clock
     cycles required to compute the results efficiently.  
     
 4. Scalability: The solution is scalable and adaptable to different matrix sizes while ensuring accurate computation of
     the product, i.e. total 27 such multiplications can be done of form mXn nXp where m,n,p belongs to integer from 1 to 3.


STRUCTURE & FRAMEWORK:-

   -Overview 
   
   The matrix multiplication accelerator is designed using a modular approach, dividing the task into smaller modules. This makes the design easier to understand the           structure that how step by step we progress to make our final module and how we implemented those small modules in final  MatrixMultiplir module and also  
   facilitates testing. Now, understanding The design that can be broken down into the following key modules:

KEY MODULES:-

1. Full Adder and Multiplier Modules:
   
   1. Full Adder: A basic building block for arithmetic operations, handling bit-wise addition with carry.
   2. 4-bit Adder: Composed of 4 full adders, it handles 4-bit addition.
   3. 8-bit Adder: Extends the 4-bit adder to handle 8-bit addition.
   4. 4-bit Multiplier: Performs multiplication of two 4-bit binary numbers, providing an 8-bit product by using and gate for mulptiplication and then using adders for 
      addition of partial products that we obtained .

2. Multiplexers:
 
   1. 2-to-1 Multiplexer: A basic multiplexer that selects between two input values based on a control signal.
   2. 4-bit 2-to-1 Multiplexer: Extends the 2-to-1 multiplexer to handle 4-bit values.
   3. 9-to-1 Multiplexer: Selects one out of nine 4-bit input values, used to manage the matrix input selection efficiently with one input getting stored at a time , so 
     here  we have used two such multiplexers for matrix A and matrix B input elements.

3. Registers:

   1. PIPO Register: A Parallel In Parallel Out register used to store and manage 4-bit values during the matrix multiplication process. 

4. Matrix Multiplication MAIN MODULE:

   1. MatrixMultiplicationCore: The central module that arranges the multiplication of two matrices. It utilizes the multiplexers to select appropriate matrix elements and 
   the 4-bit multiplier to compute their product .   



DETAILED EXPLANATION:

   -Initialization and Input Selection:
   
1. At the start, the inputs for the matrices A and B are received serially over 18 clock cycles. Two 9-to-1 multiplexers (mux9to1_a and mux9to1_b) are used to select the 
   elements from the matrices A and B respectively.
2. The control signals (clock_count_a and clock_count_b) determine which elements are being selected from the input matrices at each clock cycle. These signals increment 
   with each clock edge, ensuring all elements are captured in the respective registers i.e. inputs of A matrix set into matrix element positions one by one with help of 
   multiplexers as clock_count_a act as a select line and simultaneously this selected input with help of some particular select line also get stored with help of PIPO 
   registers and once we are done with all input elements of matrix A, the same process continues for matrix B .
   
-Register Storage:

1. The selected matrix elements are stored in the PIPO registers (PIPO_REGISTER). These registers latch the input values at each clock edge and store them until the next 
   clock cycle.
2. The PIPO registers ensure that the values of A and B are correctly held for the duration required for multiplication and addition.

-Matrix Multiplication:

1. Once all the inputs are stored in the registers, the multiplication process begins. The matrix multiplication is carried out by multiplying corresponding elements of 
   the matrices A and B following the same procedure of matrix multiplication .
2. The multiplication is performed using the multiplier_4bit module, which takes two 4-bit binary numbers and produces an 8-bit product. For each pair of elements (A[i][k] 
   and B[k][j]), the multiplier computes the partial product. 
3. The partial products generated by the multiplier are then summed up using the adder_8bit module. This module uses the 4-bit adder and the full adder to handle carry 
   propagation and produce the final sum which is a 10 bit number.
4. The addition is performed iteratively for each element of the resulting matrix C. For generating each element the partial sums are stored in registers, and the final 
   sum is computed by summing all partial products  hence giving out the single element of output matrix.
   
 -Clock Cycle Management:
 
1. The entire process is synchronized with the clock signal. At each positive clock edge, the control signals (clock_count_a and clock_count_b) are incremented to select 
   the next element for sending data (input element) one by one to input matrices a and b.
2. The state machine ensures that the multiplication and addition operations are performed in a sequential manner, with each operation being completed before moving on to 
   the next.
   
-Output Generation:

1. The final results of the matrix multiplication are stored in the output registers. The outputs are serialized and provided one at a time, as specified in the project 
   requirements.
2. The output values are latched at each positive clock edge and presented as the final result of the matrix multiplication.

SIMULATION & TESTING:-
In the files that are attached to this github repo we have alse attached a file of TESTBENCH(Final Submission) . With help of these testbenches we can check our results whether they perform matrix multiplication as per the desired results.

CONCLUSION:-
This project presents a matrix multiplication accelerator optimized for binary matrices with 4-bit values. The modular design make it efficient and scalable for various matrix sizes. By following the provided structure and operation flow, you can understand the operation of this accelerator.

