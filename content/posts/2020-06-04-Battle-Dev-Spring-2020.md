---
title: BattleDev Spring 2020
template: "post"
date: "2020-06-04"
draft: false
category: "Dev"
tags:
  - "BattleDev"
  - "Python"
social-image: "/media/battleDev2020/icon.png"
description: "In spring, I participated to a French Competition : the `BattleDev`, but it allows anyone from an EEC country to compete. Indeed, it’s a competition that bring together  thousands of programmers from all around the world.  At this edition, we were more than 5000 participants."

---

# Presentation

In spring, I participated to a French Competition : the `BattleDev`, but it allows anyone from an EEC country to compete. 
Indeed, it’s a competition that bring together  thousands of programmers from all around the world.  At this edition, we were more than 5000 participants.
It lasts two hours, and consists of six algorithmic exercises in the langage of their choice. You must solve the first question before you can see the second question, and so on. The winner is the first person to solve the last question, then the second person to solve it, and so on for everyone who solved the last question, followed by the first person to solve the second last question, etc.

We could choose to resolve the differents exercises in :
> C++
> C#
> Java
> Php
> Ruby
> Python
> Node.js.

I managed to find the first `two` exercises and was stuck on the third one, as the majority of the others.

![Result](/media/battleDev2020/result.png)

# First Exercise

## Objective

> You are in charge of carrying out an exciting marketing study on the packaging of a new organic yoghurt issued fromshort circuits. Even if you regret to see a "responsible" brand inspired by the methods of industrial producers, this is your job and you have no choice... You receive the results of a study where consumers indicate the colour they prefer for packaging. Not wanting to make such an important decision alone, you want to present the 2preferredcolors to your boss.

## Data Format

I**nput** 

Row 1 : an integer `N` between 3 and 10000 corresponding to the number of people interviewed. 
Rows 2 to `N`+1 : a string comprising between 4and 10 lower case letters corresponding to the color preferred by a given person.

**Output**

Two strings separated by a space representingthe two colors that come out the most. The first string must be the color that is favored by the greatest number of people.
There will never be two colors with the same number of votes.

## Example

**Input**
*6*
*red*
*yellow*
*blue*
*red*
*yellow*
*red*

**Output**
*red yellow*

Because red got 3 votes, yellow two votes and blue 1 vote.

## My code :

![Code 1](/media/battleDev2020/code_1.png)

# Second Exercise

## Statement

> While walking in Las Vegas, you come across a stand with a simple game: the dealer mixes the card game (limited to cards from 1 to 9) and draws one. Before the draw, if you announced the right number, you win eight times your bet, otherwise you lose your money.

> You know that the potential gains on this type of game are very low but your friend is not of the same opinion. He's going for it! Even if you watch him play, you advise him to play the numbers that often fall consecutively (there is no real explanation for this method, but hey, it's at least a strategy). So you look at past drawsthat are displayed on ascreen above the table.

## Data Format

**Entry**
Row 1 : an integer `N` between 1 and 10000 representing the number of draws displayed in the history.
Rows 2 to `N`+1 : a digit between 1 and 9 representing the number of the card drawn.

**Output** 
A number representing the length of the largest series where a number was repeated.

## Example

**Input**
*10*
*5*
*3*
*3*
*4*
*9*
*9*
*9*
*9*
*9*
*6*

**Output**
*5*

Because the longest series where a number has been repeated is when the 9 was drawn 5 times in a row.

## My code

![Code 2](/media/battleDev2020/code_2.png)