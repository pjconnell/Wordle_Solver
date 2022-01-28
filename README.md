# Wordle_Solver
Uses a Scrabble dictionary to solve the Wordle puzzle

Wordle (link: https://www.powerlanguage.co.uk/wordle/) is a word game in which the player tries to guess the identity of a hidden five letter word. After submitting a guess, the website reveals which letters of the guessed word are not in the hidden word, which are in the hidden word but in a different position, and which letters are in the correct position for the hidden word. Here is an example:

![alt text](https://github.com/pjconnell/Wordle_Solver/blob/main/Wordle_Pic.PNG)

Assuming that Wordle accepts all Scrabble words and chooses the answer from these words with equal probability (not necessarily so, see ...), one approach to finding a solution is as follows.

~10,000 5-letter scrabble words.

want to maximize the number we can rule out with each guess.

wordle gives us info on a letter-by-letter basis, so we want to maximize the expected amount of ruling out that we can do with each letter of our guess.

We want to figure out what the value of including each letter in our guess is. There are three possibilities: 

(1) that the letter is in the answer, in the position we guessed it. In this case, we can rule out all the words that do not have this letter in this position. 

(2) that the letter is in the answer, but in a different position. In this case, we can rule out all of the words that do not contain this letter at all.

(3) that this letter does not appear in the answer. In this case, we can rule out all of the words that contain this letter.


However, knowing the potential payoff for each of these possibilties is not enough - we also need an estimate of the probabilty that (1) vs. (2) vs. (3) will be the case. [E.g., there is only one word with "Q" in the second to last spot - putting a "Q" there could potentially rule out a lot of potential words ... but it is also exceedingly unlikely to be correct!]

To estimate these probabilities, we need some information on the distribution of letters within the list of eligible words

[Insert wd. freq. chart]

From this count of word frequencies, we can estimate the probabilities for each of our scenarios as:

(1) [...]

(2) [...]

(3) [...]

We can estimate the payoffs as:

(A) [...]

(B) [...]

(C) [...]

Accordingly, the expected value of including a letter in a given position for our guess is: (1)(A)+(2)(B)+(3)(C), and the total expected value of a guess would be:

val(guess) = EV_1 + ... + EV_5

*Note of caution*: to avoid double-counting the benefit of (2) and (3) for letters that appear more than once in a word, (B) and (C) should =0 for the second (or higher) occurence of a letter in a word.

Running that on the full list of eligible Scrabble words leaves "ROATE" as the optimal first choice.

The attached program will update the list of words based on information from the results of your guess - recalculating the frequency chart, payoffs and probabilites for the list or remaining words. So far, it has been able to guess the correct Wordle in 2-4 guesses (and hasn't failed yet!).
