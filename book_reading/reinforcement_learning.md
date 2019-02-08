# book notes
Refer to "Reinforcement Learning: An Introduction 2ed".

## 5. Monte Carlo Methods
* Learning From Actual Experience and Simulated Experience(page 113) 
    * **learning from actual experience**  
    In this case, the agent will learning from real world experience, 
    so does not needs any prior knowledges, such as the knowledge 
    of how to calcutate reward/return since the real world will give 
    us the real values of them.
    * **learning from simulated experience**
    Not as learning from actual experience, in this case we needs 
    prior knowledges such as we mentioned above.
* **Sample Transition VS Complete Probability Trnsitions**(page 113) 
    * **Sample Transition**  
    The probabilities transition only for the states in sampled states, 
    which means the states space is all the state appered in monte 
    carlo simulation.
    * **Complete Probability Trnsitions**
    The probabilities transition for all possible states.
* **episodic task**

### 5.2. Monte Carlo Estimation of Action Values
* **With or Wothout Model**(page 118)  
    * **With Model**  
    (?) Maybe represent with a model for state transition probabilities.
    * **Without Model**
    The agents can learn policy with a model, for example, maybe a 
    model which can help descript the distribution of state transition 
    probabilities. So obviously, Monte Carlo Estimation is a without 
    model method.
* **Exploring Start**  
(?) It can not be used when learning from actual interaction since in 
actual interaction, we can not choice which action to start.

### 5.4. Monte Carlo Control without Exploring Starts
* **|*A*(s)|**  
***A*(s)** represents all possible actions, **|*A*(s)|** represents 
the number of all possible actions.
* **e-greedy VS e-soft**(page 123)  
(?)
* **Optimal Among e-soft Policy**  
(?)
* **On-Policy Method**  
There exist a policy pi, which can make a prediction about the 
probibalities for taking each action on each state.

    
