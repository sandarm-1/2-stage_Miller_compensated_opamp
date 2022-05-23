# Final thoughts and considerations on 2 stage Miller compensated op amp

The 2 stage Miller compensated op amp:

* It has a higher DC gain that the single stage amplifier.
* Even with a resistive load, even if the 2nd stage gain drops, the 1st stage can provide enough gain.
* The noise and offset are similar to the single stage op amp. Both noise and offset are contributed mostly by the first stage, while the 2nd stage contribution is attenuated by the gain of the 1st stage.
* The slew rate, on the positive side is the same as in a single stage op amp, but on the negative side can be limited by the Io of the diff pair or by the I12 of the 2nd stage.
* The swing limits, on the input side are the same as in the single stage op amp. On the output side, they are better, as the output can swing from one VDSAT above ground up to a VDSAT below VDD.


One thing to consider is how to connect the load to a 2 stage op amp.

Since we are operating at single supply (betwen VDD and 0V Ground), the input voltage must be biased at some intermediate voltage, and hence also the output must be biased at an intermediate voltage.

That means the load is not connected between the output node and ground, but between the output node and an intermediate bias voltage (in the single supply case).

That's in the case where you have some resistive load. If the load was purely capacitive, you could connect it to any voltage, since at DC it won't draw any current.

