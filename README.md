# Couch Game Simulation

A simulation of the infamous "drinking" (not strictly necessary) **couch game**. Thanks to my good friend Sabreena for introducing this game to me!

## Overview

- The simulation will consist of $n$ bots, where $2 | n, n > 8$. $n$ is a parameter specified by the user.
- Each bot $b_i$:
  - has a team number $T$, where $T = i \space \text{mod} \space 2$
  - has two unique (among bots) properties: a real index $i$ and a fake index $j$.
  - has a map of fake indices to real indices, which
    - starts out as empty, but is added to by every move
    - has a retention rate $r_i$ where $0 \leq r_i \leq 1$. If a new entry needs to be added to the table (due to a move) which would make its size exceed $r_i \times (n - 1)$, old entries will be evicted by LRU policy.
- A field configuration is an ordered list of length $n + 1$ integers, representing "seats". Each seat in this list represents a real index if it is occupied, or $-1$ if it is unoccupied. Seats $0$ to $3$ represent the "couch". Only **one** seat can be unoccupied.
  - The initial configuration will always be an in-order list of all $n$ players, with the $n$th inde being $-1$ (i.e. unoccupied).
- A move made by a bot $b_i$ represents a single number $x$ that represents the fake index "called out" by the bot whose turn it currently is. $x \neq j_i$.

## Bot strategy

- Each bot uses the alphabeta strategy to determine its next move
- Each bot has a depth $D_i$ for determining its most strategic move
- Each bot has a drunkenness factor $d_i$ where $0 \leq d_i \leq 1$. Every time the bot's strategy involves evaluating a fellow bot's team number, there is a $d_i$ chance that this result is wrong
- Each configuration of players on the field is assigned a value via the $\text{score}$ function. See below for the implementation.

## $\text{score(Configuration)}$ function

## Order of play

### Init

- Simulation runner inputs a valid value $n$.
- Configuration is created:

$$
[0, 1, 2, ..., n-1, -1]
$$

- $n$ bots are initialized
