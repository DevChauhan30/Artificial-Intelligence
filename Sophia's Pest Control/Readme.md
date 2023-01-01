# Robot defense Project
## CSC 4240: Artificial Intelligence
### Team Members: Dev Chauhan, Autin Ring, David Miller, and Leah Faulkner


#### 1a. In the LearnerOne Agent file under the function "private static final AgentAction[] potentials" power setting was intialized into a variable called potentials. We added action to be able to set the power to 0 (off) and just point it a random direction since it was off and didnt matter. We then loaded that into the end of potentials so that it can use that action. We also implemented that if 6 ticks pass by we would force a new action consideration.

#### 1b. We calculated function to include all 32 possible actions with all 4 power settings and all 8 directions. That way it can turn off and consider power settings for each direction. We then realized that is a lot of learning it would have to do for all of those settings so we added 2 and 4 the power settings uunder the potential array and listed under the power and direction settings for optimal results. 

#### 1c. We figured out that when there are more bugs on the map, the faster the tower changes its action. So when you have to send out the bugs manually you can keep one bug on the screen at a time, so the tower have time. If the tower is sucking a bug it will have more time to capture it on the 10 sec timer. it is possible for more than one bug to be on the screen at a time, so the tower will change actions more time, therefore have less time to suck in a bug.

#### *LearnerOne File Result:*
####	Captured	Escaped
####	   62         57

#### *DevAgent File Result:*
####	Captured	Escaped
####       86	      56

#### 1d. We changed the reward function value from 10 to 20 to see if that would change the outcome. We then ran two tests on changing the bug values as we noticed at first that it had a hard time trying to catch certain bugs.

#### Simple.dat

#### *DevAgent File Result:*
#### Captured Escaped 
####  149       120

#### *LearnerOne File Result:*
####  Caputured     Escaped
####    61             58

#### 2a. To be able to run the last action that the agent took we passed the last action to the reward best action function. We then nested an if statement in the if statement that checks how many possible " Doing best" actions there is. And returned lastAction in the loop. 

#### 2b. We approached this by looked at how the states are stored in the step function. We can see that is uses lastState first and rewards that state, it then sets lastState to the current state afterwards. We can then use that to reward the current state that is stored in the lastState before it loops again. Therefore we reward our lastState normally as it caught a bug, and if lastState caught a bug we reward the current state aswell but not nearly as heavily. lastState gets rewarded 20 points while thisState gets rewarded 5 points. 

#### 3a. We know there are 8 directions and 4 power settings an we wanted to if a bug was caught on power 4 and it was pointing North, we wanted to reward the directions similar to North ; which would be North-East and North-West. So we created an array of size 16 and see how the actions are being stored when we reward them. We then printed out the array to see how they are being stored and realized there was a pattern based off our initial for loop. To  be able to get the related state you would have to increment by 2 and decrement by 2. We then tried this and got a null pointer error because if the action was stored in position 1 it would try to access and action stored in [-1]; which doesn't exist. We then made two if statements to loop back around our array so that if the action stored in 0 was called it would reward action at position 2 and position 14; which would be the two actions related to our action that we are rewarding. However we did not want to reward these actions the same value as the action that caught the bug so we rewarded it the normal value / 4, which would be 5. Which is the same value as our current action reward implemented from the last step. 

#### 3b. We changed StateVector file by modifying and creating creating a new public boolean variable called EmptyRadius and it would add all of the bugs code together and if that was 0 then that means there is nothing currently in the radius for it to make a knowledge based decision. Therefore we set this boolean in the current StateVector to true. We then create a getEmptyRadius() which returns this boolean for each state and then we can flip the switch on the vacuum to save resources. After this changes we tested the file and compared it to the LearnerOne File and we stated those results below. Overall, there was a signinificant improvment after changinging this in the StateVector file. 

####  *DevAgent File:*
####  Caputured     Escaped
####     317	      161

####  *LearnerOneAgent File:*
####  Caputured     Escaped    
####	 50	         75
 