import os
import time
import random

import os

from colorama import Fore, Back, Style
from copy import copy, deepcopy

'''
    Oliver Symbiotes, a celular automata in the vein of Conways game of life
    Dedicated to John Conway.
    Copyright (C) 2021 Adam Oliver
    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.
    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
'''

global num
num = 80
hei = 22
wid = 80


print('#')
print(Fore.RED + '%', end='') #
#print(Fore.LIGHTGREEN + '%') #
print(Fore.YELLOW + '*') #
print(Fore.GREEN + '&') #
print(Fore.BLUE + '$') #
#quit()

global grid
global grid2
grid = [[0 for i in range(wid)] for j in range(hei)] # 80 20 
grid2 = [[0 for i in range(wid)] for j in range(hei)] # 80 20 

# set all grid[x][y] to 6

county = 0
count = 0
for i in grid:
  for j in i:
    grid[county][count] = '0'
    
    count += 1
  count = 0 
  county += 1
# done




# prints the grid2
def print_grid():

  grid2 = grid
  #grid2 = deepcopy(grid)

  count = 0
  for i in grid2:
    for e in i:

      if(e=='1'):print('#', end='' ) # end='' removes newline
      if(e=='a'):print('%', end='' ) # 
      if(e=='3'):print('*', end='' ) # 
      if(e=='4'):print('&', end='' ) # 
      if(e=='5'):print('$', end='' ) # 
      if(e=='0'):print(' ', end='' ) # 

      if(e=='7'):print( 'i', end='' ) # 

      if(e=='10'):print('a', end='' ) # 
      if(e=='11'):print( 'b', end='' ) # 
      if(e=='12'):print( 'c', end='' ) # 
      if(e=='13'):print( 'd', end='' ) # 

      if(e=='14'):print( 'a', end='' ) # 
      if(e=='15'):print( 'b', end='' ) # 
      if(e=='16'):print( 'c', end='' ) # 
      if(e=='17'):print( 'd', end='' ) # 
      
      count += 1
      if(count == wid): print(''); count = 0

#
#grid[6][9] = '3'
#
print_grid()


###
# this just adds a step
#
def add_cell():

  print('')
  print('')
  
  # change range(1) to change number of new characters
  
  for i in range(3):

    # adds a '#'
    # finds a random place in the grid, adds a cell
    #print(random.randint(1,6))
    x = random.randint(0,hei-1)
    y = random.randint(0,wid-1)

    if( grid[x][y] != 0 ):
      grid[x][y] = '1' #str(random.randint(1,4))
    
    # adds a '%'
    x = random.randint(0,hei-1)
    y = random.randint(0,wid-1)

    if( grid[x][y] != 0 ):
      grid[x][y] = 'a' #str(random.randint(1,4))

# this just stops list index out of range error
def numberz_h(thenum):

  thenum=int(thenum)

  if(thenum >= wid):
    return wid - 1
  else:
    return thenum
    
def numberz(thenum):

  thenum=int(thenum)

  #print('[')
  #print('hei thenum')
  #print(hei)
  #print(thenum)

  if(thenum >= hei):
    return hei - 1
  else:
    return thenum


def a_to_0(anum): # try it with 1
  if(anum == 'a'):
    return 1
  else:
    return anum
  
def a_to_2(anum):
  if(anum == 'a'):
    return 2
  else:
    return anum

def a_step():  

  global grid
  grid2 = deepcopy(grid)

  # grid loop
  count = 0
  for i in grid:
    county = 0
    for j in i:
      #pass

      #print('Hello')
      #print(j)
      #time.sleep(1)

      total = 0


      #introduce seperate symiotic species :) (%)
      
      total = int(a_to_2( grid[numberz(count-1)][numberz_h(county-1)] )) + int(a_to_2( grid[numberz(count)][numberz_h(county-1)] )) + int(a_to_2( grid[numberz(count+1)][numberz_h(county-1)] )) + int(a_to_2( grid[numberz(count+1)][numberz_h(county)] )) + int(a_to_2( grid[numberz(count-1)][numberz_h(county)] ))  + int(a_to_2( grid[numberz(count-1)][numberz_h(county+1)] )) + int(a_to_2( grid[numberz(count)][numberz_h(county+1)] )) + int(a_to_2( grid[numberz(count+1)][numberz_h(county+1)] ))

      # a new cell now counts as 2

      #a new cell with with fewer than 3 neighbour points dies, as if by underpopulation.
      if( j == 'a' and ( total < 3 ) ): #
        grid2[count][county] = '0' #'10' # up
      #Any live new cell with more than 4 neighbour points dies, as if by overpopulation.
      if( j == 'a' and ( total > 4 ) ): #
        grid2[count][county] = '0' #'10' # up
      #Any dead cell with exactly five live neighbour points becomes a live new cell, as if by reproduction.
      if( j == '0' and ( total == 5 ) ): #
        grid2[count][county] = 'a' #'10' # up
      

      # conways species (#)

      #total += int(grid[count-1][county-1]) +int(grid[count][county-1]) +int(grid[count+1][county-1]) +int(grid[count+1][county]) +int(grid[count-1][county]) +int(grid[count-1][county+1]) +int(grid[count][county+1]) +int(grid[count+1][county+1])

      total = 0

      total = int(a_to_0( grid[numberz(count-1)][numberz_h(county-1)] )) + int(a_to_0( grid[numberz(count)][numberz_h(county-1)] )) + int(a_to_0( grid[numberz(count+1)][numberz_h(county-1)] )) + int(a_to_0( grid[numberz(count+1)][numberz_h(county)] )) + int(a_to_0( grid[numberz(count-1)][numberz_h(county)] ))  + int(a_to_0( grid[numberz(count-1)][numberz_h(county+1)] )) + int(a_to_0( grid[numberz(count)][numberz_h(county+1)] )) + int(a_to_0( grid[numberz(count+1)][numberz_h(county+1)] ))

      #print(total)
      
      # Any live cell with fewer than two live neighbours dies, as if by underpopulation.
      if( j == '1' and ( total < 2 ) ): #
        grid2[count][county] = '0' #'10' # up
      #Any live cell with two or three live neighbours lives on to the next generation.
      #if( j == '1' and ( total == 2 or total == 3 ) ): #
        #grid2[count][county] = '1' #'10' # up
      pass
      #Any live cell with more than three live neighbours dies, as if by overpopulation.
      if( j == '1' and ( total > 3 ) ): #
        grid2[count][county] = '0' #'10' # up
      #Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.
      if( j == '0' and ( total == 3 ) ): #
        grid2[count][county] = '1' #'10' # up
      

      county += 1
      
    count += 1

  grid = deepcopy(grid2)

#call a number of times to populate grid!
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()
add_cell()

while True:

  # clear the screen
  clear = lambda: os.system('cls')
  clear()

  a_step()

  print_grid()

  print('')
  
  time.sleep(.2)#0.1

quit()





