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
