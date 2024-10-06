### Lecture 0 Search
- Artificial Intelligence
	- Search
	- Knowledge
	- Uncertainty
	- Optimization
	- Learning
	- Neural Networks
	- Language
- Search Problems
	- **agent** *entity that perceives its environment and acts upon that environment*
	- **state** *a configuration of the agent and its environment*
		- **initial state** *the state in which the agent begins*
	- **actions** *choices that can be made in a state% description of what state results from performing any applicable action in any state
		- `result(s, a)` returns the state resulting from performing action `a` in state `x`
	- **state space** *the set of all states reachable from the initial state by any sequence of actions*
	- **goal test** *way to determine whether a given state is a goal state*
	- **path cost** *numerical cost associated with a given path*
	- **search problems**
		- initial state
		- actions
		- transition model
		- goal test
		- path cost function
	- **solution** *a sequence of actions that leads from the initial state to a goal state*
		- **optimal solution** a solution that has the lowest path cost among all solutions
- Solving Search Problems 
	- **Data Structure : node** *a data structure that keeps track of*
		- a state
		- a parent (node that generated this node)
		- an action (action applied to parent to get node)
		- a path cost (from initial state to node)
	- **Approach**
		- Start with a frontier that contains the initial state.
		- Repeat
			- If the frontier is empty, then no solution.
			- Remove a node from the frontier.
			- If the node contains goal state, return the solution.
			- Expand the node, add resulting nodes to the frontier.
	- **Revised Approach**
		- Start with a frontier that contains the initial state.
		- Start with an empty explored set.
		- Repeat
			- If the frontier is empty, then no solution.
			- Remove a node from the frontier.
			- If the node contains goal state, return the solution.
			- Add the node to the explored set.
			- Expand the node, add resulting nodes to the frontier if they aren't already in the frontier or the explored set.
- **Uninformed Search** *search strategy that uses no problem-specific knowledge*
	- Depth-First Search
		- **stack** *last-in first-out data type*
		- **depth-first search** *search algorithm that always expands the deepest node in the frontier*
	- Breadth-First Search
		- **queue** *first-in first-out data type*
		- **breadth-first search** *search algorithm that always expands the shallowest node in the frontier*
- **Informed search** *search strategy that uses problem-specific knowledge to find solutions more efficiently*
	- **Greedy Best-First Search**  *search algorithm that expands the node that is closest to the goal, as **estimated** by a heuristic function `h(n)`*
	- **A* search*** *search algorithm that expands node with lowest value of `g(n) + h(n)*
		- `g(n)` cost to reach node
		- `h(n)` estimated cost to goal
		- optimal if
			- `h(n)` is admissible (never overestimates the true cost)
			- `h(n)` is consistent (for every node `n` and successor `n'` with step cost `c`,  $h(n) \le h(n') + c$ )
- **Adversarial Search**
	- **Minimax** 
		- `max(x)` aims to maximize score.
		- `min(o)` aims to minimize score.
		- **Game**
			- `S_0` *initial state*
			- `PLAYER(s)` returns which player to move in state `s`
			- `ACTIONS(s)` returns legal moves in state `s`
			- `RESULT(s, a)` returns state after action `a` taken in state `s`
			- `TERMINAL(s)` checks if state `s` is a terminal state
			- `UTILITY(s)` final numerical value for terminal state `s`
		- **Minimax** *Minimize the possible loss for the worst-case scenario while maximizing the potential gain.*
			- Given a state `s`
				- `MAX` picks action `a` in `ACTIONS(s)` that produces the highest value of `MIN_VALUE(RESULT(s, a))`
				- `MIN` picks action `a` in `ACTIONS(s)` that produces smallest value of `MAX_VALUE(RESULT(s, a))`
		- **Alpha-Beta Pruning** *Ignore branches in the game tree that won't affect the final decision*
		- **Depth-Limited Minimax** *Restrict the search depth to manage complexity*
			- **evaluation function** function that estimates the expected utility of the game from a given state
