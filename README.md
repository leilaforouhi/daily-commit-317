import string


def check_password_strength(password):
    checks = {
        "At least 8 characters": len(password) >= 8,
        "Contains uppercase letters": any(c.isupper() for c in password),
        "Contains lowercase letters": any(c.islower() for c in password),
        "Contains digits": any(c.isdigit() for c in password),
        "Contains special characters": any(
            c in string.punctuation for c in password
        ),
    }

    score = sum(checks.values())

    if score <= 2:
        strength = "Weak"
    elif score <= 4:
        strength = "Moderate"
    else:
        strength = "Strong"

    return strength, checks


if __name__ == "__main__":
    password = input("Enter a password to evaluate: ")
    strength, checks = check_password_strength(password)

    print(f"\nPassword strength: {strength}")

    for requirement, passed in checks.items():
        status = "PASS" if passed else "FAIL"
        print(f"[{status}] {requirement}")
