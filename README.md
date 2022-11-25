# Sim

Here is a brief description of the modules I introduced and their responsibilities :

- SimController is responsible for building the different elements necessary to start a specific session of the game : the board, the player, the interaction controller and finally the logic to which it passes all the elements so that the game can start.

- The SimGameLogic is the brain of the game, it knows the rules of the game and acts as the conductor.

- Human/AI classes both contain player specific info like the hover/click colors as well as the current list of selected line segments by the player.
Note : specifically the AI class has a dependency on the MinMaxLineSegmentSelector and the ClickableLineSegmentClicker modules to determine which line segment to select.

- BoardGame that contains the board specific information : the polygon line segments it is made of and the remaining clickable line segments

- BoardGameBuilder is the base allowing the creation of the polygon line segments (Edge and Diagonal) that define the game board.

- OctagonBuilder inherits from BoardGameBuilder

- BoardGameDrawer is the class responsible for drawing the BoardGame anywhere we want in the world

- The LineSegment represents a segment connecting two points in space.

- The PolygonLineSegment represents a line segment connecting two vertices of a polygon. 

- Edge and Diagonal extend from PolygonLineSegment and allow defining whether the polygon line segment is an edge or a diagonal.
Note : I made a distinction between LineSegment/PolygonLineSegment since only the latter is either an edge or a diagonal. 
LineSegment does not know in which context it is used.

- ClickableLineSegment represents a clickable line segment (one that had been drawn in the world)

- BoardGameInteractionController allows to specify which player should be authorized to interact with the board.

- ClickableLineSegmentInteractionHandler is listening to pointer inputs and colorizing the associated clickable line segment.

- The MinMaxLineSegmentSelector looks at the board current state and uses minimax (without alpha/beta pruning ) to determine the best next move.
Note: it destroys each created tree node as soon as utility values have been sent back to their parent node so that we don't keep too much game state in memory.

- The ClickableLineSegmentClicker performs a click on a clickable line segment.
