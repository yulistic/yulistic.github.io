---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
type: post
link: http://yulistic.com/?p=29
slug: progress-1-flicker-a-dynamically-adaptive-architecture-for-power-limited-multicore-systems
title: '[Progress #1] Flicker: A Dynamically Adaptive Architecture for Power Limited
  Multicore Systems'
wordpress_id: 29
language:
- English
topics:
- '[Progress]'
- Paper
---

0. Environment
Future general purpose multicore system.

1. Contribution
It suggests a new approach that efficiently finds a near-global optimum configuration of finer-grained power gating (unit of _lane_, explained below) without requiring offline training, microarchitecture state, or foreknowledge of the workload. Due to  its purely online black-box approach, the Flicker control algorithm (global optimization algorithm) adapts on-the-fly to different machine microarchitectures and to machines that run a wide variety of applications.

2. Problem to solve
The paper deals with the problem of optimizing the performance of general-purpose multicore architectures that must efficiently adapt to varying, and at times highly stringent, power allocations.

3. Suggested idea
The paper suggests a new microarchitecture, _Flicker_, which dynamically adapts to varying and potentially stringent limits on allocated power. _Lane_ is a horizontal pipeline slices. It provides finer granularity for power-gating comparing to the core-level power gating. Also, the overhead of controlling lanes is far less than microarchitecture adaptation approach[1] which controls resources of each core separately.

To exploit _Flicker_'s architecture, three algorithms are introduced, which are 1) reduced sampling techniques, 2) application of response surface models to online optimization, and 3) heuristic online search.

4. Result and Summary

The global controller proposed in Flicker determine within a reasonably small fraction of a time slice the combination of powered lanes within the different cores that maximizes performance given the current power budget. It reveals better performance than the core-level gating approach when the power constraint is stringent with reasonable overheads.

5. Critical review

In the paper, there is little information of the overhead from heuristic algorithm. As the number of cores increases the overhead will increase exponentially. It is required to consider the scalability of the proposed approach.
