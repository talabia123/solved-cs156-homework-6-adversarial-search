Download Link: https://assignmentchef.com/product/solved-cs156-homework-6-adversarial-search
<br>
The objective of this homework assignment is to understand and visualize how an Adversarial Search algorithm works. Specifically, we will implement and compare the performance of Adversarial search algorithm for three different policies:

<ol>

 <li>Random</li>

 <li>Minimax</li>

 <li>Alpha Beta Pruning</li>

</ol>

We will explore these algorithms in the context of Tic Tac Toe gaming environment where the game will start with a N x N table. You (Agent) will select a square in the table and that will show up as a cross. Opponent will have the next turn and she will have the next move. Her move will show up as a circle. You keep playing with the opponent until either you win or the opponent or it ends up in a draw.

These are the following files for this assignment:




<ol>

 <li>py: is the main program that implements the tictactoe game with the user interface. It is invoked using: tictactoe.py depth search_algorithm size where</li>

</ol>




(depth=’3′, search=’minimax’, size=’3′)




Depth is the size N of the N x N Tic Tac Toe board

Search_algorithm can be one of “rand”, “mimimax” or “alphabeta”




Example:  run tictactoe.py 4 rand 3




<ol start="2">

 <li>py: this is where the adversarial search policies will be implemented. You have to implement:

  <ol>

   <li>mimimax</li>

   <li>alphabeta</li>

  </ol></li>

</ol>




Here is the skeleton of the code for your assignment:

“””

Adversarial search algorithms implementation

Your task for homework 5 is to implement:

<ol>

 <li>minimax</li>

 <li>alphabeta</li>

 <li>abdl (alpha beta depth limited)</li>

</ol>

“””

<strong>import</strong> random

<strong>import</strong> sys

<strong>def</strong> <strong>rand</strong>(game_state):

“””

Generate a random move.

:param game_state: GameState object

:return:  a tuple representing the row column of the random move

“””

done = False

<strong>while</strong> <strong>not</strong> done:

row = random.randint(0, game_state.size – 1)

col = random.randint(0, game_state.size – 1)

<strong>if</strong> game_state.available(row,col):

done = True

<strong>return</strong> row, col







<strong>def</strong> <strong>minimax</strong>(game_state):

“””

Find the best move for our AI agent by applying the minimax algorithm

(searching the entire tree from the current game state)

:param game_state: GameState object

:return:  a tuple representing the row column of the best move

“””

<strong>#Enter your code here</strong>




<strong>def</strong> <strong>value</strong>(game_state, player):

“””

Calculate the minimax value for any state under the given agent’s control

:param game_state: GameState object – state may be terminal or non-terminal

:param player: (string) ‘user’ or ‘AI’ – AI is max

:return: (integer) value of that state -1, 0 or 1

“””

<strong>if</strong> game_state.is_win(‘AI’):

<strong>return</strong> 1

<strong>if</strong> game_state.is_win(‘user’):

<strong>return</strong> -1

<strong>if</strong> game_state.is_tie():

<strong>return</strong> 0

# If the agent is MAX return max-value

<strong>if</strong> player <strong>is</strong> ‘AI’:

<strong>return</strong> max_value(game_state)

# If the agent is MIN return min-value

<strong>return</strong> min_value(game_state)







<strong>def</strong> <strong>max_value</strong>(game_state):

“””

Calculate the minimax value for a non-terminal state under Max’s

control (AI agent)

:param game_state: non-terminal GameState object

:return: (integer) value of that state -1, 0 or 1

“””

v = -sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v1 = value(game_state.successor(move, ‘AI’), ‘user’) # not good

tup = [v, v1]

# print(“TUP”, tup)

v = max(tup)

# print(‘MAX: ‘, v)

<strong>return</strong> v




<strong>def</strong> <strong>min_value</strong>(game_state):

“””

Calculate the minimax value for a non-terminal state under Min’s

control (user)

:param game_state: non-terminal GameState object

:return: (integer) value of that state -1, 0 or 1

“””

# Enter your code here and remove the pass statement below

v = sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v1 = value(game_state.successor(move, ‘user’), ‘AI’) # little gud

tup = [v, v1]

# print(“TUP”, tup)

v = min(tup)

# print(‘MIN: ‘, v)

<strong>return</strong> v







<strong>def</strong> <strong>alphabeta</strong>(game_state):

“””

Find the best move for our AI agent by applying the minimax algorithm

with alpha beta pruning.

:param game_state: GameState object

:return:  a tuple representing the row column of the best move

“””

# Enter your code here and remove the raise statement below

<strong>#Enter your code here#</strong>




<strong>def</strong> <strong>ab_value</strong>(game_state, player, alpha, beta):

“””

Calculate the minimax value for any state under the given agent’s control

using alpha beta pruning

:param game_state: GameState object – state may be terminal or non-terminal

:param player: (string) ‘user’ or ‘AI’ – AI is max

:return: (integer) value of that state -1, 0 or 1

“””

# Enter your code here and remove the pass statement below

<strong>if</strong> game_state.is_win(‘AI’):

<strong>return</strong> 1

<strong>if</strong> game_state.is_win(‘user’):

<strong>return</strong> -1

<strong>if</strong> game_state.is_tie():

<strong>return</strong> 0

# If the agent is MAX return max-value

<strong>if</strong> player <strong>is</strong> ‘AI’:

<strong>return</strong> abmax_value(game_state, alpha, beta)

# If the agent is MIN return min-value

