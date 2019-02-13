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
* **|*A*(s)|, ||**  
***A*(s)** represents all possible actions, **|*A*(s)|** represents 
the number of all possible actions.
* **e-greedy VS e-soft**(page 123)  
(?)
* **Optimal Among e-soft Policy**  
(?)
* **On-Policy Method**  
There exist a policy pi, which can make a prediction about the 
probibalities for taking each action on each state.

### 5.5. Off-policy Prediction via Immportance Sampling

* **importance-sampling ratio**(page 126)  
  When we calculating the value for a state, s, we need pi(a|s) 
  or b(a|s) to calculate the expected returns, for of-policy 
  prediction, we only has b(a|s), includes {b(at|st)}, but 
  rho(t:T-1) can represents the "factor" to transform b(a|s) 
  to pi(a|s), which means, it is an average amount that can 
  holds pi(a|s) = rho_(t:T-1) * b(a|s) for all states visited 
  during a episode. So E[rho_(t:T-1) * G_t | S_t=s] = v_pi(s). 

  On the other hand, during calculating, the value of pi(a|s) 
  was gotten from last episode, but the value of b(a|s) was 
  gotten from current, but this can also let pi(a|s) converage, 
  since the updated value of b(a|s) can sort of "correct" the 
  value of pi(a|s) since we estimate pi(a|s) = b(a|s) * rho_(t:T-1), 
  and in this operation, the b(a|s) can bring some new information.   
  
  For instance, "a" should be 2, "a * b" should be 4, in last 
  episode, we estimate a = b = 3, in current episode, we estimate 
  b = 2.5, so the estimate of "a * b" is now 7.5, relative more 
  close to 4 compare with 3 * 3 = 9. Another example, suppose the 
  "a" not changed, which is 4, "b" in 4 episodes are 2.5, 1, 0.5, 
  0.25, so the "a * b" are 10, 4, 2, 1, and the average of them 
  are 4.25, so the estimate of "a * b" is more closely to true value.   
  
  The last easily confused point, in one episode, only limited state 
  will be visited, so in this episode, only these visited states' 
  related infomation will be updated.  

* **importance-sampling ratio**(page 126), breif  
G is the mainly holder and updator of each state's value, and 
rho_(t:T-1) is used for fine tuning G using certain history data.

* **two form of importance sampling**  
    * **ordinary importance sampling**(page 126)  
    This is just arithmetic mean value of all episoddes' 
    rho_(t:T(t)-1) * G_t.
    * **weighted importance sampling**(page 127)  
    In this case, we can think the importance-sampling ratio as 
    the "importance" of this state's G_t in current episode. If 
    it's larger, which means in this episode, for this state, the 
    real G_t should be more larger than G_t compare the larger 
    degree for this state in other episodes, so this G_t should has 
    larger weight.  

    
