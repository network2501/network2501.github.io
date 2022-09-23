+++ 
date = "2022-09-22 T00:00:00Z" 
draft = true 
title = "Textual Memory Game" 
slug = "Textual Memory Game" 
tags = ['textual', 'game', 'python']
+++

# Creating a memory game with Textual

Beacuse TUIs are cool and high frequency word practice needs to be encouraged. 

## The Game

Match words, for each word matched get a point. 

### Game Elements

Player name - personalise the experience  
Score - Add some basic arithmatic into the mix  
Ascii images - reinforced words with pictures (if possible). Depending on the word set this could even be an ascii story illustration.   

### The look

Top header will have two sections that hold details like Player name, and score. Next to it will be the ascii art section for animated sprites. 
The main body will consist of a square or rectangle grid of cards that will be "face down" and when selected show the word.   

The main body has the option of grid and auto grid in textual. 

```
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  ┌────────────┐  ┌─────────────────────────────────────────┐ │
  │  │Player Name │  │                                         │ │
  │  │            │  │                                         │ │
  │  │Score       │  │ ◄──────────── ascii images   ─────────► │ │
  │  │            │  │                                         │ │
  │  │            │  │                                         │ │
  │  └────────────┘  └─────────────────────────────────────────┘ │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ └────────────┘ └────────────┘ └────────────┘ └────────────┘  │
  │                                                              │
  │ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ └────────────┘ └────────────┘ └────────────┘ └────────────┘  │
  │                                                              │
  │ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ └────────────┘ └────────────┘ └────────────┘ └────────────┘  │
  │                                                              │
  │ ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌────────────┐  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ │            │ │            │ │            │ │            │  │
  │ └────────────┘ └────────────┘ └────────────┘ └────────────┘  │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
  ```
  
  ## Movements

### Questions
Where does the selection start?

### Movement Stuff/Codebits
`on_key` to match on a key being pressed  
`event.key` to evaluate the key being pressed so i can match on ← ↑	→	↓ and then perfrom the desired action 

### Selection
Enter/spacebar or mouse left click
