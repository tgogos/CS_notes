
# Peeking Behind the Curtains of Serverless Platforms

## Abstract

About this paper:

- largest measurement study to date,
- launching more than 50,000 function instances across these three services (AWS Lambda, Azure Functions, and Google Cloud
Functions),
- in order to characterize their architectures, performance, and resource management efficiency
- explain how the platforms isolate the functions of different accounts, using either virtual machines or containers, which has important security implications
- characterize performance in terms of scalability, coldstart latency, and resource efficiency,

Highlights:
 - AWS Lambda adopts a **bin-packing-like strategy** to maximize VM memory utilization,
 - **severe contention** between functions can arise in AWS and Azure,
 - Google had **bugs** that allow customers to use resources for free

## Introduction

 - Serverless computing (or function-as-a-service, FaaS) is an emerging application deployment architecture that completely **hides server management from tenants** (hence the name).
 - *Isolation*: A function usually executes in a **dedicated function instance (a container or other kind of sandbox)** with restricted resources such as CPU time and memory.
 - *Event-driven*: Unlike virtual machines (VMs) in more traditional infrastructure-as-a-service (IaaS) platforms, a function instance will be **launched only when the function is invoked** and is put to sleep immediately after handling a request.

> Hiding resource management from tenants enables this programming model,

**but**

> the resulting opacity hinders adoption for many potential users, who have expressed concerns about:
> - security in terms of the quality of isolation, DDoS resistance, and more...
> - the need to understand resource management to improve application performance
> - and the ability of platforms to deliver on performance
