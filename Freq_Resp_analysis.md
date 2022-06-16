# Frequency response of 2 stage Miller compensated amplifier

## Motivation

The motivation for a 2-stage amplifier comes from the limitations of the single stage amplifier, whether it’s basic 5T op amp, or telescopic or other single stage topologies. Multi stage topologies (2-stage, 3-stage, etc) have advantages over single stage.

Single stage op amp has some limitations:

* **You cannot operate it with resistive loads**, just capacitive loads (like an integrator), because it will drop the DC gain because DC gain is Ao=Gm·Rout and if you put a resistive load in parallel with this amp’s Rout you will drop the Rout, dropping the DC gain. We don´t want that because lower DC gain will mean larger steady-state error.
* The **overall DC gain that we can get from this is quite limited**, it’s not huge. It’s gm1/(gds1+gds3) and that is in the order of magnitud of the gain of a single transistor (single transistor gain Av=gm·rds).
* To increase the DC gain of this amp, you would have to increase the rds1 & rds3. We know rds of transistors depends on channel length, longer device is more resistive. But if we increase L of devices, we will also have to increase W proportionally to keep W/L, since we don’t want to change gm1. So overall we will end up increasing the overall size of transistors which will increase parasitic caps and will reduce speed. Even if we don’t care much about speed, and we want to go down this route of increasing L to get some extra DC gain, we cannot increase L by 100 times, so it will be quite limited anyway.
* The way to increase DC gain from this circuit is to use cascodes, both on input pair and on loads, and that leads to **the TELESCOPIC amplifier** and the **FOLDED CASCODE amplifier**.
* Even with cascodes, you will increase the intrinsic Rout of the amplifier but you will still be unable to drive resistive loads, because again if you put a resistor on the output, it will appear in parallel with the Rout of the amp, lowering it, again dropping DC gain.
* To avoid that, you would **use a second stage** like a common source amp, Class A, Class B etc so you buffer the first stage and you get the current drive capability at the output.


