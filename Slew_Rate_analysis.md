# Slew Rate of 2 stage Miller compensated op amp

Slew rate analysis of 2 stage Miller compensated op amp.

## Slew Rate

Slew rate is **the maximum rate of change that you can get on the output**.

We start by putting the 2 stage amplifier in unity gain feedback and applying a big voltage step on the non inverting input.

![image](https://user-images.githubusercontent.com/95447782/169825025-050f5991-5732-430a-a686-b81a7ebd0465.png)


We need to consider not only the rising slew rate but also the falling one. So, both cases, the one with a positive voltage step on the input and the one with a negative step.

![image](https://user-images.githubusercontent.com/95447782/169825043-b7c2ba7a-8d6c-4c28-81c4-376dff9b3f90.png)


We see that in the case with a negative step on the input the output slew rate can be either limited by Io of the differential pair or by the bias current of the 2nd stage, I12.

![image](https://user-images.githubusercontent.com/95447782/169825057-31870b77-3a5b-45b7-a3b0-69dea4d08a17.png)




## Final thoughts

Next:
* [Final thoughts](/Final_thoughts.md)

