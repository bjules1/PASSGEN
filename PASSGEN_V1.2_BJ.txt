import random
import hashlib
import os
import time
### import these libraries to be able to run the code.
### random = randomization library
### hashlib = password hashing library
### os = use to control the "clear function" to create a cleaner sequence
### time = used to create a 5 second delay before quitting the program


def generate_password(length, chars):
    password = ''.join(random.choice(chars) for _ in range(length))
    return password
### this part defines password length & characters used for randomization

def hash_password(password):
    sha256_hash = hashlib.sha256(password.encode()).hexdigest()
    return sha256_hash
### defines how it hashes the randomized password in sha256


def clear_screen():
    
    os.system('cls' if os.name == 'nt' else 'clear')
### defines when it clears the screen after program is excecuted or exited
"""this section of the code overall defines the processes that will be used
to exceute the progam (essentially stating all the tools in the toolbelt)"""

def main():
    clear_screen()

    print("Welcome to PassGen [v1.2 2024 release]")
    print("Dev. by Bossuet Jules")
    print("All rights reserved.")
### just a simple startup screen

    chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ123456789!@#$%^&*().,'
## state your characters used

    while True:
        number = input('Amount of passwords to generate: ')
        try:
            number = int(number)
            break
        except ValueError:
            print("Please enter a valid integer.")
### must enter a valid whole integer for password amount. 
# if not, an error message will display 
    while True:
        length = input('Input password length: ')
        try:
            length = int(length)
            break
        except ValueError:
            print("Please enter a valid integer.")
### must enter a valid whole integer for password length. 
# if not, an error message will display 

    print('\nHere are your passwords and their hashes:\n')

    for _ in range(number):
        password = generate_password(length, chars)
        hashed_password = hash_password(password)
        print(f"Password: {password} | Hash: {hashed_password}")
### this is where the generated password & hash combination is output
    while True:
        user_input = input("Thank you for using PassGen. Would you like to quit? Y/N ").strip().upper()

        if user_input == 'Y':
            print("Now Quitting...")
            time.sleep(3)  
            clear_screen()
            break
        elif user_input == 'N':
            print('Continuing with PassGen...')
            main() 
        else:
            print("Invalid input. Please enter Y or N.")
            
""" you are now given the option to exit or continue. 
if continuing, it will loop back to the beginning of the program.
if not, it will display an exit dialog with a time delay of 3 seconds. """

if __name__ == "__main__":
    main()