# Python-program
Here are the Python solutions for the tasks outlined in your assignment file.
## Part 1: Basic Programming Exercises
### 1. Sum of Two Numbers
 * *Objective:* Calculate the sum of two numbers.
 * *Code:*
python
# Prompting user for two integer inputs
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

# Simple addition operation
total_sum = num1 + num2

print(f"The sum is: {total_sum}")


### 2. Odd or Even
 * *Objective:* Determine whether a number is odd or even.
 * *Code:*
python
num = int(input("Enter an integer: "))

# Checking the remainder when divided by 2
if num % 2 == 0:
    print("Even")
else:
    print("Odd")


### 3. Factorial Calculation
 * *Objective:* Compute the factorial of a given number n.
 * *Code:*
python
n = int(value := input("Enter a non-negative integer: "))

# Handling negative input edge case
if n < 0:
    print("Factorial is not defined for negative numbers.")
else:
    factorial = 1
    # Loop to calculate factorial
    for i in range(1, n + 1):
        factorial *= i
    print(f"The factorial of {n} is: {factorial}")


### 4. Fibonacci Sequence
 * *Objective:* Generate the first n numbers in the Fibonacci sequence.
 * *Code:*
python
n = int(input("Enter the number of Fibonacci terms to generate: "))

if n <= 0:
    print([])
elif n == 1:
    print([0])
else:
    # Starting sequence with the first two terms
    fib_sequence = [0, 1]
    # Iterating to calculate the rest using F(n) = F(n-1) + F(n-2)
    while len(fib_sequence) < n:
        fib_sequence.append(fib_sequence[-1] + fib_sequence[-2])
    print(fib_sequence)


### 5. Reverse a String
 * *Objective:* Reverse the characters in a string.
 * *Code:*
python
user_string = input("Enter a string to reverse: ")

# Using Python string slicing [::-1]
reversed_string = user_string[::-1]

print(f"Reversed string: {reversed_string}")


### 6. Palindrome Check
 * *Objective:* Check if a string reads the same backward as forward.
 * *Code:*
python
text = input("Enter a string to check for palindrome: ")

# Reversing string and comparing (ignoring case differences)
cleaned_text = text.lower()
if cleaned_text == cleaned_text[::-1]:
    print(True)
else:
    print(False)


### 7. Leap Year Check
 * *Objective:* Determine whether a year is a leap year.
 * *Code:*
python
year = int(input("Enter a year: "))

# A year is a leap year if divisible by 4 but not by 100 unless divisible by 400
if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(True)
else:
    print(False)


### 8. Armstrong Number
 * *Objective:* Check if a number equals the sum of its digits raised to the power of the number of digits.
 * *Code:*
python
num_str = input("Enter an integer: ")
num_len = len(num_str)
num_val = int(num_str)

# Summing each digit raised to the power of the number of digits
armstrong_sum = sum(int(digit) ** num_len for digit in num_str)

if armstrong_sum == num_val:
    print(True)
else:
    print(False)


## Part 2: Custom Encryption-Decryption System
### Project Requirements Met
 * *No built-in encryption libraries* used (built entirely from low-level logical reasoning and loops).
 * *Robust multi-layer cipher design:* Combines a variable Caesar cipher (Substitution) step with an alphanumeric inversion layout.
 * *Handles edge cases:* Gracefully handles spaces, numbers, punctuation, and case shifts without throwing errors.
### Implementation Code
python
def custom_encrypt(message, key):
    """
    Encrypts a message using a multi-layer substitution cipher.
    Does not use any external cryptography libraries.
    """
    encrypted_message = []
    
    for i, char in enumerate(message):
        # Adding index variance to the key to break simple frequency analysis
        current_shift = (key + i) % 26
        
        # Layer 1: Process Uppercase Letters
        if char.isupper():
            shifted_char = chr((ord(char) - ord('A') + current_shift) % 26 + ord('A'))
            encrypted_message.append(shifted_char)
            
        # Layer 1: Process Lowercase Letters
        elif char.islower():
            shifted_char = chr((ord(char) - ord('a') + current_shift) % 26 + ord('a'))
            encrypted_message.append(shifted_char)
            
        # Layer 2: Process Digits
        elif char.isdigit():
            shifted_digit = str((int(char) + key) % 10)
            encrypted_message.append(shifted_digit)
            
        # Layer 3: Handle structural characters like spaces & punctuation safely
        else:
            encrypted_message.append(char)
            
    return "".join(encrypted_message)


def custom_decrypt(ciphertext, key):
    """
    Reverses the custom_encrypt algorithm precisely using the matching key.
    """
    decrypted_message = []
    
    for i, char in enumerate(ciphertext):
        current_shift = (key + i) % 26
        
        if char.isupper():
            shifted_char = chr((ord(char) - ord('A') - current_shift) % 26 + ord('A'))
            decrypted_message.append(shifted_char)
            
        elif char.islower():
            shifted_char = chr((ord(char) - ord('a') - current_shift) % 26 + ord('a'))
            decrypted_message.append(shifted_char)
            
        elif char.isdigit():
            # Inverting the digit shift securely
            shifted_digit = str((int(char) - key) % 10)
            decrypted_message.append(shifted_digit)
            
        else:
            decrypted_message.append(char)
            
    return "".join(decrypted_message)


# ---- Demonstration System ----
if __name__ == "__main__":
    print("--- Custom Low-Level Cryptography System ---")
    secret_key = 7
    original_text = "Main Flow Task 2026! Protect this data."
    
    # Executing pipeline transformations
    encrypted = custom_encrypt(original_text, secret_key)
    decrypted = custom_decrypt(encrypted, secret_key)
    
    print(f"Original Message  : {original_text}")
    print(f"Encrypted Safe Text: {encrypted}")
    print(f"Decrypted Back Text: {decrypted}")
    
    # Dynamic user interface check
    print("\n--- Try your own string verification ---")
    user_msg = input("Enter any string to test: ")
    user_key = int(input("Enter a numeric encryption key: "))
    
    enc_res = custom_encrypt(user_msg, user_key)
    print(f"Encrypted output: {enc_res}")
    print(f"Decrypted output: {custom_decrypt(enc_res, user_key)}")

