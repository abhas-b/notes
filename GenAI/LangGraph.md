#genai 


# Type Annotations

## TypeDict
* Normal dictionaries have a few problems: They don't check whether the data is the correct type or structure. This becomes a problem in larger projects.
* Instead, we'll use Typed Dictionary

```
from typing import TypedDict

class Movie(TypedDict):
	name:str
	year:int
	
movie = Movie(name="Avengers", year=2019)
```

* These are type safe.
* Type Annotations are used to define states in LangGraph.


## Union

```
from typing import Union

def square(x: Union[int, float]) -> float:
	return x*x
```

## Optional

```
from typing import Optional

def nice_message(name: Optional[str]) -> None:
	if name is None:
		print("Hey random person")
	else:
		print("Hi {name}")
```

## Any

```
from typing import Any

def print_value(x: Any):
	print(x)
```

# Elements

## State

* Its a shared data structure that holds the current information or context of the entire application.
* Its like the application's memory, keeping track of application's variables and data which can be used by the nodes (both access and modify).

## Nodes
* Individual operations or functions for performing specific tasks within the graph.
* Each node receives the current state, processes it and produces an output. 
* The graph itself represents the workflow in which the nodes are inter-connected. The workflow has sequential steps, as well as conditional steps between various operations. 

## Edges
* Connections between the nodes determining flow of execution.
* They tell us which node should be executed next after the current one completes its task.


## Start
* Start node is where the workflow begins.
* It doesnt have any operations, rather serves as starting position for graph's execution.

## End
* End point of the graph.


## Tools
* Specialized functions or utilities that nodes can utilize to perform specific tasks such as fetching data from an API.
* These provide additional functionalities to the nodes.
* Technically these are part of nodes itself.


## ToolNode
* Special kind of a node whose job is to run a tool.
* Brings tool output into the State for other nodes to leverage it.


## StateGraph
* A class in LangGraph used to build and compile the graph structure.
* Manages the nodes, edges, and overall state ensuring that the workflow operates in a unified way and that data flows correctly between components.


## Runnable

* A standardized executable component that performs a specific task within an AI workflow.
* Allows us to create modular systems.
* It can represent various operations. On the other hand a node has to receive a State and updates the state.


## Messages

* Human Message: Represents input from a user
* System Message: provides instructions or context to the model
* Function Message: represents results of a function call
* AI Message: represents responses by a model call
* Tool Message: function messages specific to tool use
