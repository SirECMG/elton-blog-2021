---
layout: post
title:  "Tips on Problem Solving"
author: "Elton Murillo"
date:   2026-11-06 01:08:00 +0800
tags: [ competitive-programming ]
---


# Strategies for Problem Solving

The following tips are a reminder to myself for a framework for better tackling problems solving (with a focus on coding problems), but can be applied to general problems.


## Never go straight into coding

It never ends up well. From past experience either you get stuck or get more confused or you don't end up solvin the problem and need to ask for help or look up the solution.

## Understand the problem

What is the problem asking? Before reading anything try to identify and locate what it is asking and maybe galnce at the output and input.

## Read the paragraph and take notes on important details

## Try to identify the constraints (this can help you solve the problem and prevent bugs)

This probably the most important and most likely where bugs are introduced. We will need to practice the skill of finding the constrainst and invariants and possibly using asserts in our code to help prevent bugs.

## Explain Every Aspect in English

1. Input
2. Output
3. What potential problem you will need to solve
4. How can you transform the input or introduce state to derive the output.
5. the constraints and invariances

## Try to solve the problem in Plain English (and all the subproblems) before any coding

This will provide clarity and help identify key pieces like if you need to introduce data structures to help solve the problem.


## Try to come up with a todo list

To make things easier to code and focused. Identifiy where you are mutating or transforming to make debugging easier



# Notes from "Thinking like a Programer"


## problem solving

definition: writing an original program that performs a particular set of tasks and meets all stated constraints.



## constriants

- a problem has unbreakable rules in which the problem must be solved.



## expert problem solvers

- expert problem solvers are quick to recognize an analogy, an exploitable similarity between a solved problem and an unsolved problem.
    - If we recognize that a feature of a problem A is analogous to a feature of problem B, we have already solvbed Problem B, we have a valuable insight into solving problem A.


# tips:

- if you are unaware of all possible actions you could take, you may be unable to solve the problem.
    - we refer to these actions as operations
    - by enumerating all possible operations, we can solve many problems by testing every combination of operations until we find one that works.
    - by restating th eproblem in more formal terms, we can often uncover solutions that would have otherwise eluded us.


- list constraints
    - farmer can take only one item at a time in the boat.
    - fox and goose cannot be left alone on the same shore
    - goose and corn cannot be left alone on the same shore.

- list operations
    - make a specific list of actions we think we can take


- the goal of formally restating the problem is to gain insight for a solution.
- unless we have already solved the problem and discovered the "hidden" possible operation, taking the goose back to the near side of the river, we're not going to discover it in making our list of actions.
- instead, we should try to make operations generic, or parameterized.

- by thinking about the problem in the most general terms, this second list of operations will allow us to solve the problem without the need for an "ah-hah!" moment regarding the trip back to the near shore with the goose.

- if we generate all possible sequences of moves, ending each sequence once it violates one of our constraints or reaches a configuration we've seen before, we will eventually hit upon the solution and solve the puzzle.
- inherent difficulty of the puzzle will have been sidestepped through the formal restatement of constraints and operations.


# Restating the problem in a more formal manner is a great technique for gaining insight into a problem.

- thinking about the problem may be as productive or in some cases more productrive, than thinking about the solution. In many cases, the correct approach to the solution is the solution.

# In solving programming problems, we are sometimes faced with a situations where we can't see a clear path to code the solution, but we must never allow this to be an excuse to forgo planning and systematic approaches. It's better to develop a strategy than to attack the problem through trial and error.


# We should look for the most constrained part of the problem. While constraints are often what makes a problem difficult to begin with, they may also simplify our thinking about the solution because they eliminate choices.


# Importance of recognizing analogies

## general problem-solving techniques

### Always Have a Plan

### Restate the Problem

### Divide the Problem

### Start with What you Know

### Reduce the Problem

### Look for Analogies

### Experiement

### Don't Get Frustrated

### Exercises



## The Fox, the Goose, and the Corn

Problem: How to cross the river?

A farmer with a fox, a goose and a sack of corn needs to cross a river. The farmer has a rowboat, but there is room for only the farmer and one of his three items. Unfortunately, both the fox and the goose are hungry. The fox cannot be left alone with the goose, or the fox will eat the goose. Likewise, the goose cannot be left alone with the sack of corn, or the goose will eat the corn. How does the farmer get everything across the river?


Trying to Solve It:

Actors: 
Farmer
Fox
Goose
Sack

Fox can't be with Goose
Goose can't be with the corn
Farmer only can accomodate 1

which item can be left alone?
Fox and Corn

take goose over


pass 1.

C & F         G

farmer comes back

pass 2.

goose is on other side and again fox and corn be left alone with each other so bring corn over

take back goose


F             C
G

pass 3.

take fox to corn. and come back for goose

G              C & F


pass 4.

                C & F & G



