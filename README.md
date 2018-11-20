# MIT-OpenCourseware-Feedback-Control-Project

1 Overview
This problem considers the control of a fast tool servo (FTS), and is based upon the work done by Xiaodong Lu in his Ph.D. thesis. A copy of this thesis is available on the course web page. The design problem focuses on:
• High-bandwidth current controller for driving the actuator.
• Identification of the electromechanical plant dynamics from a measured Bode plot.
• Design of a controller to minimize following error for a sinusoidal reference trajectory, in the presence of sensor noise.
• (2.140 students only) Design of an add-on Adaptive Feedforward Cancellation (AFC) con- trol block at the reference trajectory frequency in order to eliminate following error at that frequency.
We do not give you exact specifications for the servo performance. Rather, you are to apply your best effort to get good performance. The measure of perfomance in this problem is reduction of the following error due to the reference trajectory and to sensor noise.
The problem starts with designing the controller for the current loop, and then moves on to design of the FTS position controller.
2 Current control loop
The current control loop circuit is shown in Figure 1. The circuit includes the back emf voltage from the actuator as a dependent source. The force supplied by the actuator is F = Kf ic, and the corresponding back emf voltage is Vbemf = Kfx ̇. A simple model of the electromechanical system of the FTS is shown in Figure 2, with the actuator force F applied to the mass m1.
In this problem, assume the following component values: Rc = 4 Ω, Lc = 2×10−4 H, Kf = 20 N/A. In designing the current controllers for power amplifiers, it is typical to neglect the actuator back
emf in the current loop dynamics. (The back emf is quite important in modeling nonlinear issues 1
such as amplifier saturation, but we do not consider that issue in this problem.) We ask you in this section to show that the back emf can be ignored, and then to design a current loop controller on that basis.
3
•
•
• • •
•
Calculate the plant transfer function for the current loop with the back emf voltage included. Note that in this model, the FTS mechanical dynamics will be reflected into the electrical transfer function.
Calculate the plant transfer function for the current loop with the back emf voltage assumed equal to zero. Under this assumption, the FTS mechanical dynamics will have no effect on the electrical transfer function.
Show that for high frequencies, both transfer functions are equal. Explain physically why this is the case.
On this basis, recognize that you can design the current control loop assuming the back emf voltage is zero.
Design the current control loop such that the crossover frequency is ωc = 6×105 rad/sec, with a phase margin φm ≥ 60◦. We also require that an input voltage of Vset = −10 V will result in a steady-state coil current of ic = 5 A. That is, the current drive has an input/output DC gain of Ga ≡ ic/Vset|DC = −0.5 A/V. For these design specifications, what are the resulting values of R2, R3, C1, and C2? Note that R1 is given as 10 kΩ. Further note, as shown on the schematic, that we assume that no current enters the input resistors of the differential amplifier, since these resistors are large compared with the 0.2 Ω sense resistor.
Provide a Bode plot for the loop return ratio showing the crossover frequency and phase margin.
Actuator model
The actuator conceptual model is shown in Figure 2. Here, the actuator force F = Kf ic acts on a spring/mass/damper system representing the moving components of the fast tool servo.
A block diagram for the plant dynamics is given in Figure 3. Position x is measured with a capacitance probe with a gain of G1 = 5 × 105 V/m. The sensor has an associated noise voltage Vn.
From this point on in the problem, we assume that the current drive dynamics are so fast that there is a static gain coefficient Ga A/V which relates Vset and ic. That is, we now assume that there are no dynamics associated with the current drive. This is shown on the block diagram where ic depends statically upon Vset via the gain Ga.
2
4 Plant measured Bode plot
The measured plant Bode plot is shown in Figure 4. As we see from the Bode plot, the plant dynamics are more complicated than would be expected from the simple model of Figure 2. The lowest mode in the Bode plot is due to the spring/mass/damper system, but there are higher frequency modes and a time delay.
This Bode plot and associated data files for magnitude and phase are available on the course web page in the .zip file GpPlantFrequencyData.zip. Use these data files as part of your model bulding process. In the data file, we have included a .mat file for entry into Matlab. This file includes the column vectors Gpmag, which is the magnitude of Gp(jω) in straight magnitude units, Gpphase, which is the phase of Gp(jω) in degrees, and ww, which is the associated frequency vector in rad/sec.
• On the basis of the low-frequency dynamics and first mode, what are the values of m1, b1, and k1?
• Fit a dynamical model to the measured Bode plot. Provide a pole-zero plot for your model, and show a Bode plot of your model frequency response overlaid on the measured frequency response. (In extracting data from the Matlab bode command, you will notice extra dimen- sions, which can be eliminated with the squeeze command.)
You will use this model to design your controller in the following section.
5 Controller Design
The control loop configuration is shown in Figure 5. The controller configuration is shown in Figure 6. Here, the integrator is explicitly shown, and transfer function Cls(s) is a loop shaping controller of your design.
Throughout this problem, we assume
xref = 10−5 sin 3000t [m].
We also assume throughout that
Vn =5×10−2sin105t[V].
• Design a controller with as good performance as you can achieve. The controller must mini-
mize the following error xe due to the reference trajectory and the sensor noise.
• You must show us Bode, Nyquist, and Sensitivity plots for your FTS controller design. Of course, the loop must be stable! Also, the Sensitivity magnitude plot must be under +10 dB for all frequencies. These plots are for the loop broken at the plant input Vset.
3
6
•
•
•
Also provide time-domain plots of the position error xe(t). What is the magnitude of the error due to the reference trajectory xref (t)? What is the magnitude of the error due to the sensor noise Vn(t)? How have you addressed minimizing these errors in your loop design?
Also, you must run a live simulation on Matlab during checkoffs to answer questions about the loop. Thus, you will need to have a Matlab-based model of the FTS position control loop running at your checkoff, so that we can ask you questions about its performance. Please come to lab in advance of your checkoff in order to have time to get your model running before the checkoff starts.
A template in the form of an m-file (Template.m) has been posted on Stellar. You are required to use this template to present your design during the check-offs on Monday, May 12, and Tuesday, May 13. A checkoff signup sheet will be posted in advance of checkoffs. To use the template, download a copy of it from Stellar. Please read the instructions provided below as well as the comments within the m-file on how to use the template.
Within the template, we have defined the parameters values given in the problem set, such as LC and Rc. The controller and plant transfer functions, which need to be designed and identified by you, have been declared as blank ( [] in MATLAB). You must initialize these transfer functions by adding your own code to the m-file. Once you have initialized the transfer functions, all of the plots required for the check-off can be generated by running the Template.m file. You can add your design code to this file. It is important that you use the exact same variable names declared within the template. You are allowed to declare your own variables but do not overwrite any variables already in use by the template. Please test your code on either your own laptop or the lab computers ahead of time and confirm that it runs correctly before your check-off.
For 2.140 students, you will need to document your design as it works without the AFC, and then document with AFC. For this purpose, please prepare two models from the template file, or provide some means to switch between models so that we can see the effect of using or not using AFC.
Your design project grade will depend upon your checkoff results, and upon our evaluation of the quality of your design efforts. Please prepare a lab report detailing your design work, and showing how you went about optimizing the design for the given specifications. Include relevant calculations, data, and plots.
AFC Controller Design (2.140 students only)
•
•
This section is only to be completed by 2.140 students.
In order to eliminate steady-state following error, we can add an Adaptive Feedforward Cancellation control block. A reference for the design of this type of controller is given in the Ph.D. thesis of Xiaodong Lu, which is available on the course web page. In particular, look at section 7.3 of Lu’s thesis. The controller you will implement will use only one AFC block, in the topology shown in Figure 7–12b of the thesis. The controller configuration with a single AFC control block is shown in Figure 7.
4
￼Figure 1: Current loop circuit.
Here, the transfer function A1(s) is a resonator with a natural frequency chosen to match the input position reference frequency of 3000 rad/sec. That is,
A1(s)= K1s , s 2 + ω 12
where K1 is an AFC gain to be chosen for adequate stability, and ω1 = 3000 sets the resonator to lie at the reference trajectory frequency.
• Design the AFC-based controller, and show that the following error at 3000 rad/sec is elim- inated. Show plots of the loop Bode, Nyquist and sensitivity curves. The sensitivity must remain below +10 dB for all frequencies. All these plots should be for the loop broken at the plant input Vset.
• Make a Bode plot of your controller including AFC; you should see that the controller gain is infinite at the resonant frequency.
• The approach given in section 7.3.3 of Lu’s thesis, and in particular the design rule on page 244 will help you with this design task. Explore the rate of error convergence as K1 is varied; how does K1 affect convergence? What is the upper limit of K1 for loop stability?
￼5
￼Figure 2: Model of actuator driving fast tool servo.
Figure 3: Block diagram of fast tool servo with current setpoint input Vset, sensor noise input Vn, position output x, and sensor output voltage Vsense. Plant dynamics including flexibility are represented in Gp(s).
￼6
￼ 60
 80
 100
 120
 140
 160
 180
0  90  180  270  360  450  540  630  720  810
 900
Bode plot for FTS plant transfer function G (jw) p
￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼￼23456 10 10 10 10 10
Frequency (rad/sec)
Figure 4: Experimentally-measured plant transfer function for Gp(jω). This plot and associated data files for magnitude and phase are available on the course web page.
Figure 5: Control loop configuration.
￼7
Phase (deg) Magnitude (dB)
￼Figure 6: Controller configuration with isolated integrator.
￼Figure 7: Controller configuration with isolated integrator and a single AFC controller block.
8
MIT OpenCourseWare
http://ocw.mit.edu
2.14 / 2.140 Analysis and Design of Feedback Control Systems Spring 2014
For information about citing these materials or our Terms of Use, visit: http://ocw.mit.edu/terms.
