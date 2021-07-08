# Questions - Dynamic Programming
- Setup/
- Subproblem
- Base cases
- Recursion
- How to obtain the final solution - How to obtain the final solution should really just be a call to your recursive function with the initial values provided (e.g. call opt(n) for the final solution)
  - Recuse and memoize OR build DP table bottom up
  - Relate subproblem solutions
- Time complexity
  - number of subproblems * (average cost of solving each subproblem)

## Tutorial Problems

1. You are traveling by a canoe down a river and there are $n$ trading posts along the way. Before starting your journey, you are given for each $1 \le i \lt j \le n$ the fee $F(i, j)$ for renting a canoe from post $i$ to post $j$. These fees are arbitrary. For example it is possible that $F(1, 3) = 10$ and $F(1, 4) = 5$​. You begin at trading post 1 and must end at trading post $n$ (using rented canoes). Your goal is to design an efficient algorithms which produces the sequence of trading posts where you change your canoe which minimises the total rental cost.

   > Subproblem: For each $i^{th}$​ post, we need to find the minimal total rental cost starting at post 1 to post $i$​​.
   >
   > Recursion: The optimal solution $opt(i)$ for the $i^{th}$ post can be defined with the following recurrence relation:
   > $$
   > opt(i) = \min_{1 \le j \lt i}\{opt(j) + F(i,j)\}
   > $$
   > Base Case: The base case of the recurrence solution occurs when $opt(1) = F(1,1) = 0$​.​​
   >
   > Obtaining the Final Solution:
   >
   > To obtain the final solution, create an array of size $n$​. Each element in the array stores these two values:
   >
   > - the actual minimal total renting cost to reach to the $i^{th}$ post, $opt(i)$, and
   > - the index on where the previous post is that gives us the optimal solution, $prev(i) = \arg \min_{1 \le j \le i}\{opt(j) + F(i,j)\}$
   >
   > Find the final solution through a bottom up approach. Loop through each $i^{th}$​​ post, find optimal solution that gives the minimal total rental costs to reach post $i$​ and save $opt(i)$ and $prev(i)$ in the array. We are solving the subproblems in the order of $opt(1), opt(2), ... opt(n)$​​​​​​​​.
   >
   > To find the sequence of trading posts, we can backtrack to find the previous post that gives us the optimal solution which gives us the sequence in reverse order. We can simply find this through looking up the index on where the previous post is at through the results stored in the array.
   >
   > Time Complexity: The overall time complexity is $O(n^2)$​ since for each of the $n$​ subproblems, we are computing $O(n)$​ problems to find $\min_{1 \le j \le i}\{opt(j) + F(i,j)\}$​.

2. You are given a set of $n$ types of rectangular boxes, where the $i^{th}$ box has height $h_i$ , width $w_i$ and depth $d_i$​ . You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.

   > Setup: For each box, there are 6 rotations we can make as part of the stack. Hence, if we consider each rotation as a separate box, then there are $6n$ box in total. To find a stack of boxes which is possible, we can use dynamic programming to consider all possibilities and take the most optimal solution. However, to do this, we need to have an ordering of such boxes. Let us sort the boxes in an ordering such that each box is ordered in increasing order based on the surface area.
   >
   > Subproblem: The subproblem then becomes for the $i^{th}$​ box in the sorted ordering of boxes, how many boxes would it take to create the tallest stack where the $i^{th}$ box is in the top of the stack.
   >
   > Recursion: Let $opt(i)$​ be the optimal solution to find the tallest stack if box $i$​​ is on top. To solve the subproblem, we can use the following recurrence relation defined:
   > $$
   > opt(i) = \max\{opt(j) + h_i\} \text{ where $1 \le j \lt i$ and  $w_j \gt w_i$ and $d_j \gt d_i$}
   > $$
   > Base Case: The base case for the recurrence relation occurs when $opt(1) = h_1$.
   >
   > Obtaining the Final Solution:
   >
   > Let there be an array of size $n$​. Use the recurrence relation in a bottom up approach. Loop through each box $i$​ and find the maximal height $opt(i)$​ when box $i$​ is atop the stack. Store the computation in the array at index $i$​ so that we can reuse the result in later recursion calls. Hence, solve the subproblems in the order of $opt(1), opt(2), ... opt(n)$​​ and our final solution is the maximum from $\max_{1 \le i \le 6n} opt(i)$​​. We can simply find this by finding the maximum value in the array.
   >
   > Time Complexity: The overall time complexity of this algorithm is $O(n^2)$​ as since we are solving $6n$​ subproblems, for each subproblem, it takes $O(n)$​ to find the best stack of boxes previous to the $i^{th}$​ box to have the tallest stack. 

