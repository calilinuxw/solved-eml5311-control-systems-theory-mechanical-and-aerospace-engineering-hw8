Download Link: https://assignmentchef.com/product/solved-eml5311-control-systems-theory-mechanical-and-aerospace-engineering-hw8
<br>
<em>You are encouraged to use MATLAB</em><sup> c </sup><em>to verify your answers whenever you can. However, unless specified, do not use MATLAB</em><sup> c </sup><em>to solve a problem.</em>

<strong>Problem 1. </strong>A plant is given as a SIMULINK<sup> c </sup>model plantForExperiment.xls. An example matlab script to define necessary variables and run a simulation with this plant is provided in runExperimentOnPlant.m. Write a MATLAB<sup> c </sup>script to identify the frequency response of the plant using the etfe method, by modifying the script I discussed in lecture 40, which is in Files <em>&gt; </em>resources <em>&gt; </em>code <em>&gt; </em>systemIdentification. Tasks:

<ol>

 <li>Add a feature to reduce the impact of initial conditions on estimation error (such a feature is absent in the MATLAB<sup> c </sup>script I provided and discussed in the lecture on using etfe).</li>

 <li>Repeat the identification for several types of inputs. Provide two figures: for the best identification results and worst identification results. Keep everything else the same in these two experiments except for the signal type. Also, make sure the input magnitude in all your experiments is within ±0<em>.</em></li>

 <li>In each of the two figures above, show both the estimate and the true frequency response. You can see what the true plant is by looking inside the SIMULINK<sup> c </sup> <em>Beware: As I discussed in the lecture, etfe estimates the discrete-time plant whose frequency response is slightly different from its continuous time counterpart, especially in higher frequencies. The simulink model is for a continuous-time system.</em></li>

</ol>

Submit: a brief description of the feature (item 1), not exceeding five sentences. The two figures mentioned above, and a brief description of which inputs you tried and which among them gave you the best and worst results, and why (not exceeding ten sentences).

<em>Hint: it turns out that the last 2 optional parameters in MATLAB</em><sup> c </sup><em>’s </em><em>etfe command are important to get good results in this problem. In the example covered in the lecture that was not necessary. Another key to getting good estimation is to drop some initial data to reduce the impact of initial conditions (the answer to part 1 of the question). Here is my code, as an example:</em>

……

uetfe=u(end-N+1:end); yetfe=y(end-N+1:end); idDataForThePlant = iddata(yetfe,uetfe,Ts); smoothingWindowSize = N/10;

Phat_DT = etfe(idDataForThePlant,smoothingWindowSize,numFreqRes); …

<strong>Problem 2. </strong>Estimate the frequency response of the plant <em>P</em>(<em>s</em>) mentioned in Problem 1 by using the sine sweep method. Use the same simulink model for performing experiments. Make sure the input magnitude in all your experiments is within ±0<em>.</em>6. <em>Hint: start with the script named </em>sineSweepExample withlsim forstudents.m <em>which is in Files &gt; resources &gt; code &gt; systemIdentification.</em>

Submit: (1) a Bode plot showing your estimated frequency response values and the true frequency response of <em>P</em>(<em>s</em>), (2) a brief description of how you decided which frequency values to perform sine sweep on (i.e., why those values) and your choice of various parameters such as number of cycles to average, duration of initial data to drop, etc. (2) Comment on the relative cost vs. benefit of the two methods (etfe vs. sine sweep) you see from your results. (3) Your matlab code, as a single .m file.

<em>Note: Since the solution to the problem is effectively already provided in the script </em><em>sineSweepExample withlsim forstudents.m,</em>

<em>the matlab script part of the solution to this problem will not be provided. You will need to run sine sweep on a plant provided in a simulink model form in the project. So you should write the MATLAB</em><sup> c </sup><em>script for this problem in a clean manner so you can reuse it for the project easily.</em>

<strong>Problem 3. </strong>[set point tracking, LQR, etc.] Do this using MATLAB<sup> c </sup>. Consider the following plant <em>P</em>(<em>s</em>) with input <em>u </em>and output <em>y</em>:

(1)

<em>It is almost the same as one the plant in HW7, except this plant is stable. </em>Your job is to design and output feedback controller for this plant by using a state observer and combining it with a state feedback controller <em>to track a constant reference (set point): r</em>(<em>t</em>) = 3 <em>for all t</em>, and simulate the closed loop. (use tf2ss to get a minimal realization of the plant for design.) You have to design the control system to achieve a certain performance that is specified below. Here are the tasks:

<ol>

 <li>Draw a sketch of the closed loop control system.</li>

 <li>Construct a SIMULINK model of the closed loop system. Write a MATLAB<sup> c </sup>script to initialize and define all parameters needed by the Simulink model, and also to run the model using the sim Choose a sufficiently long time to see transients die out, use the following initial conditions: <em>x</em>(0) = 10<sup>−3 </sup>× [5<em>,</em>5<em>,</em>5<em>,</em>5<em>,</em>−5]<em><sup>T</sup></em>, ˆ<em>x</em>(0) = 0. Use this initial condition for all subsequent simulations. <em>Hint: At this stage, don’t worry too much about tuning the controller for performance; just ensure that the closed loop is stable by using the pole placement method.</em></li>

 <li>Now refine the design to meet the following objective, or get close to it: “peak overshoot less than 100% and 2% settling time less than 10 seconds, while the control command <em>u</em>(<em>t</em>) less than 0<em>.</em>5 in magnitude for all <em>t</em>. Try the following two design methods for choosing <em>K</em>:

  <ul>

   <li>Pole placement: pick desired locations of controller poles (that is, eigenvalues of <em>A</em>−<em>BK</em>), and then use the place command to compute <em>K</em>.</li>

   <li></li>

  </ul></li>

</ol>

In both cases, determine <em>L </em>by using pole placement, and choose observer poles to be 5 times to the left of controller poles. The simplest way to do this is to simply multiply controller poles by

5, or add – 5*min(real(controller poles)) to the controller poles. <em>Note: I could not achieve the objective using pole placement, but I was able to do it with LQR in less than 2 minutes.</em>

Submit: (i) plots of the relevant outputs (<em>r </em>and <em>y </em>vs <em>t </em>in one figure, <em>u </em>vs. <em>t </em>in another), (ii) a picture of your simulink block, (iii) a brief description of your design process (not more than 5 sentences for each method, pole placement and LQR).

<strong>Problem 4 </strong>(open loop electromagnet)<strong>. </strong>Consider the following dynamic model of an electromagnetically suspended mass shown in the figure below

0                    (2)

where <em>d</em>(<em>t</em>) is the position of the mass, <em>I</em>(<em>t</em>) is the magnitude of the current through the electromagnet, <em>m </em>is the mass, <em>g </em>is the acceleration due to gravity, and <em>α </em>is a positive constant. Note that the electromagnet’s position is fixed, which determines the origin <em>d</em>(<em>t</em>) ≡ 0. The position <em>d</em>(<em>t</em>) is measured with an optical sensor, so it is an output. Finally, it should be emphasized that the model is valid only for positive values of <em>d</em>. The actuation signal or control command is the current <em>I</em>(<em>t</em>).

<ol>

 <li>Express the ODE in state space form <em>x</em>¯˙ = <em>f</em>(¯<em>x,u</em>¯) where ¯<em>u</em>(<em>t</em>) =<sup>∆ </sup><em>I</em>(<em>t</em>). Define your state vector ¯<em>x </em></li>

 <li>Determine all the equilibrium points (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) of this system.</li>

 <li>Suppose the desired position of the mass is <em>d</em><sub>0 </sub>(some positive constant). Determine the equilibrium point (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) corresponding to this desired position.</li>

 <li>Linearize the system around the equilibrium point corresponding to the desired position <em>d</em><sub>0</sub>. Is this linearized system internally stable/asymptotically stable? Do you need to know the numerical value of any parameter to answer this question?</li>

 <li>Is the equilibrium point (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) (corresponding to the desired position <em>d</em><sub>0</sub>) stable, asymptotically stable, or unstable (in the sense of Lyapunov), or is it not possible to say from the linearized system?</li>

</ol>

<strong>Problem 5 </strong>(open loop electromagnet – but now flipped up)<strong>. </strong>Consider the following dynamic model of an electromagnetically suspended mass shown in the figure below

0                                  (3)

where <em>d</em>(<em>t</em>) is the position of the mass, <em>I</em>(<em>t</em>) is the magnitude of the current through the electromagnet, <em>m </em>is the mass, <em>g </em>is the acceleration due to gravity, and <em>α </em>is a positive constant. <em>This magnet exerts a repulsive force on the mass to keep it suspended while the previous one exerted an attractive force. </em>Note that the electromagnet’s position is fixed, which determines the origin <em>d</em>(<em>t</em>) ≡ 0. The position <em>d</em>(<em>t</em>) is measured with an optical sensor, so it is an output. Finally, it should be emphasized that the model is valid only for positive values of <em>d</em>. The actuation signal or control command is the current

<em>I</em>(<em>t</em>).

<sup>∆</sup>

<ol>

 <li>Express the ODE in state space form <em>x</em>¯˙ = <em>f</em>(¯<em>x,u</em>¯) where ¯<em>u</em>(<em>t</em>) = <em>I</em>(<em>t</em>). Define your state vector ¯<em>x </em></li>

 <li>Determine all the equilibrium points (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) of this system.</li>

 <li>Suppose the desired position of the mass is <em>d</em><sub>0 </sub>(some positive constant). Determine the equilibrium point (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) corresponding to this desired position.</li>

 <li>Linearize the system around the equilibrium point corresponding to the desired position <em>d</em><sub>0</sub>. Is this linearized system internally stable/asymptotically stable? Do you need to know the numerical value of any parameter to answer this question?</li>

 <li>Is the equilibrium point (¯<em>x<sub>eq</sub>,u</em>¯<em><sub>eq</sub></em>) (corresponding to the desired position <em>d</em><sub>0</sub>) stable, asymptotically stable, or unstable (in the sense of Lyapunov), or is it not possible to say from the linearized system?</li>

</ol>

<em>Hint: the linearized system in the previous problem (attractive electromagnet) is unstable, while this one (repulsive) is stable.</em>

<strong>Problem 6 </strong>(A more realistic electromagnet model)<strong>. </strong>In practice, the current cannot be directly commanded, it is generated by using a voltage source. The voltage of the voltage source, <em>V<sub>s</sub></em>(<em>t</em>), can be commanded to take any desired value within a range<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. The coil in the electromagnet acts as an inductor and resistor connected in series, forming a so-called R-L (resistor inductor) circuit. The equation for the electrical circuit is

(4)

where <em>R </em>is the electrical resistance and <em>L </em>is the inductance of the coil. So, the actuation or control command is <em>V<sub>s</sub></em>, the current <em>I </em>is in fact an internal state. Consider such a current source powering a “vertically up” electromagnet of Problem 5, whose position is governed by

)                                     (5)

where <em>β &gt; </em>0 is a drag coefficient.

Figure 1: Control system: left of the dashed line is the “controller”.

<ol>

 <li>Derive a state-space model of the system (that is, equations (4)-(5)) the form <em>x</em>¯˙ = <em>f</em>(¯<em>x,u</em>¯),</li>

</ol>

∆ <em>y</em>¯ = <em>h</em>(¯<em>x,u</em>¯), where ¯<em>u </em>= <em>V<sub>s </sub></em>and ¯<em>y </em>= <em>d</em>. Use the following state: ¯ .

<ol start="2">

 <li>Compute all the equilibrium points of the system corresponding to a constant position <em>d</em><sub>0</sub>. (<em>both the equilibrium position and the equilibrium current have to be positive.</em>)</li>

 <li>Derive an LTI approximation around this equilibrium point. Is this equilibrium point stable, unstable, or “not possible to say from the linearization”?</li>

</ol>

<strong>Problem 7 </strong>(Closed loop electromagnet)<strong>. </strong>Consider the “vertically up” electromagnet model described in the previous problem. Suppose we wish to use a dynamic compensator to control the mass position.

∆ The reference for the mass position is denoted by ¯<em>r</em>(<em>t</em>). Define the deviation control input <em>u</em>(<em>t</em>) = <em>u</em>¯ − <em>u</em>¯<em><sub>eq</sub></em>, where ¯<em>u<sub>eq </sub></em>was the input part of the equilibrium point you derived in the previous problem (corresponding to the desired position being <em>d</em><sub>0</sub>). The control command <em>u</em>(<em>t</em>) is to be computed by a linear dynamic compensator <em>C</em>(<em>s</em>):

∆                                                <sup>∆                                         ∆</sup>

<em>U</em>(<em>s</em>) = <em>C</em>(<em>s</em>)<em>E</em>(<em>s</em>)<em>,</em>where <em>e </em>= <em>r</em>(<em>t</em>) − <em>y</em>(<em>t</em>)<em>, y</em>(<em>t</em>) = <em>d</em>(<em>t</em>) − <em>d</em><sub>0</sub><em>,r</em>(<em>t</em>) = ¯<em>r</em>(<em>t</em>) − <em>d</em><sub>0</sub>

Figure 1 shows the control architecture (discussed in class) for implementing the controller <em>C</em>(<em>s</em>) to control this nonlinear plant

<ol>

 <li>If a compensator <em>C</em>(<em>s</em>) is provided to you, is it possible to implement the controller (in hardware, not simulation) without knowing the the parameters <em>m,α,d</em><sub>0</sub><em>,L,β</em>?</li>

 <li>Suppose <em>α </em>= 10<sup>−4 </sup>Nm<sup>2</sup>/A<sup>2</sup>, <em>m </em>= 0<em>.</em>5 Kg, <em>g </em>= 9<em>.</em>81 m/s<sup>2</sup>, <em>R </em>= 50Ω, <em>L </em>= 0<em>.</em>015 H (Henry), <em>d</em><sub>0 </sub>= 0<em>.</em>1 m, <em>β </em>= 0<em>.</em>5 kg/s<sup>3</sup>. Design a compensator <em>C</em>(<em>s</em>) so that the desired equilibrium point of the <em>closed loop </em>nonlinear system is asymptotically stable. (The “desired equilibrium point” is the one that corresponds to the position being <em>d</em><sub>0</sub>. <em>Hint: use MATLAB</em><sup> c </sup><em>´s </em><em>sisotool to design a controller to make the linear closed loop CP/</em>(1+<em>CP</em>) <em>stable, where P is the linearized plant. Then argue why that also makes the equilibrium point of the nonlinear closed loop stable. Remember that the plant P</em>(<em>s</em>) <em>only exists in your mind, the actual plant is nonlinear.</em></li>

 <li>Perform a closed-loop simulation with the nonlinear plant and your controller. <em>A SIMULINK</em><sup> c </sup><em>model of the plant is provided in </em><em>plant ElectromagnetUpward.slx. You have to add to it to make it look like Figure 1. The blocks inside the plant expects you to define the parameters m,α etc., so be consistent. </em>Use the reference to be ¯<em>r</em>(<em>t</em>) = <em>d</em><sub>0</sub>, and start with the initial condition <em>x</em>¯(0) = ¯<em>x<sub>eq</sub></em>. Then vary the initial condition to see how well the closed loop behaves as the initial condition varies away from the equilibrium point. Once it varies sufficiently, the non-linear closed loop system may become unstable. If that happens, comment on how different ¯<em>x</em>(0) could be from the equilibrium point before you observed instability.</li>

</ol>

<em>What to submit </em>For part 1, submit a brief explanation. For part 2, specify the controller <em>C</em>(<em>s</em>) and how you obtained it (a sentence summary will suffice, such as “PID tuning method in sisotools”), the closed loop simulation with the linear plant <em>P</em>, and the Bode plot of the closed loop transfer function, a Bode plot of the loop gain <em>L </em>with gain and phase margins marked, and for Part 3, provide simulations plots with ¯<em>r</em>(<em>t</em>) and ¯<em>y</em>(<em>t</em>) vs. <em>t</em>, and ¯<em>u</em>(<em>t</em>) vs. <em>t</em>. Dont forget to add the discussion about the initial condition mentioned in part 3. The discussion of the comparison between the actual nonlinear system and should be based on a figure that shows (in the same figure) ¯<em>y</em>(<em>t</em>) from the simulation of the closed loop nonlinear system and ¯<em>y</em>(<em>t</em>) that is predicted by the closed loop with the linearized plant (i.e., compute <em>y</em>(<em>t</em>) from the closed loop system with plant <em>P</em>(<em>s</em>) and controller <em>C</em>(<em>s</em>), and add <em>d</em><sub>0</sub>).

optional (not graded)

<strong>Problem 8. </strong>Consider the following non-linear ODE model for the spread of Coronavirus in a population:

)                    (6)

)                                                                                     (7)

Read the document CoronaVirusModel.pdf in e-learning Files<em>&gt; </em>Resources <em>&gt; </em>coronaVirusNotes to understand the model, and then use a first order Euler method to discretize the ODEs and numerically compute the solution<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>. Note that if the ODE is ˙<em>x </em>= <em>f</em>(<em>x</em>), the first order forward Euler is <em>x<sub>k</sub></em><sub>+1 </sub>= <em>x<sub>k </sub></em>+ ∆<em>tf</em>(<em>x<sub>k</sub></em>). Tasks:

<ol>

 <li>Look at the original paper by Gotz where the model came from to obtain the values of the parameters <em>θ,µ,σ,N</em>. For <em>θ</em>, use the value 0<em>.</em>3056. Use the initial condition <em>I</em>(0) = 800<em>,R</em>(0) = 0. 2. Determine the unit of <em>θ</em>.</li>

 <li>(“Extra credit”) Repeat the first exercise for the time-varying model of Gotz (see eq. 3 in the CoronaVirusModel.pdf) to produce the solution that Gotz obtained, that is shown in Figure 2 of the document (Figure 7 of the paper by Gotz). You will have to estimate <em>θ</em><sub>1 </sub>from the data he provides, or make an educated guess. The value of <em>θ</em><sub>2 </sub>can be obtained from the last equation of Gotz’s paper.</li>

</ol>

Plot your solution and compare with the data on “Cumulated cases” from China that Gotz uses. (see again Gotz’s paper for the definition of “Cumulated cases”.) If your plot looks quite different from Gotz’s, try tuning the the value of <em>R</em>(0) to a small positive number (that is consistent with the definition of <em>R</em>(<em>t</em>) and <em>I</em>(<em>t</em>)) to see if you can get results that are close to Gotz’s. <em>Beware of the unit of t: some automatically assume t is in seconds in performing simulations, which is not correct. Here that mistake will cost you. The units of the parameters and the x-axis of the plots in Gotz’ paper will help you in figuring out the time unit.</em>

<a href="#_ftnref1" name="_ftn1">[1]</a> There are many ways of doing it. One can connect a battery with a constant voltage to a voltage divider. A better method is to use a solid state voltage regulator in place of the voltage divider, which uses pulse width modulation to deliver an effective voltage that is equal to the commanded voltage <em>V<sub>s</sub></em>(<em>t</em>).

<a href="#_ftnref2" name="_ftn2">[2]</a> The notes were written in March/April 2020; I have not updated them. But the points I am making in the notes remain valid today. You will also notice that the model described above is slightly different from that reported by Gotz in his paper. That is because when I simulated the model myself, my plot did not look anything like what Gotz reported in his paper. So I emailed him asking what the heck is going in. And he replied, saying, “sorry, there was a typo: <em>θ </em>in 2(a) should be <em>θ/N</em>” !!