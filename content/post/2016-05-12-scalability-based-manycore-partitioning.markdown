---
author: yulistic
comments: true
date: 2016-05-12 06:49:06+00:00
layout: post
link: http://yulistic.com/?p=61
slug: scalability-based-manycore-partitioning
title: Scalability-Based Manycore Partitioning
wordpress_id: 61
language:
- English
topics:
- Paper
---

0. Environment
Many-core system with multiple multi-threaded applications.

1. Contribution

The paper suggests SBMP (Scalability-Based Manycore Partitioning) scheduler which considers the scalability of each application and allocates the best number of CPU cores in accordance with the scalability. SBMP scheduler outperformed the traditional Linux CPU scheduler (kernel version of 2.6.37.6) about 11%.

2. Problem to solve
The system is anticipated to get more number of cores. As the number of cores increases, multiple applications will run on the system simultaneously. Also, there are multiple threads in one application. On the other hand, all the applications have different scalability but the traditional OS (Linux) CPU scheduler does not consider the scalability of each application, even though scalability of an application is one of the critical features to the CPU cores scheduling. With the trends of multiple multi-threaded applications running on one machine, the scalability of applications gets more important, so a new CPU scheduler that considers the scalability of applications is required.

3. Suggested idea

There  are four techniques introduced in the paper.  Those are 1) Scalability Prediction 2) Core Partitioning 3) Core Donation and 4) Re-partitioning algorithm. The whole process of SBMP scheduler is like below.

[caption id="attachment_62" align="aligncenter" width="604"][![SBMP scheduler](http://yulistic.com/wp-content/uploads/2013/08/SBMP-scheduler-1024x217.png)](http://yulistic.com/wp-content/uploads/2013/08/SBMP-scheduler.png) SBMP scheduler[/caption]

1) Scalability Prediction

This process is to extract the scalability of each application. The process devises a new model based on the existing Amdahl's Law. Only three samplings for each application produces the scalability graph of the application.

2) Core Partitioning

As the scalabilities of all the applications are collected, the scheduler finds out the best partitioning of 48 cores to the applications currently running. Average of Normalized Turnaround Time is used for the value to find out the best partitioning and the Hill Climbing algorithm is used to find out near optimal assignment.

3) Core Donation

Until now, one core is assigned only for one application. By the way, there is an application having low CPU utilization and it makes cores to be wasted when the application does nothing. To increase the CPU utilization is important because it is the basic metrics for the CPU performance. To increase the overall CPU utilization SBMP scheduler takes some technique: Core Donation. When the core does nothing, the application from the other core runs on it. As a result, the core does not wasted. The overhead of the shared cache system is covered by the benefit from the increased CPU utilization.

4) Re-partitioning algorithm

By 1), 2), and 3) the partitioning is finished. The partition is hold until some event occur. The trivial one is the creation or termination of the program. The other one is phase change of the application. An application can have different scalability dynamically. SBMP scheduler detect those changes and re-partition the CPU.

4. Result and Summary

With the full SBMP scheduler, the performance improved 11% over the traditional Linux CPU scheduler (without Core Donation: 8%, with Core Donation: 11%).

5. Critical review

All the application have at lease 48 threads to utilize all the cores in the system. But some application might not need those large number of threads. The experiment with the application which was aimed to use more than 48 cores will enhance the support.
