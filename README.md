Welcome to Battleship!
In this project you will build a simplified, one-player version of the classic board game Battleship! In this version of the game, there will be a single ship hidden in a random location on a 5x5 grid. The player will have 10 guesses to try to sink the ship.

To build this game we will use our knowledge of lists, conditionals and functions in Python. When you're ready to get started, click run to continue.

Make a List
Good! Now we'll use a built-in Python function to generate our board, which we'll make into a 5 x 5 grid of all "O"s, for "ocean."

The .append function will add an item to a list. Typing

board.append(["O"] * 5)
will add five "O"s, which is the basis for creating our row. We'll do this five times to make five rows. (Since we have to do this five times, it sounds like a loop might be in order.)

Check it Twice
Great job! Now that we've built our board, let's show it off.

Throughout our game, we'll want to print the game board so that the player can see which locations they have already guessed. Regularly printing the board will also help us debug our program.

The easiest way to print the board would be to have Python display it for us using the print command. Let's give that a try and see what the results look like—is this a useful way to print our board for Battleship?

Custom Print
Now we can see the contents of our list, but clearly it would be easier to play the game if we could print the board out like a grid with each row on its own line.

We can use the fact that our board is a list of lists to help us do this. Let's set up a for loop to go through each of the elements in the outer list (each of which is a row of our board) and print them.

While we're cleaning up our print routine, let's also move it to a function. Since we'll want to print our board often, it will be handy to have a function to call. Also, printing is a self-contained task that is easily packaged as a function. To be able to print a board, the print function will need to take a board as a parameter.

Printing Pretty
We're getting pretty close to a playable board, but wouldn't it be nice to get rid of those quote marks and commas? We're storing our data as a list, but the player doesn't need to know that!

To get rid of the formatting, we're going to use another built-in Python function: .join. If we type

" ".join(row)
inside our function, we tell Python to concatenate, or string together, all the "O"s in each row, putting a space in between them.

The general syntax for .join is

separator.join(list)
We'll want to do the .joining inside our for loop, so make sure your indentation is correct. If all's well, this will print each 'O' character without the quotes or commas.

Hide...
Excellent! Now that our board is printing perfectly, we need to hide a battleship on it. Since we are making a 1-player game, we'll use Python to choose a random location on the board for the battleship.

Since we have a 2-dimensional list, we'll need two numbers to identify a single location on the board: one number to specify the row and another to specify the column. Let's call our variables ship_row and ship_col.

In order to use random numbers, we will need to use the Python module called random. In this lesson we are going to only want integers, so we will use the randint function from the random module. We've imported this function at the top of the document.

randint(x, y) will generate a random integer between x and y. What should we use for x and y? We'll want to make sure the index that we generate puts the battleship in a location that is on the board!

...and Seek!
Good job! For now, let's store coordinates for the ship in the variables ship_row and ship_col. Now you have a hidden battleship in your ocean! Let's write the code to allow the player to guess where it is.

Just like we needed both a row and a column to determine the position to hide the ship, we'll need to ask the player to enter both a row and column guess. Let's call these variables guess_col and guess_row.

Use the raw_input command to ask the user to enter their guesses for row and column.

raw_input asks the user for input and returns it as a string. But we're going to want to use integers for our guesses! To do this, we'll wrap the raw_inputs with int() to convert the string to an integer. (Note that if you enter something other than a number, it will cause an error!)


It's Not Cheating—It's Debugging!
Awesome! Now we have a hidden battleship and a guess from our player. In the next few steps, we'll check the user's guess to see if they are correct.

While we're writing and debugging this part of the program, it will be helpful to know where that battleship is hidden. Let's add a print statement that displays the location of the hidden ship.

Of course, we'll remove this output when we're finished debugging since if we left it in, our game wouldn't be very challenging. :)

You win!
Okay—now for the fun! We have the actual location of the ship and the player's guess so we can check to see if the player guessed right.

For a guess to be right, guess_col should be equal to ship_col and guess_row should be equal to ship_row.

In this step, we'll write an if statement that checks to see if the player has correctly guessed the location of the ship. If they did, we will print the message "Congratulations! You sank my battleship!"

Danger, Will Robinson!!
Great! Of course, the player isn't going to guess right all the time, so we also need to handle the case where the guess is wrong.

When the player guesses wrong we'll do two things:

Print a message saying "You missed my battleship!"
To help the player keep track of which locations they have already guessed, we'll change that element in the list to an "X".
Because Python turns the numerical guesses into strings via raw_input, you'll want to use the built-in int() function to change the guesses to numbers, like so:
board[int(guess_row)][int(guess_col)] = "X"


Bad Aim
Great job! Now we can handle both correct and incorrect guesses from the user. But now let’s think a little bit more about the "miss" condition. There are lots of ways that the user can guess wrong:

They can enter a guess that's off the board
They can guess a spot they’ve already guessed
They can just miss the ship
So, let’s expand our else condition to add some helpful feedback based on each of these possibilities. We'll do this with a new if block nested under the else of our existing if block (since all of these cases will occur when the user guesses incorrectly).

First, let’s add the case where the spot the user guesses is off the board. What x and y values are illegal? Let’s build an if statement and print out "Oops, that's not even in the ocean."

Notice that you'll have to add another else for the code that is already there.

Not Again!
Great! Now let's handle the second type of incorrect guess: the player guesses a location that was already guessed. How will we know that a location was previously guessed?

It should have an 'X' instead of an 'O' if our code is working correctly.

Play It, Sam
You can successfully make one guess in Battleship! But we’d like our game to allow the player to make up to 4 guesses before they lose.

We can use a for loop to iterate through our turns just like we used it to iterate through our list. We use the same syntax, but instead of specifying a list to iterate through, we give a range. Then our loop will execute all the commands inside it that number of times.

We can use a for loop just like this to run our program 4 times for 4 turns. Let’s use the variable turn instead of i and have a range of 4. To help us see what is going on, let’s print out the value of turn each time through the loop (remember that turn will start at 0, but most human players will want their turns to start with number 1, so we’ll actually want to print turn+1.)

Make sure you are careful only to put the code that should repeat (guessing and checking the guess) inside the loop. Put the code that should only execute once (hiding the ship) outside the loop.

Game Over
If someone runs out of guesses without winning right now, the game just exits. It would be nice to let them know why. Let’s print a "Game Over" message letting the player know that they are out of turns. Since we only want this message to display if the user guesses wrong on their last turn, we need to think carefully about where to put it.
1. We’ll want to put it under the else that accounts for misses
2. We’ll want to print the message no matter what the cause of the miss
3. We’ll need to add a check to see if the user is out of guesses. Since our turn variable starts at 0 and goes to 3, it'll have value 3 on the last guess.

A Real Win
Almost there! We can play Battleship!, but you’ll notice that when you win, if you haven’t already guessed 4 times, the program asks you to enter another guess. What we’d rather have happen is for the program to end—it’s no fun guessing if you know you’ve already sunk the Battleship!

We can use the command break to get out of a for loop.