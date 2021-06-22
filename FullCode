"""
Clone of 2048 game.
"""

import poc_2048_gui
import random

# Directions, DO NOT MODIFY
UP = 1
DOWN = 2a
LEFT = 3
RIGHT = 4

# Offsets for computing tile indices in each direction.
# DO NOT MODIFY this dictionary.
OFFSETS = {UP: (1, 0),
           DOWN: (-1, 0),
           LEFT: (0, 1),
           RIGHT: (0, -1)}

def merge(line):
    """
    Helper function that merges a single row or column in 2048
    """
    
    idx = 0
    idx_2 = 0
    num_2 = 0
    result_list = [0]*len(line)
    final_result = [0]*len(result_list)
    
    
    for num in range(len(line)):
        if line[num] != 0:
            result_list[idx] = line[num]
            idx += 1
            
    for dummy_num in range(len(result_list)):
    #dummy_num is just for looping i used num for indexing
        if num_2+1 <= len(result_list)-1 :
            if result_list[num_2] == result_list[num_2+1]:
                final_result[idx_2] = result_list[num_2] + result_list[num_2+1]
                final_result[idx_2+1] = 0
                idx_2 += 1
                num_2 +=2

            else:
                final_result[idx_2] = result_list[num_2]
                idx_2+=1
                num_2+=1
                
        elif num_2 == len(result_list)-1:
            final_result[idx_2] = result_list[num_2]
       
            
    return final_result

class TwentyFortyEight:
    """
    Class to run the game logic.
    """

    def __init__(self, grid_height, grid_width):
        self._cells = []
        self._height = grid_height
        self._width = grid_width
        self.reset()
        up_list = []
        for multi in range(self._width):
            up_list.append((0, multi))
            
        down_list = []
        for multi in range(self._width):
            down_list.append((self._height-1, multi)) 
            
        right_list = []
        for multi in range(self._height):
            right_list.append((multi, self._width-1))
            
        left_list = []
        for multi in range(self._height):
            left_list.append((multi, 0))
            
        self._initial_tiles = {UP:up_list,
                              DOWN:down_list,
                              LEFT:left_list,
                              RIGHT:right_list}
        
                              

    def reset(self):
        """
        Reset the game so the grid is empty except for two
        initial tiles.
        """
        self._cells = [[0 for dummy_col in range(self._width)] for dummy_row in range(self._height)]
        self.new_tile()
        self.new_tile()
        #self.__str__()
    def __str__(self):
        """
        Return a string representation of the grid for debugging.
        """
        #print "the grid is like: "
        #for prnt_idx in range(len(self.cells)):
        return str(self._cells)
 

    def get_grid_height(self):
        """
        Get the height of the board.
        """
        return self._height

    def get_grid_width(self):
        """
        Get the width of the board.
        """
        return self._width

    def move(self, direction):
        """
        Move all tiles in the given direction and add
        a new tile if any tiles moved.
        """
        
        if direction == UP or direction == DOWN:
            has_moved = False
            for init_tile in self._initial_tiles[direction]:
                temp = []
                for mult in range(self._height):
                    cell_idx = (OFFSETS[direction][0]*mult+init_tile[0], init_tile[1])
                    #temp.append(cell_idx)
                    cell_val = self.get_tile(cell_idx[0],cell_idx[1])
                    temp.append(cell_val)
                final_list = merge(temp)
                for mult_2 in range(self._height):
                    cell_idx = (OFFSETS[direction][0]*mult_2+init_tile[0], init_tile[1])
                    self.set_tile(cell_idx[0], cell_idx[1], final_list[mult_2])       
                    if final_list != temp:
                        has_moved = True
            if has_moved:        
                self.new_tile()
                #print "temp is" + str(temp)
                #print "after" + str(x)
                               
        elif direction == RIGHT or direction == LEFT:
            has_moved = False
            for init_tile in self._initial_tiles[direction]:
                temp = []
                for mult in range(self._width):
                    cell_idx = (init_tile[0], OFFSETS[direction][1]*mult+init_tile[1])
                    #temp.append(cell_idx)
                    cell_val = self.get_tile(cell_idx[0],cell_idx[1])
                    temp.append(cell_val)
                final_list = merge(temp)
                for mult_2 in range(self._width):
                    cell_idx = (init_tile[0], OFFSETS[direction][1]*mult_2+init_tile[1])
                    self.set_tile(cell_idx[0], cell_idx[1], final_list[mult_2])
                    if final_list != temp:
                        has_moved = True
            if has_moved:            
                self.new_tile()                    
                #print "temp is" + str(temp)
                #print "after" + str(x)               
                
                
    def new_tile(self):
        """
        Create a new tile in a randomly selected empty
        square.  The tile should be 2 90% of the time and
        4 10% of the time.
        """
        number_of_zeros = 0
        zero_cells = []
        _initial_values = 9*[2] + [4]
        for col in range(self._width):
            for row in range(self._height):
                if self._cells[row][col] == 0:
                    number_of_zeros +=1
                    zero_cells.append((row, col))
                    
        if number_of_zeros >= 1:
            random_cell = random.choice(zero_cells)
            self._cells[random_cell[0]][random_cell[1]]= random.choice(_initial_values)
        else:
            pass
            
    def set_tile(self, row, col, value):
        """
        Set the tile at position row, col to have the given value.
        """
        self._cells[row][col] = value

    def get_tile(self, row, col):
        """
        Return the value of the tile at position row, col.
        """
        return self._cells[row][col]


poc_2048_gui.run_gui(TwentyFortyEight(4, 4))