<strong>return</strong> abmin_value(game_state, alpha, beta)







<strong>def</strong> <strong>abmax_value</strong>(game_state, alpha, beta):

“””

Calculate the minimax value for a non-terminal state under Max’s

control (AI agent) using alpha beta pruning

:param game_state: non-terminal GameState object

:return: (integer) value of that state -1, 0 or 1

“””

# Enter your code here and remove the pass statement below

a = alpha

v = -sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v = max([v, ab_value(game_state.successor(move, ‘AI’), ‘user’, a, beta)])

<strong>if</strong> v &gt;= beta:

<strong>return</strong> v

a = max(a, v)

<strong>return</strong> v







<strong>def</strong> <strong>abmin_value</strong>(game_state, alpha, beta):

“””

Calculate the minimax value for a non-terminal state under Min’s

control (user) using alpha beta pruning

:param game_state: non-terminal GameState object

:return: (integer) value of that state -1, 0 or 1

“””

# Enter your code here and remove the pass statement below

b = beta

v = sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v = min([v, ab_value(game_state.successor(move, ‘user’), ‘AI’, alpha, b)])

<strong>if</strong> v &lt;= alpha:

<strong>return</strong> v

b = min([b, v])

<strong>return</strong> v







<strong>def</strong> <strong>abdl</strong>(game_state, depth):

“””

Find the best move for our AI agent by limiting the alpha beta search to

the given depth and using the evaluation function game_state.eval()

:param game_state: GameState object

:return:  a tuple representing the row column of the best move

“””

# Enter your code here and remove the raise statement below

<strong>#Enter your code here#</strong>







<strong>def</strong> <strong>abdl_value</strong>(game_state, player, alpha, beta, depth):

“””

Calculate the utility for any state under the given agent’s control

using depth limited alpha beta pruning and the evaluation

function game_state.eval()

:param game_state: GameState object – state may be terminal or non-terminal

:param player: (string) ‘user’ or ‘AI’ – AI is max

:return: (integer) utility of that state

“””

# Enter your code here and remove the pass statement below

<strong>if</strong> player == ‘AI’ <strong>and</strong> game_state.is_win(‘AI’):

<strong>return</strong> 1

<strong>if</strong> player == ‘user’ <strong>and</strong> game_state.is_win(‘user’):

<strong>return</strong> -1

<strong>if</strong> game_state.is_tie():

<strong>return</strong> 0

<strong>if</strong> depth == 0:

<strong>return</strong> game_state.eval()

# If the agent is MAX return max-value

<strong>if</strong> player <strong>is</strong> ‘AI’:

<strong>return</strong> abdlmax_value(game_state, alpha, beta, depth)

# If the agent is MIN return min-value

<strong>return</strong> abdlmin_value(game_state, alpha, beta, depth)







<strong>def</strong> <strong>abdlmax_value</strong>(game_state, alpha, beta, depth):

“””

Calculate the utility for a non-terminal state under Max’s control

using depth limited alpha beta pruning and the evaluation

function game_state.eval()

:param game_state: non-terminal GameState object

:return: (integer) utility (evaluation function) of that state

“””

# Enter your code here and remove the pass statement below

a = alpha

v = -sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v = max([v, abdl_value(game_state.successor(move, ‘AI’), ‘user’, a, beta, depth -1)])

<strong>if</strong> v &gt;= beta:

<strong>return</strong> v

a = max(a, v)

<strong>return</strong> v







<strong>def</strong> <strong>abdlmin_value</strong>( game_state, alpha, beta, depth):

“””

Calculate the utility for a non-terminal state under Min’s control

using depth limited alpha beta pruning and the evaluation

function game_state.eval()

:param game_state: non-terminal GameState object

:return: (integer) utility (evaluation function) of that state

“””

# Enter your code here and remove the pass statement below

b = beta

v = sys.maxsize

<strong>for</strong> move <strong>in</strong> game_state.possible_moves():

v = min([v, abdl_value(game_state.successor(move, ‘user’), ‘AI’, alpha, b, depth -1 )])

<strong>if</strong> v &lt;= alpha:

<strong>return</strong> v

b = min([b, v])

<strong>return</strong> v










<strong><u>Summarize your observations in terms of:</u></strong>

Total Number of nodes expanded for

<ol>

 <li>Minimax</li>

 <li>Alphabeta</li>

</ol>

<strong><u>Results: </u></strong>

When run for N = 3 and depth 3

<ol>

 <li>Minimax: 2,556</li>

 <li>Alphabeta: 558</li>

</ol>

we can see a significant improvement in terms of the number of nodes that were expanded.




<table width="623">

 <tbody>

  <tr>

   <td width="156"><strong> </strong></td>

   <td width="155"><strong> </strong></td>

   <td width="156"><strong> </strong></td>

   <td width="156"><strong> </strong></td>

  </tr>

 </tbody>

</table>




<strong><u>Bonus points for:</u></strong>

<ol>

 <li>Any other insights from running your code on different values of N and depth.</li>

</ol>

When run for N = 5 and depth 3

<ol>

 <li>Minimax: 696,339</li>

 <li>Alphabeta: 43,388</li>

</ol>

As we increase the dimensions and the depth, the program seems to slow down significantly to the point where it takes several minutes to explore all possible moves. Therefore, I kept the depth constant at 3 to decrease the number of nodes needed to be explored and expanded.







<ol start="2">

 <li>Implementing Alphabeta with limited depth</li>

</ol>