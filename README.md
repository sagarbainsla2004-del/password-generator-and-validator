# password-generator-and-validator
This project focuses on developing a Password Generator and Validator using Python. The goal is to create a system that can automatically generate strong, secure passwords and also validate user-provided passwords based on standard security rules.
import random
import string
import re

# -------------------------------
# Password Generator Function
# -------------------------------
def generate_password(length=12):
    """Generate a strong random password of given length."""
    if length < 6:
        print("Password length should be at least 6 characters.")
        return None

    characters = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(random.choice(characters) for i in range(length))
    return password


# -------------------------------
# Password Validator Function
# -------------------------------
def validate_password(password):
    """Validate password strength based on rules."""
    # Define validation rules
    min_length = 8
    has_upper = re.search(r'[A-Z]', password)
    has_lower = re.search(r'[a-z]', password)
    has_digit = re.search(r'\d', password)
    has_special = re.search(r'[!@#$%^&*(),.?":{}|<>]', password)

    # Check rules
    if len(password) < min_length:
        return "❌ Password too short! Minimum 8 characters required."
    elif not has_upper:
        return "❌ Password must contain at least one uppercase letter."
    elif not has_lower:
        return "❌ Password must contain at least one lowercase letter."
    elif not has_digit:
        return "❌ Password must contain at least one number."
    elif not has_special:
        return "❌ Password must contain at least one special character."
    else:
        return "✅ Password is strong!"


# -------------------------------
# Main Program
# -------------------------------
if _name_ == "_main_":
    print("==== Password Generator and Validator ====")
    print("1. Generate Password")
    print("2. Validate Password")

    choice = input("Enter your choice (1/2): ")

    if choice == '1':
        length = int(input("Enter desired password length: "))
        new_password = generate_password(length)
        if new_password:
            print(f"Generated Password: {new_password}")
    elif choice == '2':
        password = input("Enter password to validate: ")
        result = validate_password(password)
        print(result)
    else:
        print("Invalid choice! Please select 1 or 2.")
