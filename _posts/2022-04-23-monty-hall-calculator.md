---
title:  "Monty Hall Problem"
mathjax: true
layout: post
categories: media
date:   2022-04-23
---

# Monty Hall problem

<img class = "marginauto" src="/assets/img/2022/04/2022-04-23-monty-hall/monty_hall_cover.jpeg" width = "400" height = "400"> 

<br>

Hey there. In a few seconds, you will learn how to maximize your win rate in TV shows games.
Have you ever heard about "Monty Hall Problem"?

### 1. What is Monty Hall

<img class = "marginauto" src="/assets/img/2022/04/2022-04-23-monty-hall/monty_hall_photo.jpeg" width = "400" height = "400"> 
<br>

In the 70's the TV game show "Let's make a Deal" was a big success. In this show the genious host Monty Hall played some games with the audience givin then the opportunity to win a lot o cash or other goodies.
One of these games were a incredible "probability" problem that is studied until today, and in this post you will learn a good strategy to "win" this game. Lets see

### 2. The doors problem

<img class = "marginauto" src="/assets/img/2022/04/2022-04-23-monty-hall/monty_hall_doors.jpeg" width = "400" height = "400"> 
<br>

Imagine that you must choose between 3 doors.
In one of them, you have a *big money prize*. The two others have *only a goat*.
The steps are simple:

>You select one of the doors

>The host opens one of the last doors showing you only a goat

>He asks you: Do you want to change the chosen door?

>After the question que opens the door you chosen

### 3. The strategy to win

Maybe you are thinking: Regardless of what choose the probability will still be 1/3! I prefer to continue with my lucky number.
Or even: Is there a way to increase my chances of winning?

Now the spoiler: 
>The good side is that you can double your chances o winning.
>The bad side is that the explanation isn't intuitive

Come with me, I will try to explain why "change the door" is always the best choice:

>You have 1/3 of the chances to choose the right door or, in other words, 2/3 to choose the wrong door.

>If you stay with your decision, you continue with 1/3 of the chances to win. If you change your door, your chances rise to 2/3 because of the intervention of the announcer.

>The secret of this estrategy is because the announcer will always open a bad one because *HE KNOWS WHERE THE MONEY PRIZE IS*

### 4. Graphical demonstration

Okay, I know you are confused now (As I was when I read about that for the first time).
I will try to help you with a "Graphical ilustration"

The example: 

>The money prize is on the last door (Door number 3)

| Door choosen | Change | Result |
|:--:          |:--:    |:--:    |
| 1            | Y      | W      |
| 1            | N      | L      |
| 2            | Y      | W      |
| 2            | N      | L      |
| 3            | Y      | L      |
| 3            | N      | W      |

>You have 1/3 of chances to choose the right door at first.
>>In this case if you change the door you lose.

>You have 2/3 of chances to choose the wrong door at first.
>>In this case if you change the door you win.

>If you always assume that you will choose the wrong door at first you will double your chances to win.

### 5. Simulator in python

To show you how this is a "winner strategy" I've written a script in Python to simulates this.
>Please, feel free to use this code if you want.

First we will import some libraries used in this script and create a function to "turn" things easier.

```python
# Calling used libraries
from random import sample # To sample results
import numpy # To do the if_else statement

## Now let's create a function to help us making this test multiple times
def MontyHall():

    global result, prize, door_choosen

    # Creating a list with the number of possible options
    list_of_doors = [1, 2, 3]
    print(list_of_doors)

    # Testing the sample function
    #print(sample(list_of_doors,1))

    # Assignment of the prize
    prize = int(sample(list_of_doors,1)[0])
    print(prize)

    # Choose the door
    door_choosen = int(sample(list_of_doors,1)[0])
    print(door_choosen)
    
    # Checking if is better to change the door or not
    result = numpy.where(door_choosen == prize, "Dont_change", "Change")
    return(result)
```

Now let's test the scenarios:

```python

# Set the number of tries you want to test
number_of_tries = 10

# Count the number of times change the door = win the prize
change_is_win = 0

while True:
    try:
        option = int(input("Press 1 to see all runs or 0 to skip"))
        option in [1,2]
    except ValueError:
        print("Your input is out of parameters")
        continue
    else:
        break    

for i in range(number_of_tries):
    
    MontyHall()

    # Count number of times changing the door let you win
    count = numpy.where(result == 'Change', 1, 0)
    change_is_win = int(change_is_win) + int(count)

    if option == 1 :
        print("Test number " + str(i + 1))
        print("Prize: " + str(prize))
        print("Door Choosen: " + str(door_choosen))
        print("This time you must: " + str(result))

        # Chances of win changing the door
        print("Change door chances: " + str(int(change_is_win) / int(i + 1)))

# Chances of win changing the door
final_chances = str(int(change_is_win) / int(i + 1))
print("Change door chances: " + str(final_chances))
```

Now see the results:

**Test number 1**
> Prize is on door 1

> You choose the door 3
>> If you change you win

<br>

**Test number 2**
> Prize is on door 3

> You choose the door 3
>> If you change you lose

<br>

**Test number 3**
> Prize is on door 1

> You choose the door 3
>> If you change you win

<br>

**Test number 4**
> Prize is on door 2

> You choose the door 1
>> If you change you win

<br>

**Test number 5**
> Prize is on door 2

> You choose the door 2
>> If you change you lose

<br>

**Test number 6**
> Prize is on door 3

> You choose the door 2
>> If you change you win

<br>

**Test number 7**
> Prize is on door 3

> You choose the door 3
>> If you change you lose

<br>

**Test number 8**
> Prize is on door 3

> You choose the door 2
>> If you change you win

<br>

**Test number 9**
> Prize is on door 3

> You choose the door 1
>> If you change you win

<br>

**Test number 10**
> Prize is on door 2

> You choose the door 1
>> If you change you win

<br>

**Chances to win changing the door**
> 10 tests

> 7 times you win if you change
>> 7/10 = 70% of win rate 