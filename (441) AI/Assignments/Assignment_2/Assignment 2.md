# Exercise-1
**a. An agent that senses only partial information about the state cannot be perfectly rational.**

**False**. 
	Rationality refers to maximizing success based on the available information. We can measure how well the agent responds to the information it receives regardless of the quality or locality of that information. 

**b. There exist task environments in which no pure reflex agent can behave rationally**

**True**. 
	Since reflex agents don't store any information about previously experienced percepts, very dynamic environments or  partially observable ones may elicit irrational behavior from a reflex agent. 

**c. There exists a task environment in which every agent is rational.**

**True.** 
	In an environment that is static or the solution set is deterministic...(agent has no autonomy) the agent will still tend towards the most successful behavior.

**d. The input to an agent program is the same as the input to the agent function.**

**False.** 
	The agent function maps the entire set of possible percepts to some actions. The agent program implements and handles some specific percepts and actions

**e. Every agent function is implementable by some program/machine combination.**

**False.** 
	Some problems in computing may not be solved reasonably or be infinite loops.

**f.  Suppose an agent selects its action uniformly at random from the set of possible actions. There exists a deterministic task environment in which this agent is rational.**

**True.** 
	Since an action is selected from a set of possible actions, this implies that there is a mapping by the agent function from a percept to each one of these actions. Therefore, there exists an environment from which this agent received such percepts.

**h. It is possible for a given agent to be perfectly rational in two distinct task environments.** 

**True**. 
	take an imaginary environment in which the agent selects one action (action a) over the other (action b). If we adjust the conditions slightly enough that the agent will still take take the exact same sequence of actions in this environment (for example making the agent more biased against taking the condition it wouldn't have, say taking a over b). It would still operate in the same way even though we've changed the environment.

**j. A perfectly rational poker-playing agent never loses.**

**False.** 
	An agent can maximize its performance based on the state of the game but since the environment is not deterministic (we don't know what cards we'll get) we cannot guarantee a win. 
# Exercise-2

## a. Playing Soccer

**Performance Measure**: goals, interceptions, distance ball is moved towards opposing teams goalie

**Environment**: soccer field

**Actuators**: legs, arms, hands, 

**Sensors**: eyes, ears


## b. Exploring the subsurface oceans of Titan

**Performance Measure**: amount of new area discovered, coverage of selected observation area completed 

**Environment**: water/liquid ocean, deep poorly lit vast area. 

**Actuators:** propeller, robotic arms, probes, drills

**Sensors:** cameras, depth gauges, sonar transceivers

## c. Shopping for used AI books on the internet

**Performance Measure**: average difference in prices between deals and market value

**Environment**: Internet

**Actuators**: screen, phone app

**Sensors:** keyboard, search inputs from user, internet queries 

## **d. Playing a tennis match**:

**Performance Measure:** games won, games lost by opponent 

**Environment:** Tennis court (grass, clay, cement)

**Actuators**:  arm, hand, racket, body

**Sensors**: eyes/cameras, accelerometer

## **e. Practicing Tennis against a wall**

**Performance Measure**: number of consecutive hits against the wall, hits per minute

**Environment**: Wall, Ground 

**Actuators**: racket, hand, body

**Sensor**: camera/eye, accelerometer

## **f. performing a high jump**

**Performance measure**: height of the jump, distance between bar and agent at lowest point

**Environment**: gym, high elevation bar
 
**Actuators:** Pole,  body, legs, arms

**Sensors:** cameras/eyes, rangefinder, proximity sensor. 

## **g. knitting a sweater**

**Performance Measure:** conciseness and uniformity of pattern

**Environment:** rocking chair, fabric

**Actuators:** sewing needles, arms/hands/manipulators

**Sensors:** camera/image sensor

## **h. Bidding on an item at an auction**

Performance Measure: winning at the lowest possible price 

**Environment:** sales floor, auction house

**Actuators:** price display, bidding software system

**Sensors:** camera, live auction feed, audio input for spoken word auctions

# Exercise-3 

## Google's Bard AI Chatbot
 
 **Explain the Experiment**: 
	 Bard is googles AI chatbot built on the GPT-3 Large Language Model
 
**what are the applications of this experiment:** 
	This product allows users to make broad requests and have them filled according to their specific situation and context. This allows users to apply general knowledge to their specific situation.

**How was this experiment Implemented?**:
	this chatbot was implemented using a Large Language Model (LLM). These are pre-trained weighted and biased networks of neurons that generate character after character of text as output. 

