
# Peeking Behind the Curtains of Serverless Platforms

## About this paper:

- largest measurement study to date,
- launching more than 50,000 function instances across these three services (AWS Lambda, Azure Functions, and Google Cloud
Functions),
- in order to characterize their architectures, performance, and resource management efficiency
- explain how the platforms isolate the functions of different accounts, using either virtual machines or containers, which has important security implications
- characterize performance in terms of scalability, coldstart latency, and resource efficiency,

Highlights:
 - AWS Lambda adopts a bin-packing-like strategy to maximize VM memory utilization,
 - severe contention between functions can arise in AWS and Azure,
 - Google had bugs that allow customers to use resources for free
