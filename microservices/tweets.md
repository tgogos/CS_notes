# complexity for velocity?
Microservices trade **complexity for velocity**. While achieving the latter is not guaranteed, the former always is! [tweet](https://twitter.com/bibryam/status/1172050320442241026)

![](./imgs/uber_microservices_graph.jpg)



# CPU burn
\- The thing that nobody talks about with the whole **sidecar pattern** is how much CPU it burns. If you're moving a lot of data in/out through the proxies it can be non-trivial. Adding 10-15% to your compute budget is a serious ask.

\- I dunno - folks using a sidecar often **tradeoff latency and efficiency for ... developer productivity**. That’s always how I’ve rationalized it.
[tweet/discussion](https://twitter.com/copyconstruct/status/1171646790610894849)



# ability to scale VS ability to be agile & survive
Forget that all these things exist: Microservices, Lambda, API Gateway, Containers, Kubernetes, Docker. Anything whose main value proposition is about **“ability to scale”** will likely trade off your **“ability to be agile & survive”**. That’s rarely a good trade off." [thread](https://twitter.com/dvassallo/status/1154516910265884672)



# Discussion (June 2019)
\- Service meshes provide a lot of value, especially around **encryption** and **observability**. I question, though, whether circuit breaking/timeouts/retries should be externalized (deferred) to the network. [Thread](https://twitter.com/embano1/status/1142188360192208896)

...

\- It requires a **mature engineering organization** to develop standards and best practices, as well as complying with them, around the problem of reliability and correctness in distributed communication.