```Python
def MAX_VALUE(state):
	if TERMINAL(state):
		return UTILITY(state)
	v = float('-inf')
	for actions in ACTIONS(state):
		v = max(v, MIN_VALUE(RESULT(state, action)))
	return v

def MIN_VALUE(state):
	if TERMINAL(state):
		return UTILITY(state):
	v = float('inf')
	for action in ACTIONS(state):
		v = min(v, MAX_VALUE(RESULT(state, action)))
	return v
```
### Lecture 1 Knowledge
- **knowledge-based agents** *agents that reason by operating on internal representations of knowledge*
- **Propositional Logic**
	- **sentence** *an assertion about the world in a knowledge representation language*
	- **Proposition Symbols**
		- $P$ 
		- $Q$ 
		- $R$ 
	- **Logical Connectives**
		- $\neg\quad$ not
		- $\wedge\quad$ and
		- $\vee\quad$ or
		- $\rightarrow\quad$ implication
		- $\leftrightarrow\quad$ biconditional
	- **model** *assignment of a truth value to every propositional symbol (a "possible world" )*
	- **knowledge base** *a set of sentences known by a knowledge-based agent*
	- **entailment** $\alpha\models\beta$ *In every model in which sentence $\alpha$ is true, sentence $\beta$ is also true*
	- **inference** *the process of deriving new sentences from old ones*
- **Inference Algorithms**
	- **Model Checking**
		- To determine if $\text{KB} \models \alpha$
			- Enumerate all possible models.
			- If in every model where $\text{KB}$ is true, $\alpha$ is true, then $\text{KB}$ entails $\alpha$.
			- Otherwise, $\text{KB}$ does not entail $\alpha$.
- **Knowledge Engineering**
	- Example: Clue
	- Example: Logic Puzzles about HP-House
	- Example: Mastermind
- **Inference Rules**
	- **Modus Ponens** $\alpha\rightarrow\beta \quad \& \quad \alpha \quad \implies \quad \beta$
	- **And Elimination** $\alpha\wedge\beta \quad \implies \quad \alpha$
	- **Double Negation Elimination** $\neg\left(\neg\alpha\right) \quad \implies \quad \alpha$
	- **Implication Elimination** $\alpha\rightarrow\beta \quad \implies \quad \neg\alpha\vee\beta$
	- **Biconditional Elimination** $\alpha\leftrightarrow\beta \quad \implies \quad \left(\alpha\rightarrow\beta\right)\wedge\left(\beta\rightarrow\alpha\right)$
	- **De Morgan's Law**
		- $\neg\left(\alpha\wedge\beta\right) \quad \implies \quad \neg\alpha\vee\neg\beta$
		- $\neg\left(\alpha\vee\beta\right) \quad \implies \quad \neg\alpha\wedge\neg\beta$
	- **Distributive Property**
		- $\left(\alpha\wedge\left(\beta\vee\gamma\right)\right) \quad \implies \quad \left(\alpha\wedge\beta\right)\vee\left(\alpha\wedge\gamma\right)$
		- $\left(\alpha\vee\left(\beta\wedge\gamma\right)\right) \quad \implies \quad \left(\alpha\vee\beta\right)\wedge\left(\alpha\vee\gamma\right)$
	- **Theorem Proving**
		- initial state: starting knowledge base
		- actions: inference rules
		- transition model: new knowledge base after inference
		- goal test: check statement we're trying to prove
		- path cost function: number of steps in proof
	- **clause** *a disjunction of literals*
	- **conjunctive normal form** *logical sentence that is a conjunction of clauses*
	- **Conversion to CNF**
		- Eliminate biconditionals
			- Turn $\left(\alpha\leftrightarrow\beta\right)$ into $\left(\alpha\rightarrow\beta\right)\wedge\left(\beta\rightarrow\alpha\right)$
		- Eliminate implications
			- Turn $\alpha\rightarrow\beta$ into $\neg\alpha\vee\beta$
		- Move $\neg$ inwards using De Morgan's Laws
		- Use distributive law to distribute $\vee$ wherever possible
- **Inference by Resolution**
	- To determine if $\text{KB}\models\alpha$
		- Convert $\left(\text{KB}\wedge\neg\alpha\right)$ to Conjunctive Normal Form.
		- Keep checking to see if we can use resolution to produce a new clause. 
			- If ever we produce the empty clause (equivalent to False), we have a contradiction, and $\text{KB}\models\alpha$
			- Otherwise, if we can't add new clauses, no entailment.
- **First-Order Logic**
	- Constant Symbol & Predicate Symbol
	- Universal Quantification & Existential Quantification