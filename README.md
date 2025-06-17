# Project-Guessing-Gameimport random

def play_number_guessing_game():
    """
    Plays a number guessing game with the user, including difficulty options
    and a limited number of attempts.
    """
    print("Welcome to the Number Guessing Game!")

    # --- Difficulty Selection ---
    while True:
        difficulty_choice = input("Choose difficulty (Easy, Medium, Hard): ").strip().lower()
        if difficulty_choice in ["easy", "medium", "hard"]:
            break
        else:
            print("Invalid difficulty. Please choose Easy, Medium, or Hard.")

    if difficulty_choice == "easy":
        lower_bound = 1
        upper_bound = 50
        max_attempts = float('inf')  # Unlimited attempts
        print("\n--- Easy Difficulty ---")
        print("You have unlimited guesses.")
    elif difficulty_choice == "hard":
        lower_bound = 1
        upper_bound = 200
        max_attempts = 7  # More challenging range, fewer attempts
        print("\n--- Hard Difficulty ---")
        print(f"You have a maximum of {max_attempts} attempts.")
    else:  # medium (default)
        lower_bound = 1
        upper_bound = 100
        max_attempts = 10
        print("\n--- Medium Difficulty ---")
        print(f"You have a maximum of {max_attempts} attempts.")

    secret_number = random.randint(lower_bound, upper_bound)
    attempts = 0
    print(f"I'm thinking of a number between {lower_bound} and {upper_bound}.")

    # --- Game Loop ---
    while True:
        # Check if attempts are exhausted (only applies if not unlimited)
        if max_attempts != float('inf') and attempts >= max_attempts:
            print(f"\nGame Over! You ran out of attempts.")
            print(f"The secret number was {secret_number}.")
            break

        try:
            guess_input = input("Enter your guess: ")
            guess = int(guess_input)
            attempts += 1

            if guess < secret_number:
                print("Too low! Try again.")
            elif guess > secret_number:
                print("Too high! Try again.")
            else:
                print(f"\nCongratulations! You guessed the number {secret_number} in {attempts} attempts.")
                break  # Exit the loop, game won
        except ValueError:
            print("Invalid input. Please enter a whole number.")

        # Display attempts left if applicable
        if max_attempts != float('inf'):
            attempts_left = max_attempts - attempts
            if attempts_left > 0:
                print(f"Attempts left: {attempts_left}")

# --- Main Execution Block ---
if __name__ == "__main__":
    play_number_guessing_game() 
