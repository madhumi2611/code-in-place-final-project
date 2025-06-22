# Stanford Code in Place - Final Project (The WordGuess game)
This is one of the final project ideas for Code in Place. It is a console based project.
<br>
When the user plays WordGuess, the computer first selects a secret word at random from a list built into the program. The program then prints out a row of dashes—one for each letter in the secret word and asks the user to guess a letter. If the user guesses a letter that is in the word, the word is redisplayed with all instances of that letter shown in the correct positions, along with any letters correctly guessed on previous turns. If the letter does not appear in the word, the user is charged with an incorrect guess. The user keeps guessing letters until either (1) the user has correctly guessed all the letters in the word or (2) the user has made eight incorrect guesses. A sample run of the game is shown below.

The Word Guessing Game: https://codeinplace.stanford.edu/cip5/share/XoEYB6KZI1lgV2Gp47km


<img src="https://github.com/madhumi2611/code-in-place-final-project/blob/main/SampleRun.png">
<br>

# Deployment
To deploy this project run
```bash
"""
Project: Word Guessing Game
-------------------
"""
import random

LEXICON_FILE = "Lexicon.txt"  # File to read word list from
INITIAL_GUESSES = 7           # Max number of guesses per game


def play_game(secret_word):
    guesses= INITIAL_GUESSES
    curr_word= ['-']* len(secret_word)
    while guesses!=0 :
        print("The word now looks like this: ", end="")
        for text in curr_word:
            print(text, end="")
        print()
        print(f"You have {guesses} guesses left")
        letter= input("Type a single letter here, then press enter: ")
        if len(letter) != 1:
            print('Guess should be a single uppercase letter.')
            continue
        if letter not in secret_word:
            guesses-=1
            print(f"There are no {letter}'s in the word")
        else:
            print("That guess is correct")
            for i in range (len(secret_word)):
                if secret_word[i] == letter:
                    curr_word[i]= letter

            if '-' not in curr_word:
                print(f"Congratulations, the word is: {secret_word}")
                return

    print(f"Sorry, you lost. The secret word was: {secret_word}")
    return

def get_word(filename):
    """
    This function returns a secret word that the player is trying
    to guess in the game.  This function initially has a very small
    list of words that it can select from to make it easier for you
    to write and debug the main game playing program.  In Part II of
    writing this program, you will re-implement this function to
    select a word from a much larger list by reading a list of words
    from the file specified by the constant LEXICON_FILE.
    """
    with open (filename, "r") as fp:
        words= fp.readlines()
        for i in range(len(words)):
            words[i]= words[i].strip()
        word = random.choice(words)
        return word

def main():
    """
    To play the game, we first select the secret word for the
    player to guess and then play the game using that secret word.
    """
    secret_word = get_word(LEXICON_FILE)
    play_game(secret_word)

if __name__ == "__main__":
    main()
```
