# Offset of 2 stage Miller compensated amplifier

Offset is by definition DC so we ignore caps.

![image](https://user-images.githubusercontent.com/95447782/169706140-8d1b3f58-b580-40f7-9eed-ce1ace4355c9.png)

Again the **RANDOM offset** is the same as noise. 1st stage is what defines it.

But, here comes an IMPORTANT POINT about offset:
* This calculation so far is for RANDOM offset.
* There is also the other component of offset, which is SYSTEMATIC offset.

The **systematic offset** component is relevant only for the 2 stage opamp. In the single stage op amp, it was not relevant. This is because in the single stage op amp, due to symmetry, the operating point at the drains of both PMOS load devices was the same (vom = vop if both branches carry the same current and devices are symmetrically matched). Yes there will be random offset in the single stage op amp because of mismatch, but not systematic.

Now in the 2 stage op amp we will also have a systematic offset component that is NOT DUE TO DEVICE MISMATCH, but is actually due to the 1st and 2nd stages “fighting” to set the operating point at vop (output of 1st stage) at slightly different levels.

Let’s see the reasoning for systematic offset.


![image](https://user-images.githubusercontent.com/95447782/169706149-9ca9adea-f0b7-4301-af2b-49f95db2f9e0.png)


Continuation of systematic offset derivation:

![image](https://user-images.githubusercontent.com/95447782/169706153-b958dc6d-8bf7-4bf9-bf50-75b81ddaa84e.png)


And finally, to finalize with the systematic offset derivation, we see how we can avoid systematic offset, and that is by equalizing the current densities in M4 and M11:

![image](https://user-images.githubusercontent.com/95447782/169706158-86f9584c-e2e0-42f5-9654-f52f824b4df6.png)


This finalizes the Offset analysis in the 2 stage Miller compensated op amp.

Next is swing limits.


## Slew rate

[Slew rate](/Slew_Rate_analysis.md)
