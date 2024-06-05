TECHNIQUES USED:
1.	HYBRID APPROACH OF
A.	N-GRAM-based guessing(nlp)
B.	Frequency-based guessing using trie data structure
2.	MULTI-THREADING

GUESS METHOD:
1.	The guess function takes a word (current state of the Hangman word) and the number of tries remaining as input.
2.	If the number of tries is less than 3, it employs the nlp method for a more context-aware guess.
3.	If the number of tries is 3 or more, it falls back to the frequency_guess method for a frequency-based guess.
4.	The function returns either the result from the n-gram method or the frequency-based method, based on the number of tries.
Advantage:
i.	Adaptive Strategy: The approach adapts its guessing strategy based on the number of remaining tries, utilizing the more accurate n-gram method when tries are limited.
ii.	Efficiency: Switching to the simpler frequency-based method with more tries ensures efficient guessing, saving computational resources.
iii.	Balanced Performance: By combining both methods, it aims to balance accuracy and efficiency in letter guessing.

N-gram based guessing:
N-gram based guessing in the Hangman game involves predicting the next letter by analysing the frequency and patterns of pairs or sequences of letters (n-grams) in words from a dictionary, improving the accuracy of letter choices.
Frequency-based guessing:
Frequency-based guessing using a Trie data structure in the Hangman game involves selecting the next letter by considering the most common letters in the remaining words from the dictionary, enhancing the chances of correct letter guesses.

N_GRAM(NLP) METHOD:
1.	The nlp function is responsible for guessing the next letter. It calculates probabilities for each letter based on n-grams (unigrams, bigrams, trigrams, fourgrams, fivegrams) of words from the dictionary.
2.	The make_grms function constructs various n-gram dictionaries from the given dictionary of words. It prepares unigram, bigram, trigram, fourgram, and fivegram frequency counts for different lengths of words.
3.	The code employs a sequence of functions (fivegrm_probs, fourgrm_probs, trigrm_probs, bigrm_probs, unigrm_probs) to calculate probabilities based on n-grams and updates the probabilities vector. Each function considers patterns of known and unknown letters in the given word.
4.	The probability vector (probs) is updated using a weighted combination of probabilities derived from different n-grams. The weights are assigned to favor higher-order n-grams more.
5.	The final probability vector is normalized, and the AI chooses the letter with the highest probability as the guess. If no letter has a high probability, the AI randomly selects from the remaining letters.
Advantage:  The combination of contextual analysis, probabilistic reasoning, and dynamic adaptation results in an advanced guessing method that consistently makes well-informed guesses, leading to improved game performance.
Example:
a.	The method is given the partial word: "b__r__".
b.	It calculates probabilities for the next letter using n-grams.
c.	Using trigrams, it observes that "b" followed by "r" has a high probability based on the dictionary.
d.	Based on bigrams, it notices that "br" followed by any letter could also be likely.
e.	It combines these probabilities, weighting them according to n-gram order.
f.	It selects the letter with the highest combined probability, such as "i".
g.	If no high-probability letter is found, it randomly picks a remaining letter.

FREQUENCY METHOD:
1.	Filtering Words: The method uses the Trie's efficient search to filter words from the dictionary that match the pattern of the partial word.
2.	Letter Frequency: For the filtered words, the method calculates the frequency of each unguessed letter that hasn't been guessed yet.
3.	Common Letters: It compiles a list of common letters based on their frequencies in the remaining words, sorted from highest to lowest.
4.	Letter Selection: The method iterates through the common letters and selects the first letter that hasn't been guessed yet.
5.	Enhanced Guessing: This approach enhances guessing accuracy by considering the likelihood of letters appearing in the context of the partial word.
6.	Trie's Advantage: The Trie data structure enables efficient pattern matching and reduces the search space, making the guessing process quicker and more effective.

Advantage: The method's utilization of both Trie-based pattern matching and frequency analysis allows it to intelligently prioritize guesses, increasing the chances of selecting the correct letter, and thereby improving overall game performance.
Example:
a.	Suppose the Hangman word is initially: _ _ _ _ _ _ _ _ _
b.	The method first filters the dictionary based on the word length and the known letters: filtered_words = ['elephant', 'eleven', 'example', ...]
c.	It calculates the frequency of each letter in the filtered dictionary: 'e': 50, 'a': 30, 'i': 20, ...
d.	The method prioritizes guessing letters based on their frequency in the filtered dictionary.
e.	Let's assume that the letter 'e' has the highest frequency. It hasn't been guessed yet, so the method guesses 'e'
f.	If 'e' is in the word: _ e _ _ _ _ _ _ _, the method continues with the next guess.
g.	If 'e' is not in the word: _ _ _ _ _ _ _ _ _, the method would continue guessing based on the frequency of other letters.

GAMEFLOW:
1.	The Hangman game initializes with a dictionary of words and sets up data structures like n-gram and Trie for word frequency analysis and pattern matching.
2.	For each turn, the guess function is called, which takes the current partial word and the number of remaining tries as inputs.
3.	If the number of remaining tries is less than 3, the function employs the NLP-based strategy (nlp method) to analyze the partial word and guess the next letter.
4.	The NLP strategy computes probabilities of potential letters based on n-gram patterns, adjusting the probabilities with each level of n-gram analysis (5-gram, 4-gram, 3-gram, 2-gram, 1-gram) while considering incorrect guesses and their impact on pattern matching.
5.	If the number of remaining tries is 3 or more, the function resorts to the frequency-based strategy (frequency_guess method). This strategy suggests a letter by calculating the frequency of letters in the remaining words of the dictionary
6.	If no confident letter is found through the above strategies, a fallback is used where the AI guesses the most common vowels (e, a, i, o, u) or any available letter if these vowels are already guessed.
7.	The chosen letter is returned by the guess function to the Hangman game for evaluation.
8.	The game evaluates the guessed letter, updating the guessed letters, the current word, and the number of remaining tries accordingly.
9.	The process repeats until the game ends, either by correctly guessing the word, running out of tries, or solving the word.
10.	The AI's ability to adapt its strategy based on the number of remaining tries provides a dynamic and evolving gameplay experience, enhancing the player's challenge and enjoyment.