3. TODO: You have an amount of money $M$ and you are in a candy store. There are $n$​ kinds of candies and for each candy you know how much pleasure you get by eating it, which is a number between 1 and 100, as well as the price of each candy. Your task is to chose which candies you are going to buy to maximise the total pleasure you will get by gobbling them all.

   > Setup: This problem can be represented as a knapsack problem where $M$​ is the knapsack. For each $i^{th}$ candy, denote $c_i$ be the total cost and $v_i$ the pleasure gained.
   >
   > Subproblem: The subproblem can be defined as which candies are going to maximise the total pleasure if you have the total amount of money equal to $i$​​. 
   >
   > Recursion: Let $P(i)$​​​ denote the optimal solution where it gives the total pleasure you will gain if you only have the total money equalling to $i$. We can define the recurrence relation as follows:
   > $$
   > P(i) = \max_{1 \le j \lt n}\{P(i - w_j) + v_j\}
   > $$
   >
   > Base Case: Let the base case for our optimal solution be $P(1) = v_1$ and $P(j) = 0$ where $j \le 0$​​​.
   >
   > Obtaining the Final Solution: Construct an $M \times n$ matrix. We build a table for each knapsack of capacities of $i \le C$ and cache the results in the table to be reused in later computations. 
   >
   > Time Complexity: For each $M$ subproblems, we are computing $n$ operations to find the maximum pleasure gained. Thus, the complexity if $O(Mn)$.
   >
   > 

4. Consider a 2-D map with a horizontal river passing through its centre. There are $n$ cities on the southern bank with x-coordinates $a_1 . . . a_n$ and $n$ cities on the northern bank with x-coordinates $b_1 . . . b_n$. You want to connect as many north-south pairs of cities as possible, with bridges such that no two bridges cross. When connecting cities, you are only allowed to connect the the $i^{th}$ city on the northern bank to the $i^{th}$​ city on the southern bank.

   > Setup: Sort the cities in the northern and southern bank by the x-coordinates in increasing order.
   >
   > Subproblem: If there are $i$ cities, what is the maximum pairs of cities to connect by bridge such that no two bridge cross with the condition that the $i^{th}$​ cities has a bridge connecting the two cities.
   >
   > Recursion: Let $M(i)$ be defined as a function which returns the optimal solution which gives the maximum bridge connections with $i$ cities. For each $i^{th}$ city, let $p_i$ denote the connection between $a_i$ and $b_i$. The recurrence relation can be modelled as:
   > $$
   > M(i) =\max_{1\le j \lt i}\{M(i-j) + p_i\} \text{ only where $p_{i-j}$ does not intersect with $p_i$}
   > $$
   > Base Case: The base case of $M(i)$ occurs when $M(1) = p_1$​.​
   >
   > Obtaining the Final Solution: Construct an $M \times n$ matrix​​ where for each cell store these two values:
   >
   > - the maximum connection of bridges that can be made, and
   > - the predecessor activity $j$ that gives us the optimal solution (as a way to backtrack to find the sequence of bridges.)
   >
   > Find the argument that can be found using the following definition:
   > $$
   > \pi(i) = \arg\max_{1\le j \lt i}\{M(i-j) + p_i\} \text{ only where $p_{i-j}$ does not intersect with $p_i$}
   > $$
   > For each $n$​​​ subproblem, compute the optimal solution where we are only considering $i$​​ cities and cache the results in the array so that it can be used in later computations. Finding the optimal solution just requires finding the maximum element with the maximum connection of bridges in the matrix and using the predecessor value to backtrack and find the sequence of bridges.

