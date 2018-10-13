# Pursuit Android 5.4 Homework 01.02

## Write a text-based game

### Project overview

Write a command line tool that leads the user through a text-based adventure.

The way text-based games work usually goes something like this:

1. Program begins by printing some text that provides the user with a little context and a starting point for the adventure. Prompts user to input first move and waits for user to input text. 
2. Program accepts input text and prints more text that tells the user what happened based on their action. 
3. Repeat.

Example:

```
You wake up and find yourself in a room so dark that you can't see anything. You hear a strange noise on the other side. Do you want to investigate it? (Y or N)
> Y

You walk closer to the sound. As you approach it, you feel something drip from the ceiling on your shoulder. Keep going?
> Y

You keep walking. Suddenly the floor disappears in front of you and you fall into a pit and perish. GAME OVER!!!
```

### Requirements

This assignment is fairly open-ended, so be creative with your game ideas and have fun! However, the completed submission should include each of the following requirements:

- Accept input from the user with a `Scanner` object.
- At least one `if`/`else-if`/`else` type control structure and one `switch` statement.
- At least one `while` loop and one `for` loop.

### Additional factors

- Your game should be able to run to completion without noticeable bugs or crashes.
- Code should be organized into methods as appropriate to demonstrate good modularization and code reuse.
- All submitted code should be formatted as defined by the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html).

This is an individual assignment, so each student will be responsible for submitting their own original game.

### Some examples

- [Internet Archive: Supernova (1987)](https://archive.org/details/msdos_Supernova_1987)
- [Internet Archive: Hamurabi (1996)](https://archive.org/details/msdos_Hamurabi_1996)
- [Internet Archive: The Hobbit (1983)](https://archive.org/details/msdos_Hobbit_The_1983)
- [Internet Archive: The Treasury of Zan (1989)](https://archive.org/details/treasury-of-zan)

### Fun ideas 

- Try using some ASCII art in your prompts (there are lots of image to ASCII converters online)
- Try making a map of the area and have the user navigate through it. Maybe there are hidden surprises along the way...

Example:

```
     [ ]--[ ]
      |
[X]--[ ]--[ ]
```

- Can you make an entire story [using just emoticons](http://hexascii.com/japanese-emoticons/)?

## Homework submission

1. Create a package called CYOA_Pursuit_HW_LASTNAME_FIRSTNAME (replace `LASTNAME` and `FIRSTNAME` with your own last and first name)

2. Commit and push all work and submit your repo link using the Canvas link on the calendar by **8pm on Saturday 10/27/2018**. Submitting this assignment in on time, and to completion, is expected of all participants.