![image](https://user-images.githubusercontent.com/95447782/169705663-e65166db-e9d8-49c9-8dae-785216bab64f.png)


Notice the polarity inversion in the terminals of the transconductors in the 2 stage one.

How we implement these 2 stages?

In this example we will make the 1st stage with a diff pair with current mirror load, and 2nd stage with a PMOS common source, which is another transconductor. We could use an NMOS output stage but it would be more inconvenient, maybe easier with low VDD but usually you will use a PMOS.

![image](https://user-images.githubusercontent.com/95447782/169705667-a0b2cc46-87b7-4acb-8bf0-21c8da81d1b9.png)


 This is the Miller-compensated op amp.
 
 ## Frequency response of the Miller compensated op amp
 
 ### At transconductor level
 
 First of all, this is what gives rise to this 2 stage topology with a cap across the 2nd stage (Miller compensated).
 
 ![image](https://user-images.githubusercontent.com/95447782/169705687-f3369270-e5c0-4deb-aee1-415affdb98e8.png)


So this is the 2 stage topology that we will have. This will be a 2 pole system (there are 3 caps but they are connected in a loop so their voltages are in series, meaning that only 2 cap voltages are independent, so only 2 independent state variables, so 2 poles).

The DC gain of it we can calculate by inspection, before doing the full blown Laplace analysis.

![image](https://user-images.githubusercontent.com/95447782/169705694-de1a570c-2920-4425-a4ee-c414d4549901.png)


Now doing the full transfer function analysis:

![image](https://user-images.githubusercontent.com/95447782/169705699-27b54461-66ee-417c-8732-2a84bfc9a2a2.png)


We solve Vo with Cramer’s rule:

![image](https://user-images.githubusercontent.com/95447782/169705705-e6fd1f63-ed2f-4d17-805c-ce0f55d2eff9.png)


The full transfer function is then:

![image](https://user-images.githubusercontent.com/95447782/169705707-af86a475-2fdb-406d-97c4-c42132d7a36b.png)


The poles are at:

![image](https://user-images.githubusercontent.com/95447782/169705713-f9356330-e6c8-4def-b0ef-b631b777b509.png)


We can also try to get the poles just by inspection of the circuit. When we have 2 stages concatenated, and each stage’s output has a parallel combination of R and C, each stage’s pole is at Gm/C of that stage. So with 2 stages concatenated, the transfer functions just multiply each other, and you just get 2 poles, the poles of the 2 separate stages.

![image](https://user-images.githubusercontent.com/95447782/169705717-c0aaddda-a3cc-42b2-90f2-c5a159d0a0e8.png)


Now the problem comes when you have a Miller cap wrapping around one stage. In that case, you apply Miller’s theorem on the Miller cap, splitting it in 2, so after doing that you can see the 2 poles by inspection again.

![image](https://user-images.githubusercontent.com/95447782/169705722-d6532c0b-eb26-4eb5-bd42-48a3a52abd84.png)


Since our 2nd stage has a gain of -Gm2/Go2 (=-Gm2·Ro2), the cap C looks like a cap of value (Gm2/Go2 + 1)C in parallel with C1 of 1st stage.

This has the effect of shifting the dominant pole p1 down in frequency.

![image](https://user-images.githubusercontent.com/95447782/169705730-ec3bbeae-37bf-43d5-9c69-3998f6662a84.png)


So, this is the comparison of where the poles are located, with and without the Miller cap.

It turns out **the Miller cap does the effect of POLE SPLITTING. The dominant pole p1 is pushed to LOWER frequency and the non-dominant pole p2 is pushed to HIGHER FREQUENCY (this is good for stability).**

![image](https://user-images.githubusercontent.com/95447782/169705740-66f92f49-38da-4f65-8695-26d4ab591f6e.png)


This is the overall “Frequency response datasheet” that we have for the 2-stage op amp Versus the single stage one (at transconductor level, not at transistor level, hence neglecting parasitic caps here):

![image](https://user-images.githubusercontent.com/95447782/169705792-fb31bb74-caf0-4ec3-9f8f-db002c93cf2d.png)
 
 
 Note, here at transconductor level **we can already see the right half plane zero (RHPZ), that is z1=Gm2/C,** where Gm2 is the 2nd stage transconductor's transconductance and C is the Miller Cap. So, **the RHPZ comes from the parallel path created by the Miller cap in parallel with Gm2.** We have obtained it simply from applying nodal analysis to the 2 transconductors plus the Miller cap (no parasitic caps taken into account yet), writing the conductance matrix and then solving with Cramer's rule. By doing that we got the transfer function and in that transfer function we got a zero on the numerator, and it's a positive zero so it's in the Right Half Plane so that's where the RHPZ comes from. This zero is the one that can create stability concern as it creates phase lag and for this zero you see sometimes the nulling resistor in series with the Miller cap.

One thing to note is, the single stage opamps (transconductors driving a capacitive load) we have shown them as SINGLE POLE SYSTEMS, because we are at this point thinking of them as IDEAL transconductors, so there is only one pole (load cap). But in reality we saw that once we implement this single stage amp with for example a 5T amplifier circuit at transistor level, once we take into account the parasitic cap of that circuit, then it becomes a 2 pole system on its own. But it’s ok the Miller principle is illustrated well anyway with ideal transconductors.

Overall, **the Bode plot of the transfer function for the 2 stage op amp with Miller compensation looks like this:**


![image](https://user-images.githubusercontent.com/95447782/169705809-6b9f8542-b037-425b-8ef4-318b36e9c263.png)


We see that applying feedback around the op amp makes a difference for stability. The worst case for stability is to have unity feedback, as in K=1. Higher feedback gain is better for stability as seen in the plot above, although of course it also reduces overall unity gain frequency of the feedback system.

![image](https://user-images.githubusercontent.com/95447782/169705816-f5f06cf9-b5ca-4037-998c-0560cd36aafe.png)


Note, here in the 2 stage op amp the non dominant pole p2 MAY OR MAY NOT BE ABOVE THE UNITY-GAIN FREQUENCY. Don’t get confused with the single stage op amp (5T) where we got the result that, once taking parasitic caps into account, it became a 2 pole system where the 2nd pole was ALWAYS beyond unity gain frequency so it was UNCONDITIONALLY STABLE. This is not the case here with the 2 stage op amp. In the s tage op amp we need to actively ensure p2 is indeed after the unity gain frequency, to ensure we cross unity gain frequency with -20dB/dec and not with -40, which would be unstable.

![image](https://user-images.githubusercontent.com/95447782/169705823-3e836935-ea67-406e-81c4-9b615cc8cb13.png)


### At transistor level

Ok, so **up to this point we have analyzed the Frequency Response of the 2-stage Miller compensated op amp WITH TRANSCONDUCTORS, BUT NOT AT TRANSISTOR LEVEL YET**.

Let’s go back to the TRANSISTOR LEVEL IMPLEMENTATION, and let’s get the Frequency Response of the transistor level implementation.

This will be a case of mapping our TRANSISTOR LEVEL parameters to the TRANSCONDUCTOR LEVEL parameters.

Ok so **let’s transistorize**.

![image](https://user-images.githubusercontent.com/95447782/169705866-a9f65dd2-9f1f-4c0a-bad6-c4e16d58f819.png)


To transistorize this, we simply have to identify the values of these components C, C1, CL, Go1, Go2, Gm1, Gm2 in our transistor level implementation.

One thing to note here is, for Gm1 we need to use the Ym(s) which we already obtained for the single stage op amp at transistor level, that is, the Ym(s) including the parasitic caps in the diff pair with current mirror load.

![image](https://user-images.githubusercontent.com/95447782/169705880-be313612-9120-4476-82dc-4d7f5d0787c2.png)


Now let´s insert the values into the overall transfer function of the 2 stage opamp:

![image](https://user-images.githubusercontent.com/95447782/170734642-58ffc991-3ac8-4ae2-9172-b175096dad5d.png)


Note, in the datasheet or summary above:
* p1 is the dominant pole, lowest frequency, already pushed to lower frequency by the "pole splitting" effect
* p2 is the non-dominant pole, the one that gets pushed to higher frequency by the "pole splitting" effect
* p3 is the pole created by the parasitic cap Cd3 inside the first, single stage amp
* z1 is the RHPZ, right half plane zero, it comes from the parallel path created by the Miller cap in parallel with Gm2
* z2 is the pole created by the parasitic cap Cd3 inside the first, single stage amp, it's 2x the frequency of the p3 pole. Note that z2 is a left half plane zero while z1 is a RHPZ so they have different effect in the phase, in particular the LHPZ "helps" by increasing the phase value in the phase plot (thus increasing PM) while the RHPZ has a worsening effect in phase, as it reduces phase in the phase plot, hence pushing the phase value closer to the danger zone of -180º, i.e. reducing PM.

Now let’s see with specific values why the 2-stage opamp advantage is that it allows us to achieve decent DC gain into a resistive load.

Example with RL of 1KOhm, and let’s say we want to achieve a DC gain of about 1000.

![image](https://user-images.githubusercontent.com/95447782/169705885-4b01a35d-fa1d-41d5-b7ca-02c54dc88ba1.png)


This finished the FREQUENCY RESPONSE analysis of the 2 stage op amp.

Now we can move to Noise, Offset, Slew rate and Swing limits.

Next thing is Noise.


## Noise

Next:

* [Noise](Noise_analysis.md)



 
