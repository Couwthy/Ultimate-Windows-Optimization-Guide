# Interrupt Affinity Policy Tool

## Understanding the Interrupt Affinity Policy Tool
- The 'Interrupt Affinity Policy Tool,' a Microsoft creation, empowers users to designate specific CPUs (threads) for device management. This guide details how to proficiently select suitable CPUs (threads) for your GPU and USB devices.

## Reliable Tool, Expert Handling Required

- Rest assured, this tool boasts a track record of safety across numerous computer systems. However, challenges may arise if used without a comprehensive understanding. Potential issues include: Latency issues, FPS Drops, Freezes, Stutters.

## How to set GPU & USB affinities

- First of all, you have to check if you have (ΗΤ) hyper threading & (SMT) Simultaneous Multithreading ON or OFF.

- I suggest to disable HT or SMT if you have at least 12 threads. Otherwise enable it.

## What difference does it make to the process if I have HT or SMT enabled or disabled

- If we have disabled HT or SMT then we will simply choose 1 CPU (thread).

# How it works Auto GPU Affinity

- Execute 'Auto Gpu Affinity' via the command-line, and hit 'Enter' to initiate the benchmarking process.

- Once the tool completes core benchmarking, GPU affinity will revert to the Windows default, and a results table will emerge. The xperf report resides in the designated session directory.

- Conduct a minimum of 3 tool runs. Should a single core consistently exhibit strong performance and the 0.005% Lows values align well with other outcomes, your results achieve reproducibility, confirming the consistency of your testing environment.

## After all the tests we did are completed, we head out to this path: “Auto Gpu Affinity\captures”.

- In each test we look at the 1% low & 0.1% low . If out of the 5 tests, 3 come out as the best CPU, for example CPU 1 is the best according 1% low and CPU 2 according 0.1% low and Max FPS .  Note! During the tests, the computer is not used and you have made sure that no unnecessary processes are running. In the case that you cannot get a result with 3 tests, continue to do the above benchmarks or try the previous method. Don't forget to put the affinity on the “PCI Express Root Port” beyond the GPU.

# How to set affinities for all USB devices

- In my opinion, what you should focus on is, the distance between the highest and the lowest frequency should be as small as possible, with this reasoning you will find the best affinity. There is no official way to find the best affinity for our USB devices. I think the primary goal is to stabilize the DPI of the mouse, keyboard or controller. For example, it should be as stable as possible at 1000 polling rate. However there are 2 obvious ways to find the best affinities. The first is with the Latency monitor to check if there are decreases or increases in latency after applying the changes. The second obvious and quite difficult way is to observe with our own eyes the experience we have in games, if for example it is smoother, with less delay, etc. The way I will show which is the most commonly accepted is by using the mouse tester. So this program helped us to see in a graph the frequency of our mouse.

## How to set affinities for Only 1 device

- Furthermore, certain tweakers suggest exploring both singular and collective device affinities. Their rationale is straightforward: associating more devices within a single affinity can contribute to increased latency. While I cannot definitively verify its efficacy, experimentation is encouraged. Illustrated in the image is my personal example, showcasing an assigned affinity for my mouse device.