5. You are given a boolean expression consisting of a string of the symbols $true$ and $false$ and with exactly one operation $and$, $or$, $xor$ between any two consecutive truth values. Count the number of ways to place brackets in the expression such that it will evaluate to $true$. For example, there is only 1 way to place parentheses in the expression $true$ and $false$ xor $true$ such that it evaluates to $true$​.

   > 

6. A company is organising a party for its employees. The organisers of the party want it to be a fun party, and so have assigned a fun rating to every employee. The employees are organised into a strict hierarchy, i.e. a tree rooted at the president. There is one restriction, though, on the guest list to the party: an employee and their immediate supervisor (parent in the tree) cannot both attend the party (because that would be no fun at all). Give an algorithm that makes a guest list for the party that maximises the sum of the fun ratings of the guests.

   >Subproblem: For employee $i$ in the tree, find a guest list that gives that maximises the fun rating where employee $i$ is rooted at the tree. We must consider two options, whether employee $i$ would be included in the guest list which maximises the fun rating. For each $i^{th}$ employee, lets $f(i)$ define the number of fun received if the employee is going to the party.
   >
   >Recursion: Lets define a function $E(i)$​ given a subtree where employee $i$ is rooted at the top, it finds the guest lists that maximises the fun rating if employee $i$ is included in that list. Lets define another function $N(i)$ similar to $E(i)$ but instead, it finds the optimal guest list where employee $i$​ is NOT included.
   >$$
   >E(i) = \sum_{1 \le j \le n}E(j) + f(i) \text{ where $n$ is the strict child of employee $i$ in the tree}
   >$$
   >$$
   >N(i) = \sum_{1 \le j \le n}\max\{E(j), N(j)\} \text{ where $n$ is the strict child of employee $i$ in the tree}
   >$$
   >
   >For these recurrence functions, we are looping through each strict child of employee $i$​​ and finding the maximum child node that gives us the maximum fun through the recursive calls. We are calling the opposite recursive calls (i.e $N(i) \rightarrow E(j), $​​ $E(i) \rightarrow N(j)$​​ ) as this ensures an employee and their immediate supervisor does not attend the party. Lets define a function $M(i)$​​ which returns the guess list which gives maximise the fun rating if employee $i$​​ is the root node. The function is defined as:
   >$$
   >M(e_{president}) = \max\{E(e_{president}),N(e_{president})\}
   >$$
   >
   >
   >Base Case: The base case of the recurrence occurs when the employee that is rooted in the subtree is the leaf node in the tree. This gives us  $E(j) = f(j)$​​​ and $I(j) = 0$ where $j$ would be the employees that are the leaf node in the subtree.​​
   >
   >Obtaining the final solution: Find the optimal solution if the president was rooted at the root employee and apply the function call $M$​​​​ to find the guest list that gives the maximum fun rating. We can find the guess list by redefining our function $E$​ and $N$​​​ such that it gives back the argument value which produces the optimal solution.
   >
   >Time Complexity: This algorithm runs overall in $O(n)$​ as for we are linearly going through each employee.
   
7. TODO: You have $n_1$​ items of size $s_1$​ and $n_2$​ items of size $s_2$​. You would like to pack all of these items into bins, each of capacity $C$​​, using as few bins as possible.

   > Subproblem: We define as subproblem $P(i,j)$ to find the minimal capacity of packing $i$ items of size $s_1$ and $j$ items of size $s_2$​ where $i \le s_1$ and $j \le s_2$.
   >
   > Recursion: Assume that $s_1 \le s_2$. When finding the how much items can we pack items of size $s_1$, let $I= floor(C / s_1)$. This takes up many items of $s_1$ to fill a bin with capacity $C$.

