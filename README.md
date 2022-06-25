# guessing_game.py
# Tech Degree Proj-1
"""
Python Web Development Techdegree
Project 1 - Number Guessing Game
--------------------------------

For this first project we will be using Workspaces.

NOTE: If you strongly prefer to work locally on your own computer,
you can totally do that by clicking: File -> Download Workspace in
the file menu after you fork the snapshot of this workspace.
"""

"""Psuedo-code Hints

When the program starts, we want to:
------------------------------------
    1. Display an intro/welcome message to the player.
    2. Store a random number as the answer/solution.
    3. Continuously prompt the player for a guess.
      a. If the guess greater than the solution, display to the player "It's lower".
      b. If the guess is less than the solution, display to the player "It's higher".

    4. Once the guess is correct, stop looping, inform the user they "Got it"
         and show how many attempts it took them to get the correct number.
    5. Let the player know the game is ending, or something that indicates the game is over.

    ( You can add more features/enhancements if you'd like to. )
"""
# write your code inside this function.
import random


scores = []
scores.sort()


def start_game():
    # Set the number of guesses to zero within the function for the start of the game
    num_guesses = 0
    # Set the 'secret number' to a random number between 1 and 10
    num = random.randint(1, 10)
    # Initialize necessary variables
    guess = 0
    score = 0
    global scores
    # Print a welcome message to the user
    print("""
        =======================================================================
        Welcome to the Number Guessing Game! Try to guess our secret number!!!!
        =======================================================================
        """)
    # User will be prompted for a guess as long as their answer is not right
    while guess != num:
        # Take a guess from the user
        guess = (input("Guess any number between 1 and 10 and hit Enter >>>   "))
        num_guesses += 1
        # Set the score as the number of guesses
        score = num_guesses
        # Taking an input might throw a ValueError, this will be the catch
        try:
            guess = int(guess)
        except ValueError as err:
            print("Your entry is invalid. Try again but this time, only enter "
                  "a positive whole number between 1 and 10")
            print("Error: {}.".format(err))
            continue
        # Make sure their guess is in bounds
        if guess > 10 or guess < 1:
            print("Your guess is out of bounds. Guess any positive integer between 1 and 10")
        elif guess < num:
            print("It's higher")
        elif guess > num:
            print("It's lower")
        if guess == num:
        # Print a message when they guess correct and let them know how many attempts they made
            print("Congrats!!! You Got it in only {} attempts! the secret number was {}".format(num_guesses, num))
            scores.append(score)
            scores.sort()
            print("Your score: {}".format(score))
            print("High Score: {}".format(scores[0]))
            keep_going = input("""Would you like to continue? 
Press any key to continue, otherwise, type 'N' to end the game >>>  """)
            if keep_going.upper() == "N":
                if len(scores) > 1:
                    highest_score = min(scores)
                else:
                    highest_score = score
                break
            else:
                num_guesses = 0
                print("""
                                         ~~~~~ High Score: {} ~~~~~""".format(scores[0]))
                start_game()
                if len(scores) > 1:
                    highest_score = min(scores)
                else:
                    highest_score = score


# Kick off the program by calling the start_game function.
start_game()
print("Thanks for playing!!")