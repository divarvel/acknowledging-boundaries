% Acknowledging boundaries.
% Clément Delafargue / [Clever Cloud](http://clever-cloud.com)
% 2016-09-28

------------------------------------------------------------------------------

# Acknowledging boundaries


<div style="margin-top: 300px; font-size: 1.5em; text-align: center;">
Bring back consistency in your microservices architecture
</div>

------------------------------------------------------------------------------

# I'm online!

 - [\@clementd](https://twitter.com/clementd) on twitter
 - [cltdl.fr/blog](http://cltdl.fr/blog)
 - [clever cloud](http://clever-cloud.com)


-------------------------------------------

![](assets/clever-16-9.png)

<details>
we used microservices early on, with one service less micro than the other
</details>

------------------------------------------------------------------------------

## Microservices

<details>
show of hands
who knows what they are?
who's using them?
</details>

------------------------------------------------------------------------------

<video src="/home/clement/Images/lol/but-why.webm" loop></video>

<details>
what's the problem with monoliths? Why add complexity?
</details>

------------------------------------------------------------------------------

## Separation of concerns

<details>
Avoid duplication of business logic
</details>

------------------------------------------------------------------------------

## Smaller codebases

<details>
Easier to understand
</details>

------------------------------------------------------------------------------

## Smaller teams

<details>
Small autonomous teams. New projects can easily be started by cross-functional
teams, less time wasted on synchronisation
</details>

------------------------------------------------------------------------------

## Independent lifecycles

<details>
Independent release schedules, independent deployments. No more "stop the
world" releases

Maybe the most important thing to understand about microservices
</details>

------------------------------------------------------------------------------

## Polyglot tech stacks

<details>
Language best suited for the task. Maybe it's a bash script to pilot a C
reverse proxy, or a JEE API, or a small scala service
</details>

------------------------------------------------------------------------------

## Good for polyglot persistence

<details>
no more central data model
end of the monolithic SQL db
multiple data stores with different capabilities / scaling needs and
possibilities
</details>

------------------------------------------------------------------------------

## Compartimentalize failure

<details>
If a part of your system is hanging (typically HTTP thread exhaustion, it
doesn't bring your whole system down)
</details>

------------------------------------------------------------------------------

## Allow different scaling policies

<details>
  simple stateless part of the system can scale out
  big stateful part can scale up
  parts that are harder to scale are stripped down to control their growth
</details>

------------------------------------------------------------------------------

## Don't use microservices if

<details>
  - complexity
  - more deployments
  - hidden failure modes
</details>

------------------------------------------------------------------------------

## Can you afford microservices?

<details>
Are you ready for microservices ?
There are prerequisites
</details>

------------------------------------------------------------------------------

## Rapid provisionning

<details>
Lots of applications, designed to ease scale out => you need to make room for
a new instance very quickly
</details>

------------------------------------------------------------------------------

## Basic monitoring

<details>
Lots of application, you need to know when one fails.
</details>

------------------------------------------------------------------------------

## Rapid application deployment


<details>
Easy rollback / restart on failure. Scaling out quickly reduces the degraded
quality during traffic surges
</details>

------------------------------------------------------------------------------

## 12factor

<details>
Go farther than the 3 core requirements. 12 factor is completely suited for
microservices architectures
</details>

------------------------------------------------------------------------------

## Automate everything

<details>
  - automate deployments
  - automate builds
  - build / configuration separation
  - independent apps
  - test environnements
  - service dependencies
</details>

------------------------------------------------------------------------------

## Don't share state

<details>
Each microservice is responsible for its own state
no shared access to a DB
end of the "SQL store + multiple applications writing in it"
</details>

------------------------------------------------------------------------------

## Use explicit synchronization

<details>
Each microservice is responsible for its own state
no shared access to a DB
end of the "SQL store + multiple applications writing in it"
</details>

------------------------------------------------------------------------------

## The hard parts

<details>
  Network is fragile, errors happen
</details>

------------------------------------------------------------------------------

## Know your failure modes

<details>
Where will your system break?
If service A breaks, what will it take down?
If service A is dead slow, what will it make slow?
</details>

------------------------------------------------------------------------------

## Know if a call is local or distant

<details>
If you feel like you're doing RPC everywhere, then your boundaries are likely
bad
</details>

------------------------------------------------------------------------------

## Know your topology

<details>
You MUST know how services relate to each other, where network is involved.
Semantic topology. a docker-compose.yml or a kubernetes JSON config file is
not a proper way to define a topology, the same way that a makefile does not
describe your business model
</details>

------------------------------------------------------------------------------

## Make topology explicit

<details>
Don't use stacks that fake locality in order to ease the use of microservices.
If you're hiding essential complexity, it can only be by creating accidental
complexity
</details>

------------------------------------------------------------------------------

## Make micro-services topology-agnostic

<details>
  - rabbitMQ instead of HTTP to make a service topology-agnostic
</details>

------------------------------------------------------------------------------

## Complexity doesn't magically disappear

<details>
  - complexity exists at boundaries
  - complexity lies in interactions
</details>

------------------------------------------------------------------------------

## Document interactions

<details>
  - document and specify interactions
</details>

------------------------------------------------------------------------------

## Know your protocols

<details>
  - for HTTP, endpoints and representation structures
  - for message brokers, exchanges / queue names / topics / …
  - shared protocols description
  - at the very least serialization & data types
</details>

------------------------------------------------------------------------------

## Serialization

------------------------------------------------------------------------------

## Avoid language-specific serialization

------------------------------------------------------------------------------

## Breaks polyglotism

------------------------------------------------------------------------------

## Poor tooling and documentation

------------------------------------------------------------------------------

## Extended attack surface

------------------------------------------------------------------------------

## JSON schema

<details>
  representation structure
</details>

------------------------------------------------------------------------------

## Swagger / RAML

<details>
  endpoints
  integrates document structure
  API explorer
  client generation
</details>

------------------------------------------------------------------------------

## Avro

<details>
  apache serialization language
  protocol definition
  schema evolution
</details>

------------------------------------------------------------------------------

## Evolution strategies

<details>
proper definition of boundaries will make clear when evolutions are local or
modify the communication protocol
</details>

------------------------------------------------------------------------------

## Stop-the-world

<video src="/home/clement/Images/lol/well-fuck.webm" loop></video>

<details>
more convenient if you can afford it (small number of parts affected, non
critical part, small traffic).
Stop everything, update, restart
</details>

------------------------------------------------------------------------------

## Forward-compatible update

<details>
Deploy a forward compatible evolution service by service
Remove transition code service by service
</details>

# I'm online!

- [\@clementd](https://twitter.com/clementd) on twitter
- [cltdl.fr/blog](http://cltdl.fr/blog)
- [clever cloud](http://clever-cloud.com)

