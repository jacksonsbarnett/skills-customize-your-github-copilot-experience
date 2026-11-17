# 📘 Assignment: Hangman Game

## 🎯 Objective

Build a Hangman game where players guess letters to reveal a hidden word before running out of attempts. Practice string manipulation, loops, conditionals, user input, and random selection in Python.

## 📝 Tasks

### 🛠️ Select a Word and Display Guesses

#### Description
Choose a random word from a predefined list and let the player guess letters to reveal it.

#### Requirements
Completed program should:

- Randomly select a word from a predefined list at the start of the game.
- Display an underscore for each unguessed letter, separated by spaces (for example, `_ _ _`).
- Accept letter guesses using `input()`.
- Reveal every occurrence of a correctly guessed letter while keeping unguessed letters hidden.

### 🛠️ Track Attempts and End the Game

#### Description
Track the player's remaining incorrect guesses and end the game when the player wins or runs out of attempts.

#### Requirements
Completed program should:

- Start with a fixed number of allowed incorrect guesses and display that number to the player.
- Reduce the remaining attempts by one for each incorrect guess and display the updated count.
- Continue accepting guesses while the word is incomplete and attempts remain.
- End the game with a win message when all letters have been revealed.
- End the game with a lose message and reveal the word when no attempts remain.
