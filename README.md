# Olivers_Symbiotes
Celular Automata

Made to run on Windows this time

Like Conways Game of Life, but with symbiotic new cells :)

This makes the game of life run for longer, with cells dying off more slowly overall.

New cell rules:
- A new cell with with fewer than 3 neighbour points dies, as if by underpopulation.
- Any live new cell with more than 4 neighbour points dies, as if by overpopulation.
- Any dead cell with exactly five live neighbour points becomes a live new cell, as if by reproduction.

These cells and Conways cells can see each other and live symbiotically.

> To run game: python olivers_game_of_life.txt

Enjoy! :)