8. You are given $n$ activities and for each activity $i$ you are given its starting time $s_i$ , its finishing time $f_i$ and the profit $p_i$ which you get if you schedule this activity. Only one activity can take place at any time. Your task is to design an algorithm which produces a subset $S$ of those $n$ activities so that no two activities in $S$ overlap and such that the sum of profits of all activities in $S$​​ is maximised.

   > Setup: Sort the activities by finishing time in increasing order.
   >
   > Subproblem: Define the subproblem as what is the maximum sum of profits for the subset of activities where activity $i$ is included.
   >
   > Recursion: Lets define a function called $P(i)$ where it gives us the optimal solution. We can define the function as follows:
   > $$
   > P(i) = p_i + \max_{1 \le j \lt i}\{P(j)\} \text{ for only actvity $j$ where $f_j \le s_i$}
   > $$
   > In the recurrence relation, we are including the profits made from activity $i$ and also the maximum activity sequence where it does not overlap with $s_i$.
   >
   > Base Case: The base case for the recurrence relation occurs when $P(1) = p_1$​.
   >
   > Obtaining the Final Solution: This problem can be modelled similar to the increasing sequence problem. Construct an array of size $n$ where each element $i$ stores:
   >
   > - the total profits made if activity $i$ is included in the subset
   > - the argument value $j$​ that gives $\max_{1 \le j \lt i}\{P(j)\}$​ when finding the optimal solution $P(i)$
   >
   > Solve the $n$ subproblems and for each each activity $i$, find the optimal solution $P(i)$​​​ and store the final results in the array. We can now find the highest sum of profits by performing a linear search on the array to determine which element contains the highest total profits. From there, we can utilise the argument value $j$ and backtrack to that predecessor each time to find the sequence of jobs that gives us the optimal solution.
   >
   > Time Complexity: The time complexity of this algorithm is $O(n^2)$.

9. Your shipping company has just received $N$ shipping requests (jobs). For each request $i$, you know it will require $t_i$ trucks to complete, paying you $d_i$ dollars. You have $T$​ trucks in total. Out of these $N$ jobs you can take as many as you would like, as long as no more than $T$​​ trucks are used in total. Devise an efficient algorithm to select jobs which will bring you the largest possible amount of money.

   > The problem can be represented as the knapsack problem.

10. Again your shipping company has just received $N$ shipping requests (jobs). This time, for each request $i$, you know it will require $e_i$ employees and $t_i$ trucks to complete, paying you $d_i$ dollars. You have $E$ employees and $T$ trucks in total. Out of these $N$ jobs you can take as many of them as you would like, as long as no more than $E$ employees and $T$​​ trucks are used in total. Devise an efficient algorithm to select jobs which will bring you the largest possible amount of money.

    > 
    
11. Because of the recent droughts, $n$ proposals have been made to dam the Murray Darling river. The $i^{th}$ proposal asks to place a dam $x_i$ meters from the head of the river (i.e., from the source of the river) and requires that there is not another dam within $r_i$ metres (upstream or downstream). What is the largest number of dams that can be built? You may assume that $x_i < x_{i+1}$.

    >Subproblem: We define the subproblem such that what is the largest number of dams where the $i^{th}$ proposal would be built as well.
    >
    >Recursion: Let $L(i)$​ be the optimal solution in finding the largest number of dams where the $i^{th}$ proposal is build as well. We can define the recursive function as follows:
    >$$
    >L(i) = 1 + \max\{L(j): 1 \le j \lt i \text{ and } x_i - x_j \gt \max(r_i, r_j)\}
    >$$
    >Base Case: Our base case occurs when $L(1) = 1$
    >
    >Obtaining the Final solution: Construct an array of size $n$ where each element stores the largest number of dams including the $i^{th}$ proposal. Solve for each $n$ problems and populate the array such that we cache the results for future computations and know what is the largest number of dams that can be built including the $i^{th}$ proposal. After solving the $n$ subproblems, we can simply perform a linear search to determine the highest element in the array which is the largest number of dams that can be built.
    >
    >Time Complexity: The algorithm runs in $O(n^2)$ as for each $n$​ subproblems, the average costs in solving the subproblem is $O(n)$ due to finding the largest number of dams that can be built.

