Download Link: https://assignmentchef.com/product/solved-comp9021-lab7
<br>






<h1>1           R Change-making problem: greedy solution</h1>

Write a program greedy_change.py that prompts the user for an amount, and outputs the minimal number of banknotes needed to yield that amount, as well as the detail of how many banknotes of each type value are used. The available banknotes have a face value which is one of $1, $2, $5, $10, $20, $50, and $100.

Here are examples of interactions:

$ python3 greedy_change.py Input the desired amount: 10

1 banknote is needed.

The detail is:

$10: 1

$ python3 greedy_change.py

Input the desired amount: 739

12 banknotes are needed The detail is:

$100: 7

$20: 1

$10: 1

$5: 1

$2: 2

$ python3 greedy_change.py

Input the desired amount: 35642

359 banknotes are needed The detail is:

$100: 356

$20: 2

$2: 1

The natural solution implements a <em>greedy </em>approach: we always look for the largest possible face value to deduct from what remains of the amount.

Suppose that the available banknotes had a face value which was one of $1, $20, and $50. For an amount of $60, the greedy algorithm would not work, as it would yield one $50 banknote and ten $1 banknotes, so eleven banknotes all together, whereas we only need three $20 banknotes.

<h1>2           Change-making problem: general solution</h1>

Write a program general_change.py that prompts the user for the face values of banknotes and their associated quantities as well as for an amount, and if possible, outputs the minimal number of banknotes needed to match that amount, as well as the detail of how many banknotes of each type value are used.

Here are examples of interactions:

$ python3 general_change.py

Input pairs of the form ’value : number’ to indicate that you have ’number’ many banknotes of face value ’value’. Input these pairs one per line, with a blank line to indicate end of input.

2 : 100

50: 100

Input the desired amount: 99

There is no solution.

$ python3 general_change.py

Input pairs of the form ’value : number’ to indicate that you have ’number’ many banknotes of face value ’value’. Input these pairs one per line, with a blank line to indicate end of input.

1 : 30

20 : 30

50 : 30

Input the desired amount: 60 There is a unique solution:

$20: 3

$ python3 general_change.py

Input pairs of the form ’value : number’ to indicate that you have ’number’ many banknotes of face value ’value’. Input these pairs one per line, with a blank line to indicate end of input.

1: 100

2: 5

3: 4

10:5

20:4

30:1

Input the desired amount: 107

There are 2 solutions:

$1: 1

$3: 2

$10: 1

$20: 3

$30: 1

$2: 2

$3: 1

$10: 1

$20: 3

$30: 1

The natural approach makes use of the linear programming technique exemplified in the computation of the Levenshtein distance between two words.

<h1>3           R The Target puzzle</h1>

The Target puzzle is a 3 <em>× </em>3 grid (the target) consisting of 9 distinct (uppercase) letters, from which it is possible to create one 9-letter word. The aim of the puzzle is to find words consisting of distinct letters all in the target, one of which has to be the letter at the centre of the target. Write a program target.py that defines a class Target with the following properties.

<ul>

 <li>To create a target object, three keyword only arguments can be provided:

  <ul>

   <li>dictionary, meant to be the file name of a dictionary storing all valid words, with a default value for a default dictionary named txt, supposed to be stored in the working directory;</li>

   <li>target, with a default value of None, otherwise meant to be a 9-letter string defining a valid target (in case it is not valid, it will be ignored and a random target will be generated as if that argument had not been provided);</li>

   <li>minimal_length, for the minimal length of words to discover, with a default value of 4. __repr__() and __str__() are implemented.</li>

  </ul></li>

 <li>It has a method number_of_solutions() to display the number of solutions for each word length for which a solution exists.</li>

 <li>It has a method give_solutions() to display all solutions for each word length for which a solution exists; this method has an argument, minimal_length, with a default value of None, that if provided allows one to display only solutions of that length or more.</li>

 <li>It has a method named change_target(), that takes two arguments, to_be_replaced and to_replace, both meant to be strings. The target will be modified if:

  <ul>

   <li>to_be_replaced and to_replace are different strings of the same length;</li>

   <li>all letters in to_be_replaced are distinct and occur in the current target;</li>

   <li>replacing each letter in to_be_replaced by the corresponding letter in to_replace yields a valid target.</li>

  </ul></li>

</ul>

If those conditions are not satisfied then the method prints out a message indicating that the target was not changed. If the target was changed but consists of the same letters, and with the same letter at the centre, then the method prints out a message indicating that the solutions are not changed.

