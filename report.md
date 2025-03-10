# Report for assignment 4

## Project

Name: Discord bot

URL: https://github.com/python-discord/bot

This project is a Discord bot specifically for use with the Python Discord server. It provides numerous utilities and other tools to help keep the server running like a well-oiled machine.

## Onboarding experience

We continue on the previous project, the onboarding experience can be found in the [report for assignment 3](https://github.com/SEF-Group-25/discord-bot/blob/main/report.md)

## Effort spent (Tang)
plenary discussions/meetings;
- a meeting to decide the issue, 1h
- a discussion over the plan to solve the issue, 2h
- a meeting to decide the division of work, 1h

discussions within parts of the group;
- voice call to confirm technical details, 1h
- text discussion, 1h

reading documentation;
- search and read documentation and manual, 3h

configuration and setup;
- set up and run the bot using docker, 30m

analyzing code/output;
- analyze the source code structure, 2h
- analyze the feature and utility functions we need to use, 2h

writing documentation;
- write the report, 2h
- draw diagrams, 2h

writing code;
- write the feature code, 2h
- write test cases, 1h

running code?
- running the bot and test cases, 2h

## Effort spent (Zubair)
plenary discussions/meetings;
- a meeting to decide the issue, 1h
- a discussion over the plan to solve the issue, 2h
- a meeting to decide the division of work, 1h

discussions within parts of the group;
- voice call to confirm technical details, 1h
- text discussion, 1h

reading documentation;
- reading documentation and instructions on github page, 2h

configuration and setup;
- set up and run the bot using docker, 30m

analyzing code/output;
- analyze the source code structure, 5h

writing documentation;
- write the report, 1h

writing code;
- write the feature code, 4h
- write test cases, 2h

running code?
- running the bot and test cases, 1h

## Effort spent (Oscar)
plenary discussions/meetings;
- a meeting to decide the issue, 1h
- a discussion over the plan to solve the issue, 2h
- a meeting to decide the division of work, 1h

discussions within parts of the group;
- voice call to confirm technical details, 1h
- text discussion, 2h

reading documentation;
- reading documentation and instructions on github page, 3h

configuration and setup;
- set up and run the bot using docker, 3h, mostly due to it not playing nice with ARM chips and emulation.

analyzing code/output;
- analyze the source code structure, 7h

writing documentation;
- write the report, 1h

writing code;
- write the feature code, 1h
- write test cases, 2h

running code?
- running the bot and test cases, 1h

## Effort spent (Anton Yderberg)
plenary discussions/meetings;
- a meeting to decide the issue, 1h
- a discussion over the plan to solve the issue, 2h
- a meeting to decide the division of work, 1h

discussions within parts of the group;
- voice call to confirm technical details, 1h
- text discussions, 1h (roughly)

reading documentation;
- reading documentation and instructions on github page, 1h

configuration and setup;
- set up and run the bot using docker, 30m

analyzing code/output;
- analyze the source code structure, 5h

writing documentation;
- write the report, 30min

writing code;
- write the feature code, 3h
- write test cases, 3h

running code?
- running the bot and test cases, 2h

## Overview of issue(s) and work done.

Title: Keyword Alerts

URL: https://github.com/python-discord/bot/issues/3153

Send a DM to members when the bot detects a certain keyword in the incoming messages. And also be careful of malicious trigger of the detector (DDoS attack).

To fix this issue, a new command will be added to the bot. It is a new feature so it won't affect other functionalities of the discord bot.

## Requirements for the new feature or requirements affected by functionality being refactored

### Requirement: Spam Check #6 (Tang)

Title: Rate Limiting System for Preventing Malicious Trigger Abuse

Description:
This system implements a rate limiter to prevent users from excessively triggering a specific action (e.g., sending a DM) within a short time frame. It tracks message triggers per user and enforces a threshold-based restriction within a defined time window. If a user exceeds the allowed trigger count, they are flagged as malicious.

Test cases: test_spam_check.py

### Requirement: Add `track` command #4 (Zubair)
Title: Add `track` command to track words

Description:
Command that takes a string as an argument of what should be kept track of.
I.e /track hello sets up the bot to track the word "hello".

Test cases: test_word_tracker.py

### Requirement: Add DMs #3 (Oscar)
Title: Add functionality to send DM

Description:
Function that sends a DM with a message

Test cases: test_detect.py, https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/tests/bot/exts/stalking_system/test_detect.py#L10
The 4 tests in TestSend_DM.

### Requirement: Add message detection #5 (Anton)
Title: Word stalker

Description:
Function to scan for words specified in #4.
Also responsible for calling spam check and send DM functions if match is found.

Test cases: test_detect.py
Link to the line start of my test class for the detect class: https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/stalking_system/test_detect.py#L54

There are 3 test cases, within the class. One that makes sure it ignores bot messages, one that makes sure nothing happens if the channel is not on the list of tracked channels and one that tests if spam get blocked correctly if is_malicious() returns true.

## Code changes

### Patch

To see code added for the feature: `git diff 314ccbb 237da3d`.

To see code added for the DM feature, click here https://github.com/SEF-Group-25/stalking-system/pull/18/files. This function sends a discord DM to a specified user, with a specified message. It contains error handling and testing has 100% coverage.

### Code for `word_tracker.py` (Zubair)
`read_json(self)` and `write_json(self, data: dict)`: These two files are simple util functions used to read and write to the json file created by the track command. **Links:** 
https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/exts/utils/word_tracker.py#L20

https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/exts/utils/word_tracker.py#L30C20-L30C36

`track_word(self, ctx: Context, word: str)`: Stores the tracking information for a word in the current channel. **Link:** 
https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/exts/utils/word_tracker.py#L39C25-L39C55

`show_tracked(self, ctx: Context)`: Shows all the tracked words by all users in the current channel. **Link:** 
https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/exts/utils/word_tracker.py#L56

` untrack_word(self, ctx: Context, word: str)`: Stops tracking a specific word in the current channel. **Link:** 
https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/exts/utils/word_tracker.py#L73C14-L73C58

Test cases for all functions can be found here: 
https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/utils/test_word_tracker.py#L10

### Code for `spam_check.py` (Shangxuan Tang)
The RateLimiter component ensures that the system does not send excessive notifications due to spam or frequent message triggers. It maintains a record of user-triggered events and enforces a threshold-based limit within a defined time window.

Key Methods:

[is_malicious](https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/utils/spam_check.py#L18)(user, timestamp) -> bool

- Checks if a user has triggered too many notifications in a short period.
- Compares the user's message timestamps against a predefined threshold and time window.
- Returns True if the user exceeds the limit, indicating potential spamming behavior.

[record_trigger](https://github.com/SEF-Group-25/stalking-system/blob/cf52e4ede63794bd2fb63e5b7951e25228b5e4dc/bot/utils/spam_check.py#L37)(user, timestamp)

- Records the time at which a user triggers a notification event.
- Maintains a history of timestamps for each user to track their message frequency.
- Ensures old timestamps are removed after the defined time window to maintain efficiency.

Tests for RateLimiter:

[test_below_threshold](https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/stalking_system/test_spam_check.py#L11)()

A user sends two messages within the time window, staying below the defined threshold (3 messages). The test asserts that the user is not flagged as malicious.

[test_exceed_threshold](https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/stalking_system/test_spam_check.py#L21)()

A user sends three messages within a short time, exceeding the threshold. The test asserts that the user is flagged as malicious.

[test_old_messages_are_ignored](https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/stalking_system/test_spam_check.py#L32)()

The user has older messages outside the time window, which should not contribute to the rate limit check.
A new message is sent within the window, but the user remains below the threshold. The test asserts that the user is not flagged as malicious.

[test_independent_users](https://github.com/SEF-Group-25/stalking-system/blob/bddf60c09ce32a5193f1b8a52d794876cb6e2c37/tests/bot/exts/stalking_system/test_spam_check.py#L43)()

Two users are tested separately. User 1 exceeds the threshold and is flagged as malicious. User 2 has no recorded messages, so they should not be flagged. This ensures that each user is tracked independently.

To see code added for Detect() class and the on_message event listener, click here: https://github.com/SEF-Group-25/stalking-system/blob/ab9e58663371a2840664343a17be69c66e926503/bot/exts/stalking_system/detect.py#L19

The main function "on_message" for every message reads in a json file that is tracking all words that are currently being tracked. Checks if the message itself is in a tracked channel and isnt sent by a bot. And then checks if the message contains any key words. If yes it then calls the rate limiters "is_malicious()" method to check if it should start sending DMs. If it does then it loops through everyone who was tracking that keyword and sends them a DM by calling the send_DM() method. It sends a seperate DM to every person for every relevant keyword that was mentioned in the message.

## Test results
Before:
========================================= short test summary info =====================================================
FAILED tests/bot/exts/stalking_system/test_detect.py::TestDetect::test_spam_blocked - NameError: name 'Detect' is not defined

FAILED tests/bot/exts/stalking_system/test_detect.py::TestDetect::test_ignore_bot_message - NameError: name 'Detect' is not defined

FAILED tests/bot/exts/stalking_system/test_detect.py::TestDetect::test_no_tracked_channel - NameError: name 'Detect' is not defined

============================ 3 failed, 431 passed, 1 skipped, 733 warnings in 17.33s ====================================
Branch be found here https://github.com/SEF-Group-25/stalking-system/tree/origin/test/2-detect-tests

After:

=============================== 451 passed, 1 skipped, 742 warnings in 8.90s ================================
Branch https://github.com/SEF-Group-25/stalking-system


## UML class diagram and its description

![UML](./UML.jpg)

### Architectural overview

#### System Purpose and Objectives
The Stalking System is a newly introduced feature designed to allow users to track specific words in Discord messages and receive notifications via direct messages (DMs) when these words appear.

However, to prevent abuse, the system also implements a rate-limiting mechanism that ensures users do not receive excessive notifications due to spam or malicious behavior. By balancing real-time monitoring with controlled notifications, the system provides a user-friendly and efficient experience without overwhelming users with unnecessary alerts.

The main objectives of this feature include:

- Enabling users to track, untrack, and review monitored words.
- Automatically detecting messages that contain tracked words and notifying the respective users.
- Implementing rate limiting to prevent excessive notifications from spammy or repeated triggers.
- Seamlessly integrating into the existing Discord bot architecture while maintaining modularity and scalability.

#### System Architecture and Feature Integration
To integrate the Stalking System efficiently into the Discord bot, the architecture is built around key components: Commands.Bot and Commands.Cog.

Commands.Bot serves as the central manager for the Discord bot. It is responsible for:

- Managing commands and cogs by registering them dynamically.
- Processing user inputs and invoking the corresponding command functions.
- Handling event listeners that allow the bot to react to messages and other interactions.
- The bot acts as the entry point of the system, ensuring that features can be modularized while maintaining a single source of execution and management.

To maintain a clean and scalable architecture, Discord bot functionalities are implemented using Cogs. A Cog is a class that groups related commands and event listeners together, making it easier to manage and extend features.

- Each Cog registers its commands and event listeners with the bot.
- The bot automatically detects and loads Cogs, ensuring modular functionality.
- Cogs can be independently developed and maintained, avoiding monolithic code structures.

By using Cogs, the system organizes different features into separate modules, making it easier to add new functionalities without modifying the bot’s core logic.

In addition, decorators play a crucial role in registering commands and event listeners dynamically. The Discord bot framework provides decorators such as @commands.command() and @commands.Cog.listener() to streamline functionality.

- @commands.command() marks a function as a command that can be invoked by users.
- @commands.Cog.listener() designates a function as an event listener, allowing it to react to incoming messages and other Discord events.

With the Discord bot architecture in place, the Stalking System was integrated as a new feature using the Cog structure and decorators. The system comprises three main components:

WordTracker: Managing Tracked Words
- Provides commands to allow users to /track, /untrack, and /tracked words.
- Uses @commands.command() to register tracking-related functionalities.

Detect: Monitoring Messages and Sending Alerts
- Listens for messages using @commands.Cog.listener().
- Checks if a message contains a tracked word and sends a DM to the tracking user.

RateLimiter: Preventing Spam and Abuse
- Stores timestamps of tracked-word notifications for each user.
- Enforces a threshold-based rate-limiting mechanism to prevent excessive notifications.
- Used within the Detect component to validate if a notification should be sent.

### Relation to design patterns

The newly added command follows three key design patterns: Command Pattern, Observer Pattern, and Decorator Pattern. These patterns contribute to a modular, maintainable, and scalable architecture for the bot's functionality.

#### Command Pattern
The bot’s command system is structured using the Command Pattern, where each command is encapsulated as an independent function inside a `commands.Cog` subclass. By using this pattern, the bot's command system becomes more scalable since new commands can be added simply by creating new Cog classes without modifying the existing system.

#### Observer Pattern
The bot’s event-driven system follows the Observer Pattern, where multiple event listeners can be registered dynamically and notified when an event occurs. The `Cog` class registers event listeners, allowing them to subscribe to specific Discord events, such as `on_message`. The bot acts as the subject (publisher), and the Cog modules function as observers (subscribers). When an event (e.g., a message being sent) occurs, all registered observers are notified and can execute their logic.

#### Decorator Pattern
The command system uses the Decorator Pattern to define and register both commands and event listeners. The `@commands.command()` decorator automatically registers a method as a bot command without requiring manual intervention. The `@commands.Cog.listener()` decorator transforms a method into an event handler, making it a part of the bot’s event-driven system. Instead of manually mapping function names to commands or events, decorators enhance readability by explicitly marking functions as commands or listeners.

## Overall experience (Tang)

From this project, I learned how to work as a group to solve code issues. We discussed the direction of solving the problem and developed a plan in detail. This is a valuable practical experience. When evaluting the source code of Discord Bot, I learned lots of technologies of system design. Although there isn't much documentation about the code, I can easily find the code location of the feature using original bot command.

## Overall experience (Zubair)
From this project, I learned how to go about understanding large codebases to be able to contribute in a meaningful way. Working with an established project taught me how to integrate new features while maintaining existing code standards and patterns.

## Overall experience (Oscar)
I learned how annoying it can be when things don't work (ARM emulation) and that some codebases can be daunting to get into. I spent a lot of time looking at a different way to do this task, but at the end concluded that I didn't really understand the code we would've to work with good enough. It was also good to practice working in a team.

## Overall experience (Anton)
There were two parts of this whole experience that was interesting. First working as a team and discussing what to do beforehand was very new for me. Im very used to "aiming and shooting" with my work. But a more measured and discussion driven aproach has given me some experience in how to express myself to my peers and ill be taking it with me for future work. It was also very fun working with a bunch of new elements, the testing wasnt much new since it was simailar to what I did in the last labb but it was nice to get some practice. The interesting part mainly was learning and seeing how i was supposed to integrate my work into the already formed structure. All the api calls the bot that the discord bot is based on and most of all the whole "cog" structure was very interestnig. Its interesting to reflect on how my experience was so different from the last asignment where we simply refactored. Actually contributing is a completley different experience.


### How did you grow as a team, using the Essence standard to evaluate yourself?
According to the Essence standard, we meet all the requirements of the Performing state. However, there's some room for improvement. For instance, one requirement states 'The team continuously adapts to changing context', we found ourselves sometimes slow to adapt when facing implementation difficulties. This could have been improved with slightly better team communication. Despite these minor setbacks, we're generally satisfied with how our team functions and collaborates.

## Software Practices
Our work is well tested, relatively independent of other functions of the bot. This allows modifications to be done easier in the future as less conflicts could arise. Although this also makes the code a bit less consistent with the existing codebase, which makes it a bit less organized. We used issues to track features, collaborated when necessary, seperate branches, and full coverage testing.

### Opportunity
Our work allows users to better monitor their interests as they will be notified when decided topics are discussed.

### Stakeholders 
The people most affected are users of discord servers with the bot. Adding notifications would allow users to spend less time on browsing discussions that do no entertain them.
Requirements – I think we defined and meet our requirements reasonably well. We have a functional feature with spam filters to mitigate malicious use.

### Software System
I think the quality, maintainability, and effectiveness are all adequate for the its purpose. We used accepted practices in the development, like high test coverage and mocking API calls. Maintainability should be quite good as the system does not rely on overly many or complex other systems. As for effectiveness, it does what it’s supposed to do and we haven’t gotten it to malfunction.

### Work
We first discussed what project to do. After settling on that we each looked through the issues and agreed on one we all felt was reasonable. After that, we forked. the repo and created issues for each part required that we could identify. We added testing for our functions to ensure quality and then integrated them with each other. All throughout the project, we made sure to link commits to issues, worked on dedicated branches and asked for help if necessary. A considerable amount of time was spent on discussing our approaches.