12. You are given an $n \times n$ chessboard with an integer in each of its $n^2$​ squares. You start from the top left corner of the board; at each move you can go either to the square immediately below or to the square immediately to the right of the square you are at the moment; you can never move diagonally. The goal is to reach the right bottom corner so that the sum of integers at all squares visited is minimal. 

    a) Describe a greedy algorithm which attempts to find such a minimal sum path and show by an example that such a greedy algorithm might fail to find such a minimal sum path.

    > 

    b) Describe an algorithm which always correctly finds a minimal sum path and runs in time $n^2$. 

    c) Describe an algorithm which computes the number of such minimal paths. 

    d) (Very Tricky!) Assume now that such a chessboard is stored in a read only memory. Describe an algorithm which always correctly finds a minimal sum path and runs in linear space (i.e., amount of read/write memory used is $O(n)$) and in time $O(n^2)$​.

13. A palindrome is a sequence of letters which reads equally from left to right and from right to left. Given a sequence of letters, find efficiently its longest subsequence (not necessarily contiguous) which is a palindrome. Thus, we are looking for a longest palindrome which can be obtained by crossing out some of the letters of the initial sequence without permuting the remaining letters.

    > Subproblem: The subproblem can be defined as what is the longest palindrome starting from letter $i$ to letter $j$.
    >
    > Recursion and Base Case: Let $P(i,j)$​ denote as the recurrence relation to solve the subproblem in finding the longest palindrome between letter $i$ and $j$​​. Let the recursion be defined as:
    > $$
    > P(i,j)
    > =
    > \begin{cases}
    >   1 & \text{if $i = j$} \\
    >   2 & \text{if $i + 1 = j$} \\
    >   P(i + 1, j - 1) + 2 & \text{if $i = j$ and $j - i \gt 2$} \\
    >   \max\{P(i + 1, j), P(i, j - 1)\} & \text{else}
    > \end{cases}
    > $$
    >
    > Obtaining the Final solution: We can solve the final solution by in a top-down approach by calling $P(1, n)$ where $n$ is the last letter in the sequence which gives us the longest length of the palindrome.
    >
    > Time Complexity: The time complexity is given by $O(n^2)$ as for solving the $n$​ subproblems, each operation takes $O(n)$.

    

14. A partition of a number $n$ is a sequence $<p_1, p_2, . . . , p_t>$ (we call the $p_k$ parts) such that $1 \le p_1 \le p_2 \le . . . \le p_t \le n$ and such that $p_1 + . . . + p_t = n$.

    (a) Find the number of partitions of n in which every part is smaller or equal than $k$, where $n$, $k$ are two given numbers such that $1 \le k \le n$.

    >

    (b) Find the total number of partitions of $n$​.

    > 