Here is a possible interaction.

$ python3 …

&gt;&gt;&gt; from target import *

&gt;&gt;&gt; target = Target()

&gt;&gt;&gt; target

Target(dictionary = dictionary.txt, minimal_length = 4

&gt;&gt;&gt; print(target)

___________

| S | M | E |

___________

| N | G | U |

___________

| J | T | D |

___________

&gt;&gt;&gt; target.number_of_solutions()

In decreasing order of length between 9 and 4:

l solution of length 9

l solution of length 8 2 solutions of length 6

5 solutions of length 5

16 solutions of length 4 &gt;&gt;&gt; target.give_solutions(5) Solution of length 9:

JUDGMENTS

Solution of length 8: JUDGMENT

Solutions of length 6:

JUDGES

SMUDGE

Solutions of length 5:

GENUS

GUEST

JUDGE

NUDGE

STUNG

&gt;&gt;&gt; target.change_target(’MT’, ’TT’) The target was not changed.

&gt;&gt;&gt; target.change_target(’JUDGMENTS’, ’ABCDEFGHI’) The target was not changed.

&gt;&gt;&gt; target.change_target(’MT’, ’TM’) The solutions are not changed.

&gt;&gt;&gt; target.change_target(’GM’, ’MG’)

&gt;&gt;&gt; target.give_solutions() Solution of length 9:

JUDGMENTS

Solution of length 8:

JUDGMENT

Solution of length 6:

SMUDGE

Solutions of length 5:

MENDS

MENUS

MUNDT

MUSED

MUTED

Solutions of length 4:

GEMS

GUMS

MEND

MENS

MENU

METS

MUGS

MUNG

MUSE

MUST

MUTE

SMUG

SMUT

STEM

&gt;&gt;&gt; target = Target(target = ’IMRVOZATK’, minimal_length = 5)

&gt;&gt;&gt; print(target)

___________

| I | M | R |

___________

| V | O | Z |

___________

| A | T | K |

___________

&gt;&gt;&gt; target.number_of_solutions()

In decreasing order of length between 9 and 5:

l solution of length 9 2 solutions of length 6

6 solutions of length 5 &gt;&gt;&gt; target.give_solutions() Solution of length 9: MARKOVITZ

Solutions of length 6:

MARKOV

MOZART

Solutions of length 5:

KIROV

MAORI

MARIO

OZARK

RATIO

VOMIT

&gt;&gt;&gt; target.change_target(’IVAKZRMO’, ’DAFNEMRS’)

&gt;&gt;&gt; print(target)

___________

| D | R | M |

___________

| A | S | E |

___________

| F | T | N |

___________

&gt;&gt;&gt; target.give_solutions(9) Solution of length 9:

DRAFTSMEN

<h1>4                    The <em>n</em>-queens puzzle (optional, advanced)</h1>

This is a well known puzzle: place <em>n </em>chess queens on an <em>n × n </em>chessboard so that no queen is attacked by any other queen (that is, no two queens are on the same row, or on the same column, or on the same diagonal). There are numerous solutions to this puzzle that illustrate all kinds of programming techniques. You will find lots of material, lots of solutions on the web. You can of course start with the wikipedia page: <a href="https://en.wikipedia.org/wiki/Eight_queens_puzzle">http://en.wikipedia.org/wiki/Eight_queens_puzzle</a><a href="https://en.wikipedia.org/wiki/Eight_queens_puzzle">. </a>You should try and solve this puzzle in any way you like.

One set of technique consists in generating permutations of the list [0<em>,</em>1<em>,…,n − </em>1], a permutation [<em>k</em><sub>0</sub><em>,k</em><sub>1</sub><em>,…,k<sub>n−</sub></em><sub>1</sub>] requesting to place the queen of the first row in the (<em>k</em><sub>0 </sub>+ 1)-st column, the queen of the second row in the (<em>k</em><sub>1</sub>+1)-st column, etc. For instance, with <em>n </em>= 8 (the standard chessboard size), the permutation [4<em>,</em>6<em>,</em>1<em>,</em>5<em>,</em>2<em>,</em>0<em>,</em>3<em>,</em>7] gives rise to the solution:

0 0 0 0 1 0 0 0

0 0 0 0 0 0 1 0

0 1 0 0 0 0 0 0

0 0 0 0 0 1 0 0

<ul>

 <li>0 1 0 0 0 0 0</li>

 <li>0 0 0 0 0 0 0</li>

</ul>

0 0 0 1 0 0 0 0

0 0 0 0 0 0 0 1

The program cryptarithm_v1.py, written by Raymond Hettinger as part of ActiveState Code Recipes, demonstrates the use of the permutations() function from the itertools module. With cryptarithm_v2.py, we have a variant with an implementation of Heap’s algorithm to generate permutations and a technique to ’skip’ some of them. We could do the same here. For instance, starting with [0<em>,</em>1<em>,</em>2<em>,</em>3<em>,</em>4<em>,</em>5<em>,</em>6<em>,</em>7], we find out that the queen on the penultimate row is attacked by the queen on the last row, and skip all permutations of [0<em>,</em>1<em>,</em>2<em>,</em>3<em>,</em>4<em>,</em>5<em>,</em>6<em>,</em>7] that end in [6<em>,</em>7]. If you have acquired a good understanding of the description of Heap’s algorithm given in

Permutations.pdf and of cryptarithm_v2.py, then try and solve the <em>n</em>-queens puzzle generating permutations and skipping some using Heap’s algorithm; this is the solution I will provide. Doing so will bring your understanding of recursion to new levels, but it is not an easy problem, only attempt it if you want to challenge yourself…

Here is a possible interaction. It is interesting to print out the number of permutations being tested.

$ python3 …

&gt;&gt;&gt; from queen_puzzle import *

&gt;&gt;&gt; puzzle = QueenPuzzle(8)

&gt;&gt;&gt; puzzle.print_nb_of_tested_permutations()

3544

&gt;&gt;&gt; puzzle.print_nb_of_solutions()

92

&gt;&gt;&gt; puzzle.print_solution(0)

0 0 0 0 1 0 0 0

0 0 0 0 0 0 1 0

0 1 0 0 0 0 0 0

0 0 0 0 0 1 0 0

<ul>

 <li>0 1 0 0 0 0 0</li>

 <li>0 0 0 0 0 0 0</li>

</ul>

0 0 0 1 0 0 0 0

0 0 0 0 0 0 0 1

&gt;&gt;&gt; puzzle.print_solution(45)

<ul>

 <li>0 0 0 0 1 0 0</li>

 <li>0 0 0 0 0 0 0</li>

</ul>

0 0 0 0 1 0 0 0

0 1 0 0 0 0 0 0

0 0 0 0 0 0 0 1

0 0 1 0 0 0 0 0

0 0 0 0 0 0 1 0

0 0 0 1 0 0 0 0

&gt;&gt;&gt; puzzle = QueenPuzzle(11)

&gt;&gt;&gt; puzzle.print_nb_of_tested_permutations()

382112

&gt;&gt;&gt; puzzle.print_nb_of_solutions()

2680

&gt;&gt;&gt; puzzle.print_solution(1346)

0 0 0 0 0 1 0 0 0 0 0

0 0 0 0 0 0 0 1 0 0 0

0 0 1 0 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 0 0 1

0 0 0 0 0 0 1 0 0 0 0

0 1 0 0 0 0 0 0 0 0 0

<ul>

 <li>0 0 0 0 0 0 0 0 1 0</li>

 <li>0 0 0 0 0 0 0 0 0 0</li>

</ul>

0 0 0 1 0 0 0 0 0 0 0

0 0 0 0 0 0 0 0 1 0 0

0 0 0 0 1 0 0 0 0 0 0

<h1>5                    Random walk (optional)</h1>

Write a program random_walk.py that creates the picture of a random walk for a default of 50,001 points, starting from the point (0<em>,</em>0) and randomly choosing at every step to move horizontally and vertically by at most 4 units, west or east and north or south, respectively—it is allowed to move only horizontally or only vertically, but not to stay in place. The picture is drawn thanks to the matplotlib.pyplot module, which it is convenient to import as plt.

<ul>

 <li>The picture is 5 inches wide and 3 inches high—check out figure(), passing as argument the system’s resolution (in dots per inch) for best results.</li>

 <li>Check out scatter():

  <ul>

   <li>we want the points to be printed out with a size of 1 point<sup>2</sup>, with no edges, and use the cm.Blues colormap, the first points being the lightest, the last points being the darkest, which we obtain by letting the colour of the (<em>i </em>+ 1)<sup>st </sup>point be determined by <em>i </em>itself;</li>

   <li>we want to print out the first point in green, the last point in red, with a size of 10 point<sup>2</sup>, with no edges.</li>

  </ul></li>

 <li>We do not want to display axis lines and labels—check out axis().</li>

</ul>

To display the figure, check out plt.show(). Here is one possible such picture: