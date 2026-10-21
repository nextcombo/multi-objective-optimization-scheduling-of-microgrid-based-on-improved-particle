# Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code Implementation)

🏆 Bloggers' Advantage: 🌞🌞🌞 The content of the blog strives to be rigorous in thought and clear in logic, for the convenience of readers.
⛳️ Mantra: The journey of a hundred miles is half done in the last ninety.
📋📋📋This article's table of contents is as follows: 🎁🎁🎁
💥1 Overview of References:
​  
Microgrid optimization scheduling, as an important component of smart grid optimization, plays a significant role in reducing energy consumption and environmental pollution. The development goals of microgrids should not only meet the basic needs for power supply but also enhance economic benefits and environmental protection. To this end, we propose a multi-objective optimization model for microgrid integration that takes into account both the operational costs and environmental protection costs of the microgrid system. This model is solved using an improved particle swarm optimization algorithm. Simulation results show that this model can effectively reduce electricity costs and environmental pollution for users, promote the optimized operation of microgrids, and validate the superior performance of the improved particle swarm algorithm. Microgrid optimization scheduling refers to arranging different DG outputs reasonably under various system constraints to ensure optimal operation of the microgrid and its integration with the main grid.
The transmission power between the two sides, in order to achieve different goals such as low operating costs, low emissions, high reliability, high power generation efficiency and so on. For the demand side, the optimization dispatch of microgrid can effectively reduce the electricity cost for users. For the power supply side, microgrid optimization scheduling can improve.
The stability of the power grid, reducing energy loss and environmental pollution in power production. Therefore, optimizing the dispatch of microgrids is of great importance.
Realistic significance.
1.1 Distributed power sources and energy storage characteristics within microgrids
Editor
Editor
1.2 Multi-objective Optimization Model for Microgrids
Editor
This article considers the improved particle swarm algorithm with inertia factor and particle adaptive mutation to solve it📚2 Running results
Editor
Editor
Editor
Editor
Editor
Editor
Editor
Editor
🌈3 Matlab code implementation:
%% Initialize parameters
global PV;  
global WT;  
% Maximum discharge power of the battery (positive indicates power supply for load, i.e., discharging)
BESSMax_dischar = 30;
% Maximum charging power of the battery
BESSMax_char = -30;
% Maximum power generation of the diesel engine
DEMax = 30;
% Minimum power generation of the diesel engine
DEMin = 6;
% Maximum power generation of the gas turbine
MTMax = 30;
% Minimum power generation of the gas turbine
MTMin = 3;
% Maximum power exchange between the main grid (positive indicates power supply for load)
GridMax = 30;
% Minimum power exchange between the main grid
GridMin = -30;
% Initialization of the population
if nargin == 0
    c = [0.1, 0.2]; % Acceleration factor
    iw = [0.5, 0.001]; % Inertia factor
    max_iter = 100; % Maximum iterations
% Power output constraints for each device
for n = 1:144 % Particle length is 144 (PV, wind power, energy storage, diesel, gas turbine, and the 6*24 hours power output of the main grid)
    if n < 25
        lower_bound(n) = 0;
        upper_bound(n) = PV(n);
    end
    if n > 24 && n < 49
        lower_bound(n) = 0;
        upper_bound(n) = WT(n-24);
    end
    if n > 48 && n < 73
        lower_bound(n) = BESSMax_char;
        upper_bound(n) = BESSMax_dischar;
    end
    if n > 72 && n < 97
        lower_bound(n) = DEMin;
    end
upper_bound(n) =DEMax;  
end  
if n>96&&n<121  
lower_bound(n)=MTMin;  
upper_bound(n) =MTMax;  
end  
if n>120  
lower_bound(n)=GridMin;  
upper_bound(n) =GridMax;  
end  
end  
swarm_size=100; % population size
rep_size=100; % Archive repository size
grid_size=7; % Each dimension's grid number
alpha=0.1; % Inflation rate
beta=2; % Leadership selection pressure
gamma=2; % Delete selection pressure
mu=0.1; % Variation rate
Problem = @prob; % Create a function handle for Problem, Function is pro, can be simply understood as calling
end  
%% Initialize particles
fprintf('Initializing the population...\n')
w = @(it) ((max_iter - it) - (iw(1) - iw(2)))/max_iter + iw(2); % Update inertia factor -- Improved Particle Swarm Optimization
pm = @(it) (1-(it-1)/(max_iter-1))^(1/mu); % Similar to genetic algorithm, introduce mutation operation and update the mutation rate, in particle function's 78-84 lines.
swarm(1, swarm_size) = Particle(); % Call the Particle function to get swarm_size from obj.
for i = 1:swarm_size  
swarm(i) = Particle(lower_bound, upper_bound, problem); % Call the Particle function
retry = 0;  
While swarm(i).infeasablity > 0 && retry < 100 %, the loop condition is: there are no infeasible solutions and the number of attempts is less than 100.
swarm(i) = Particle(lower_bound, upper_bound, problem); % Call the Particle function
retry = retry + 1;  
end  
end  
REP = Repository(swarm,rep_size,grid_size,alpha,beta,gamma); % Call the Repository function
%% Algorithm loop
fprintf('Optimization algorithm starts in the loop\n')
for it=1:max_iter  
leader = REP.SelectLeader(); % Select leader
wc = w(it); % Current inertia factor
pc = pm(it); % Current mutation factor
for i = 1:swarm_size % update the population
swarm(i)=swarm(i).update(wc,c,pc,leader,problem);  
end  
REP = REP.update(swarm);  
Title = sprintf('Iteration %d, number of non-dominant solutions in archive library = %d', it, length(REP.swarm));
PlotCosts(swarm, REP.swarm, Title) % Call the following PlotCosts function
disp(Title);  
end  
🎉4 References  
[2] Hu Zhiqiang. Research on Multi-Objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm [D]. Nanchang University, 2020. DOI:10.27232/d.cnki.gnchu.2020.002673.

## Images

![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](01.gif)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](02.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](03.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](04.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](05.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](06.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](07.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](08.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](09.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](10.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](11.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](12.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](13.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](14.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](15.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](16.png)
![Multi-objective Optimization Scheduling of Microgrid Based on Improved Particle Swarm Algorithm (Matlab Code)](17.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