15. We say that a sequence of Roman letters $A$ occurs as a subsequence of a sequence of Roman letters $B$ if we can obtain $A$ by deleting some of the symbols of $B$. Design an algorithm which for every two sequences $A$ and $B$ gives the number of different occurrences of $A$ in $B$, i.e., the number of ways one can delete some of the symbols of $B$ to get $A$​. For example, the sequence ba has three occurrences in the sequence baba: baba, baba, baba.

    > Subproblem: Let $T(i,j)$ gives us the number of occurrence of $A[1..i]$ in $B[1..j]$​. We can define the subproblem to be how many occurrences of the first $i^{th}$ letters of $A$ are in the first $j$ letters of $B$.
    >
    > Recursion: We can define the recursion as follows:
    > $$
    > T(i,j) = 
    > \begin{cases}
    > 0 & \text{if $i \gt j$} \\
    > T(i, j - 1) & \text{if $A[i] \ne B[j]$} \\
    > T(i - 1, j - 1) + T(i, j - 1) & \text{if $A[i] = B[j]$}
    > \end{cases}
    > $$
    > If $A[i] \ne B[j]$, this means that the last letter in $B$ must be deleted as it means $B[j]$ is not the last letter in the first $i^{th}$  letters of $A$. We then recursive call $T(i,j -1)$​ to find if there exists a solution without $B[j]$.
    >
    > If $A[i] = B[j]$, this means we know the the $i^{th}$ and $j^{th}$ letters are the same and we move it back to match the $i - 1$ letters to $j - 1$ letters. Hence $T(i - 1, j - 1)$. For the case of $T(i, j - 1)$​, we are finding if there exists another mapping of $A$ in $B[1..j-1]$.
    >
    > Base Case: The base case occurs when $T(1,1) = 1$ if $A[1] = B[1]$ and 0 otherwise.
    >
    > Obtaining the final solution: We can obtaining the final solution through the top-down dynamic programming approach where we simply call $T(len(A), len(B))$ to find the maximum number of ways.
    >
    > Time Complexity: Since there exists $n$ subproblems (i.e. where $1 \le i \le len(A)$ and $1 \le j \le len(B)$), each operation takes $O(n)$ to computer the maximum number of ways. Thus, this algorithm costs $(n^2)$ overall.

16. We are given a checkerboard which has 4 rows and $n$ columns, and has an integer written in each square. We are also given a set of $2n$ pebbles, and we want to place some or all of these on the checkerboard (each pebble can be placed on exactly one square) so as to maximise the sum of the integers in the squares that are covered by pebbles. There is one constraint: for a placement of pebbles to be legal, no two of them can be on horizontally or vertically adjacent squares (diagonal adjacency is fine). 

    (a) Determine the number of legal patterns that can occur in any column (in isolation, ignoring the pebbles in adjacent columns) and describe these patterns. Call two patterns compatible if they can be placed on adjacent columns to form a legal placement. Let us consider sub-problems consisting of the first k columns $1 \le k \le n$​. Each sub-problem can be assigned a type, which is the pattern occurring in the last column. 

    > 
    
    (b) Using the notions of compatibility and type, give an $O(n)$​-time algorithm for computing an optimal placement.
    
    >
    
17. Skiers go fastest with skis whose length is about their height. Your team consists of $n$​ members, with heights $h_1, h_2, . . . , h_n$​. Your team gets a delivery of $m \ge n$​ pairs of skis, with lengths $l_1, l_2, . . . , l_m$​. Your goal is to design an algorithm to assign to each skier one pair of skis to minimise the sum of the absolute differences between the height $h_i$​ of the skier and the length of the corresponding ski he got, i.e., to minimise
    $$
    \sum_{1 \le i \le n}|h_i - l_s(i)|
    $$
    where $s(i)$ is the index of the skies assigned to the skier of height $h_i$​.

    > 

18. You have to cut a wood stick into several pieces. The most affordable company, Analog Cutting Machinery (ACM), charges money according to the length of the stick being cut. Their cutting saw allows them to make only one cut at a time. It is easy to see that different cutting orders can lead to different prices. For example, consider a stick of length 10 m that has to be cut at 2, 4, and 7 m from one end. There are several choices. One can cut first at 2, then at 4, then at 7. This leads to a price of $10 + 8 + 6 = 24$ because the first stick was of 10 m, the resulting stick of 8 m, and the last one of 6 m. Another choice could cut at 4, then at 2, then at 7. This would lead to a price of $10 + 4 + 6 = 20$​, which is better for us. Your boss demands that you design an algorithm to find the minimum possible cutting cost for any given stick.

    >

19. For bit strings $X = x_1 . . . x_m, Y = y_1 . . . y_n$​ and $Z = z_1 . . . z_{m+n}$​ we say that $Z$​ is an interleaving of $X$​ and $Y$​ if it can be obtained by interleaving the bits in $X$​ and $Y$​ in a way that maintains the left-to-right order of the bits in $X$​ and $Y$​. For example if $X = 101$​ and $Y = 01$​ then $x_1x_2y_1x_3y_2 = 10011$​​ is an interleaving of $X$​ and $Y$​, whereas 11010 is not. Give an efficient algorithm to determine if $Z$​ is an interleaving of $X$​ and $Y$​.

    >  

20. Some people think that the bigger an elephant is, the smarter it is. To disprove this you want to analyse a collection of elephants and place as large a subset of elephants as possible into a sequence whose weights are increasing but their IQs are decreasing. Design an algorithm which given the weights and IQs of n elephants, will find a longest sequence of elephants such that their weights are increasing but IQs are decreasing.

    > Setup: Sort the elephants by their weights in increasing order.
    >
    > Subproblem: This problem can be modelled as an increasing subsequence problem. Define the subproblem as what it the longest subsequence for $i$ elphants.
    >
    > Recursion: Define $E(i)$ as the optimal solution where it finds the longest subsequence of elephants out of the $i$ elephant such that elephant $i$ is included. For each $i^{th}$ elephant, let $w_i$ be defined as their weight and $q_i$​​​ as their IQ. Assume that we have solve the optimal solution, our recursive solution is given:
    > $$
    > E(i) = \max\{E(j) + q_i: 1 \le j \lt i \text{ and } q_j \lt q_i\}
    > $$
    > Base Case: The base case occurs when $E(1) = q_i$​
    >
    > Time Complexity: $O(n^2)$

21. You have been handed responsibility for a business in Texas for the next $N$ days. Initially, you have $K$ illegal workers. At the beginning of each day, you may hire an illegal worker, keep the number of illegal workers the same or fire an illegal worker. At the end of each day, there will be an inspection. The inspector on the $i^{th}$ day will check that you have between $l_i$ and $r_i$ illegal workers (inclusive). If you do not, you will fail the inspection. Design an algorithm that determines the fewest number of inspections you will fail if you hire and fire illegal employees optimally.

    >

22. Given an array of $N$ positive integers, find the number of ways of splitting the array up into contiguous blocks of sum at most $K$.

    >Subproblem: We can define the subproblem as what is the maximum ways to split the array of the first $i$ elements which gives us a sum at most $K$.
    >
    >Recursion: Let $S(i)$ find the total ways to split the first $i$ elements in the given array up into contiguous blocks of sum at most $K$. We can define the recurrence relation as follows:
    >$$
    >S(i) = \sum\limits_{j = 1}^{j \le i}\{S(j): \text{sum(i,j)} \le K\}
    >$$
    >Base Case: $S(0) = 1$

23. There are $N$ levels to complete in a video game. Completing a level takes you to the next level, however each level has a secret exit that lets you skip to another level later in the game. Determine if there is a path through the game that plays exactly $K$ levels.

    >

24. Given a sequence of $n$ positive or negative integers $A_1, A_2, ...A_n$, determine a contiguous subsequence $A_i$ to $A_j$ for which the sum of elements in the subsequence is maximised.

    >

25. Consider a row of $n$​ coins of values $v_1, v_2, ...v_n$​, where $n$ is even. We play a game against an opponent by alternating turns. In each turn, a player selects either the first or last coin from the row, removes it from the row permanently, and receives the value of the coin. Determine the maximum possible amount of money we can definitely win if we move first.

    > 

