# FIFA-World-Cup-2026-case-study
This repository is done by Luxury-tech's Cloud Engineer Yasser Alaa as a demonstration to explain the technology behind Tod's outstanding performance during World Cup 2026

## Overview
### During the past FIFA World cup 2026, many of us has witnessed a unique case, watching a match over a pirated broadcast website comes with the worst experience possible, almost every non cloud technical specialist thinks it's because of the connection speed, but the legit streamers ( like TOD) providing great UX on the same connection, so how is this possible? 

As a cloud architect represents an information technology company, I'll explain in this repository how that works, dismantle the complexity so that CEO's, CTOs, CFOs and every decision  maker can understand how this happened. 

## The common thought
### As mentioned above, almost every None cloud engineer thinks this is an internet issue, and they think having stable or fast connection is enough to have the best UX, and with the World cup experience, this common thought has been shuttered when almost all of the users whom have best connection and tried to watch a match on a pirated stream website they had horrible UX, Now they suspect of the connection, issues, Now I want to affirm, It's NOT internet or connection issue, it's an infrastructure issue.

## The Technical difference between pirated streams websites and legit websites. 
### The Legit distributors:- Hosting isn't having a server, servers are one piece of the puzzle, if we wanted to represent the infrastructure with the human part, the servers will only be the brain, you'll need a neural system, and that's the networking, you'll a memory, and that's the storage, you'll need an immunity system, and that's security, The legit providers have teams deeply understand these concepts, and able to utilize the cloud provided services like orchestra to  get the best quality possible for their users.

### The pirated distributors:- They might have the knowledge to apply the concepts that provides the same UX quality, but they Don't have the means to apply it, All they can do is having an offshore servers, datacenters in places don't obliged by the copyrights roles, but edge locations around the world, no Global accelerators services, which is the service that takes the connection out of the public internet through privet AWS fiber, or it's equalvent from Google cloud or Azure cloud, you can imagine how this improve the connection.
## Also, During a World Cup kickoff, millions of connection requests hit the authentication and routing tier simultaneously. Legit broadcasters utilizes managed, auto-scaling ingress controllers (like AWS Application Load Balancers) and containerized orchestration (Amazon EKS) to instantly distribute this traffic across healthy backend nodes. 
## Illicit architectures rely on static, centralized load balancers (like a basic NGINX reverse proxy on a dedicated server). When the concurrent connection limit of that single proxy is reached, the routing tier crashes, taking the entire streaming network offline, even if the backend media servers have available capacity

