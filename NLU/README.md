# NLU
Natural Language Understanding for someone who understands Natural Language

## Table of Contents
1. [Adversarial Training](#adversarial-training)
2. [Task-Completion Dialogues](#task-completion-dialogues)
3. [User Simulator](#user-simulator)
## Adversarial Training

## Task-Completion Dialogues
First let's define some terminology.</br>
Task-Completion Dialogues: Dialogues between a user and agent that can be composed of several utterances with an end goal in mind.</br> For example a dialogue for booking a movie(goal) could go like this:</br>
> User - "What's playing?"</br>
Agent - "Deadpool 2 and Winnie the Pooh."</br>
User - "What time is Winnie the Pooh?"</br>
Agent - "At 7:30pm."</br>
User - "Great i'll get those tickets."</br>

In this example, the user through a series of exchanges got a movie he liked at 7:30. The process that took the user there was a series of steps that required the the agent to guide the answer correctly. If the agent did not take the right steps in the conversation, it could have played out like:</br>

> User - "What's playing?"</br>
Agent - "Deadpool 2 and Winnie the Pooh."</br>
User - "What time is Winnie the Pooh?"</br>
Agent - "There is also Bohemian Rhapsody."</br>
User - "No, what time is Winnie the Pooh."</br>
Agent - "Winnie the Pooh is playing in 3D."</br>
User - "Nevermind..."</br>

In this scenario, the user did not end the result he wanted, this was because the agent took the wrong steps of the conversation after the user asked "What time is Winnie the Pooh?". So, if a conversation is a series of steps and yours steps can take you to the right or wrong place...then...we can reframe the problem...any ideas? REINFORCEMENT LEARNING! NLU can become a RL problem following a policy to get the right results.</br>

## User Simulator
Now that we know what a Task-Completion Dialogue is and that conversations can be reframed into an RL problem, why do we need a User Simulator. A User Simulator is just that, a User Simulator, it acts like a user conversating with the agent. A User Simulator's purpose is to give more diverse data at a lower price tag(since you don't have to pay people to train with the agent) and train an agent faster than a human can.</br>

> "Practical dialogue systems consist of several components. The natural language understanding
(NLU) module maps free texts to structured semantic frames of utterances. The natural language
generation (NLG) module maps the structured representations back into a natural-language form.
Knowledge bases (KBs) and state trackers provide access to side information and track the evolving
state of the dialogue, respectively. The dialogue policy is a central component of the system that
chooses an action given the current state of the dialogue."

A User Simulator helps us train the dialogue policy. This policy can even explore spaces(other sentences) that would not have been made by humans if they were training the agent, there only so many ways I can think of asking for chicken. Given the reward signal if the task was correct, the agent can learn unsupervised giving it less bias to an expert who asks for movies in a certian amount of ways.
