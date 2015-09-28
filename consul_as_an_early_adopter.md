Consul as an early adopter
==========================

Nelson Elhage at Stripe (tech lead for infrastructure)

Previously using puppet and custom hacks (ruby service registry)

Implementing health monitoring to catch issues before they become a problem

Saw a lot of instability in raft early on. "consul not optimizied for platter drives"

Main stripe product (api) started using consul at startup for service discovery.

consul-template service watches generates a lot of churn. Watching a large amount of services causes a bit of a self-ddos. consul-template -once, on cron. Little more latency in updates, but less thrashing when updates occur.

Due to leaks and other issues with early consul, Stripe decided to only use consul for service-discovery. 

Used consul-template to generate zone file and served that out of normal dns server. Instead of using consul's built in dns

All services at Stripe are registered in consul, operations tools use the consul http interface.

consul-template is used for all haproxy config and other config files.

All memory leaks that Stripe experience were fixed in 0.5.2, consul-template watches are still broken for them, but 0.6 was promised to help.


