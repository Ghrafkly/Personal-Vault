## Details
This assessment will be marked out of 40 and based on the report you submit. It has three main parts:
1. Gathering the requirements of the game.
2. Developing a suite of test cases based on the requirements (without coding).
3. Discussing the test strategies employed in developing the test cases.

### Requirements Gathering
Imagine you are tasked with writing and testing Commandle, a simplified version of the Wordle game for the command line (not in the browser). The game interface is shown in the following figure.

The basic gameplay mechanisms and rules are the same as the original game, except for the following simplifications/modifications:

- When checking a word, it is done **case-insensitively**. In other words, the input query is the same as _Query_ and _quErY_, for instance.
- Colours will not be used in Commandle to indicate the correctness of letter placement as in the original game. Instead, it uses ‘#’ to indicate a letter, not in the word, ‘?’ to indicate a letter that is in the word, but not in the correct position, and the letter itself if the letter is in the correct. For example, if the correct word is a query and the current guess is heart, then the feedback given to the user will be #?#r#.
- For each day (midnight to midnight), a maximum of 10 games can be played.  
- For each day (midnight to midnight), the winning percentage is to be recorded and displayed to the user.  
- For a single _session_ of consecutive games, each game needs to have a unique target.
- The game only accepts valid, 5-letter words as input for each guess. A list of valid words will be provided. The game needs to check for validity as well as length.

With the above information, formalise the _functional requirements_ (i.e. game mechanisms/rules) and organise them in bullet points.

Note that there is no _single correct answer_. As the specification above has been (deliberately) kept terse and incomplete, you need to conduct some research on the game and come up with sensible test cases.

### Test Suite Development
Based on the above specification of our Commandle game, you need to develop a suite of test cases. There is no specific format for the test cases. However, each of your test cases should include at least the following components:
- **Test ID.** Each test case should have a unique ID.
- **Description & rationale**. A brief description of the test case and the rationale for including it.
- **Test steps.** Steps that need to be taken to “execute” this test case.
- **Test data.** Data that is necessary for the execution of the test case.
- **Input & expected output.** The provided input and the expected output or system behaviour when the test cases are executed and 'passes'.

The test cases can be documented in the form of a table.

### Test Strategies Discussion
Discuss, briefly, the test strategies you employed when coming up with the test cases. You may refer to the black-box testing techniques you have learned in this unit. In your report, you can discuss individual test cases or a group of test cases when describing a specific strategy you have employed.

## Submission Format
You will need to submit a report, which contains the three parts described. Your report needs to be in pdf format, other file types will not be accepted and will not be marked. The report will include three parts:
1. Requirements: **12 marks** — Requirements gathering and documentation. This part of the report should not exceed **2 pages** in length.
2. The test suite: **20 marks** — Test suite development. This part of the report should be concise: it should not exceed **3 pages** in length.
3. The test strategies: **8 marks** — Testing strategy discussion. This part of the report should not exceed **1 page** in length.

Your final submission should not exceed **6 pages** in length.

Note: the reference list is not included in the word count.

## Marking Guide
![[1. Marking Guide.png]]
