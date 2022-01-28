# Wordle_Solver
Uses a Scrabble dictionary to solve the Wordle puzzle

Wordle (link: https://www.powerlanguage.co.uk/wordle/) is a word game in which the player tries to guess the identity of a hidden five letter word. After submitting a guess, the website reveals which letters of the guessed word are not in the hidden word, which are in the hidden word but in a different position, and which letters are in the correct position for the hidden word. Here is an example:

![alt text](https://github.com/pjconnell/Wordle_Solver/blob/main/Wordle_Pic.PNG)

Assuming that Wordle accepts all Scrabble words and chooses the answer from these words with equal probability, one approach to finding a solution is as follows.

Wordle gives us information on a letter-by-letter basis, so we want to maximize the expected number of words in the Scrabble dictionary that we can rule out with each letter of our guess. To that end, there are three possibilities for the types of words a guessed letter can help us rule out:

- **Scenario 1** if the letter is in the answer in the position we guessed it, then we can rule out all the words that do not have this letter in this position. 

- **Scenario 2** if the letter is in the answer but in a different position, then we can rule out all of the words that do not contain this letter at all.

- **Scenario 3** if the letter does not appear in the answer, then we can rule out all of the words that contain this letter.


However, knowing the number of words we can rule out for each of these possibilties is not enough - we also need an estimate of the probabilty that **Scenario 1** vs. **Scenario 2** vs. **Scenario 3** will be the case. [E.g., there is only one word with "Q" in the second to last spot - "BURQA" - so, putting a "Q" there could potentially rule out a lot of words ... but it is also exceedingly unlikely (~1/9,000 if 5-letter Scrabble words are chosen with uniform probability) to be the case that this happens!]

To estimate the probability that each of these scenarios would happen, we need some information on the distribution of letters within the list of eligible words. The attached program does that by counting the frequency with which each letter occurs in each position for whichever 5-letter Scrabble words we have not excluded yet.

![alt text](https://github.com/pjconnell/Wordle_Solver/blob/main/letter_freq.PNG)

From this count of word frequencies, we can estimate the probabilities for each of our scenarios as:

- Prob(Scenario 1) = []

- Prob(Scenario 2) = []

- Prob(Scenario 2) = []

We can estimate the payoffs as:

- Payoff(Scenario 1) = []

- Payoff(Scenario 2) = []

- Payoff(Scenario 2) = []

Accordingly, the expected value of including a letter in a given position for our guess is: 

EV_i = sum_j^3 Prob(Scenario j)* Payoff(Scenario j)

and the total expected value of a guess would be:

val(guess) = EV_1 + ... + EV_5

*Note of caution*: to avoid double-counting the benefit of (2) and (3) for letters that appear more than once in a word, (B) and (C) should =0 for the second (or higher) occurence of a letter in a word.

Running that on the full list of eligible Scrabble words leaves "ROATE" as the optimal first choice.

The attached program will update the list of words based on information from the results of your guess - recalculating the frequency chart, payoffs and probabilites for the list or remaining words. So far, it has been able to guess the correct Wordle in 2-4 guesses (and hasn't failed yet!).
