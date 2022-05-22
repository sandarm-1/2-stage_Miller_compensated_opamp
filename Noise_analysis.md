# Noise of 2 stage Miller compensated op amp

## Noise analysis

To get the overall noise of the 2 stage op amp, first we remember that we already know the noise for the single stage op amp from before.

Then we neglect all caps (noise result will only be valid for DC but ok as an approximation).

Then we analyze it by superposition principle. 

![image](https://user-images.githubusercontent.com/95447782/169706066-76ea8426-a253-41ce-8d5e-b45f0ba15d82.png)


Overall, as a general result we know that if we have a number of stages concatenated, the overall input referred noise will be the input referred noise of 1st stage, plus input referred noise of second stage divided by gain of 1st stage squared, plus input referred noise of third stage divided by the product of gains of 1st and 2nd stage squared, and so on.

![image](https://user-images.githubusercontent.com/95447782/169706076-c67f8f49-084a-49a9-a5b3-1d9c1071f155.png)


So overall we see that the input referred noise is mostly given by the input referred noise of the first stage. The noise of the 2nd stage is divided down by a large amount, by the gain of the 1st stage. If we have a 3rd stage, this will be divided down even more. So the noise of the 1st stage is what matters.

**Summary: NOISE of 2 stage op amp is the same as the noise of single stage op amp!! Svin=(16/)3·KT/gm1*(1+gm3/gm1)**

![image](https://user-images.githubusercontent.com/95447782/169706085-2b7317e7-d23e-4682-80bf-57900df91702.png)


That´s it for noise of the 2 stage op amp. Let´s look at offset now.


## Offset

Next:

* [Offset](Offset_analysis.md)

