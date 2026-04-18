# SimpleForLoop
A simple for loop game


https://rhoded-uwp.github.io/SimpleForLoop/

# SimpleForLoop

A browser-based speed drill that quizzes intro Python students on the three variants of `for _ in range(...)`. Built as a single HTML file, deployed on GitHub Pages, and embedded in Canvas via iframe.

**Live demo:** https://rhoded-uwp.github.io/SimpleForLoop/

Built for CS 1430 (Intro to Programming in Python) at UW-Platteville. Free to fork, remix, and use in your own classroom.

## What it does

Four levels, timed, with first-try accuracy tracked separately from retries:

1. **Simple repeat** (3 correct): `for _ in range(N):`
2. **Start and stop** (2 correct): `for _ in range(start, stop):`
3. **Start, stop, step** (2 correct): `for _ in range(start, stop, step):`
4. **Challenge mix** (4 correct): all three variants shuffled, with at least one guaranteed from each prior level

If a student answers wrong, the game shows them the correct code and makes them retype it before continuing. The retype does NOT count toward their correct total, which keeps the pressure on first-try accuracy without letting them get stuck.

Final score is a function of first-try correct answers minus a time penalty, with ranks ranging from "Script Kiddie" to "Kernel Overlord" to give students something to chase.

## Classroom use

Drop the Pages URL into a Canvas page as an iframe. Students hit it as a practice warmup before a loops quiz, or as a speedrun competition in class. No login, no accounts, no data stored.

## The Vibe Coding Process

This project was built in one conversation with Claude Opus 4.7 using what Steve Yegge calls "vibe coding": describe the thing you want clearly enough, let the model write it, then iterate from what you see. No scaffolding, no boilerplate hunting, no Stack Overflow tabs. Two prompts, one working tool.

I am publishing the actual prompts below so other instructors can see what level of specificity the model needed. The quality of the output tracked the quality of the prompt almost exactly.

### Prompt 1: The full spec

> Help me write a single file, HTML file, that will be uploaded to GitLab as a static web site. create a HTML game for intro to Python students that quizzes them on for loops. Can it be in a dark hacker theme, but please keep the background plain black, avoid distracting gifs etc. The goal will be to master all the levels of for loops in as short a time as possible. For each level ask the user to write a different number of correct examples, check for accuracy, keep the timer going. If they get it wrong, show them the correct code and ask them to retype it, when they are correct then continue. Do not count these are correct answers. Level 1 - Simple for loop - Senario - Write the first line of a python for loop with an underscore iterator, that will repeat 3 times. (Just vary the repeat) Level one requires 4 correct for loops. Level 2 - more complicated for loop, Write the first line of a python for loop with an underscore iterator that starts at 2 and stops at 22 (just vary the 2 and 22) Level 2 requires 3 correct for loops. Level 3 = Start, Step, Stop - Ask the students to write a for loop in python with an underscore iterator that starts a 3, counts to 33 by 5's. (Just vary the 3, 33, and 5's) Level 3 requires 2 correct for loops - Level 4 Challenge level - 5 correct answers - answer questions for all levels mixed, but ensure at least one from each level. When done show a number correct, number wrong and total time. Create a scoring algorithm based on time and percentage of correct the first time answers.

That prompt produced a working game on the first try. Theme, mechanics, randomization, retype flow, scoring, and final screen, all in one shot.

### Prompt 2: The playtesting adjustment

After demoing it to students:

> This amazing. The game took a little too long. Can you can the levelReqs to 3 at level 1, 2 at level 2 and 3 then 4 at level 4

One config change, Claude adjusted the requirements array, updated the briefing text, updated the final screen total, rebalanced the Level 4 queue builder, and rescaled the rank thresholds since the max possible score dropped. That kind of cascading edit is where an AI coding assistant earns its keep. I would have missed the rank thresholds and shipped a broken scoreboard.

### What Claude Opus 4.7 actually did

For instructors new to this workflow, here is where the model added value that would be hard to replicate manually in the same timeframe:

- **Translated a natural-language spec into working code.** I described the game in conversational English with typos and the model built regex-based answer validators that tolerate whitespace variants like `for  _  in range( 5 ):` while rejecting wrong iterator names, missing colons, or wrong case.
- **Made reasonable design choices I did not specify.** Terminal green on black, monospace font, blinking cursor, color-coded feedback (green for success, yellow for retype, red for error), a mobile-responsive layout. I said "dark hacker theme" and got a coherent aesthetic.
- **Tested its own output.** Before handing back the file, it ran a syntax check on the script block and fed test strings through the answer regex to confirm both positive and negative cases behaved. I did not ask it to do this.
- **Cascaded a small change correctly.** The Prompt 2 edit touched five different parts of the code that all needed to stay in sync. Getting that right by hand is the kind of thing that causes subtle bugs two weeks later.
- **Explained its reasoning in the handoff.** It flagged which constants to tune if I wanted different difficulty or scoring, saving me from re-reading code later.

What Claude did NOT do: design the activity. The pedagogy, the level structure, the retype-to-continue mechanic, and the decision to separate first-try correct from retry correct were all instructor judgment calls. The model is a good builder, not a good curriculum designer.

## Takeaways for other instructors

If you want to build tools like this:

1. **Write the spec like you are briefing a competent TA.** State the audience, the goal, the constraints, and the specific mechanics. Ambiguity in the prompt becomes ambiguity in the code.
2. **Specify what you do NOT want.** "Plain black background, no distracting gifs" saved a round trip. Negative constraints are as useful as positive ones.
3. **Playtest with real students before you iterate.** My first adjustment was a length complaint I could not have predicted from my own playthroughs. Students are faster than you think.
4. **Single HTML file plus GitHub Pages plus Canvas iframe is a shockingly good stack.** No build tools, no server, no database, no accounts. Students get a fast tool, you get a URL you can embed anywhere.

## Forking and adapting

Clone or fork the repo, edit `index.html`, push. GitHub Pages picks it up automatically.

Good places to customize:

- `levelReqs` array near the top of the script controls how many correct answers each level needs
- `genLevel1`, `genLevel2`, `genLevel3` set the number ranges for difficulty
- `computeScore` controls the time penalty weighting
- `rankForScore` sets the rank labels and thresholds
- CSS variables at the top of the `<style>` block control the color scheme if you want a different theme

You could adapt this same structure for while loops, list comprehensions, if/elif/else chains, function definitions, or any other syntax pattern that has a small number of variations. The retype-on-wrong mechanic works for anything where the goal is muscle memory.

## Credits

Game designed by Dan Rhode, UW-Platteville CS Department. Code written by Claude Opus 4.7 (Anthropic) through two conversational prompts. Published under no warranty, use freely, attribution appreciated but not required.

If you use this or adapt it for your own classroom, I would love to hear about it. Ping me on GitHub.
