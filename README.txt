# Extra-Credit
.data
prompt_L:  .asciiz "Enter the value for L: "
prompt_M:  .asciiz "Enter the value for M: "
prompt_N:  .asciiz "Enter the value for N: "
error_msg: .asciiz "Illegal Number!\n"

.text
main:
    # Step 1: Input L, M, and N
    jal input_number   # Get input for L
    move $s0, $v0     # Save L in $s0

    jal input_number   # Get input for M
    move $s1, $v0     # Save M in $s1

    jal input_number   # Get input for N
    move $s2, $v0     # Save N in $s2

    # Step 1: Check if the input numbers are legal
    bge $s0, 1, legal_L       # Check if L > 0
    j illegal_number          # L is not legal, prompt again


legal_L:
    bge $s1, 1, legal_M       # Check if M > 0
    j illegal_number          # M is not legal, prompt again

legal_M:
    bge $s2, 1, legal_N       # Check if N > 0
    j illegal_number          # N is not legal, prompt again

legal_N:
    bge $s0, 20, illegal_number   # Check if L <= 20
    bge $s1, 20, illegal_number   # Check if M <= 20
    bge $s2, 20, illegal_number   # Check if N <= 20

 # All numbers are legal, proceed to Step 2
    # ... (Step 2 code will go here)

    # Exit the program
    li $v0, 10
    syscall

input_number:
    # Function to input an integer
    li $v0, 4
    syscall

    li $v0, 5
    syscall
    jr $ra

illegal_number:
    # Display error message and prompt user again
    li $v0, 4
    la $a0, error_msg
    syscall
    j main
