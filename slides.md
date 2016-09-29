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

<video src="/home/clement/Images/lol/puppy-head.webm" loop></video>

<details>
Small autonomous teams. New projects can easily be started by cross-functional
teams, less time wasted on synchronisation
</details>

------------------------------------------------------------------------------

## Independent lifecycles

<video src="/home/clement/Images/lol/hamsters.webm" loop></video>

<details>
Independent release schedules, independent deployments. No more "stop the
world" releases

Maybe the most important thing to understand about microservices
</details>

------------------------------------------------------------------------------

## Compartimentalize failure

<video src="/home/clement/Images/lol/exploding-poo.webm" loop></video>

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

## Polyglot tech stacks

<details>
Language best suited for the task. Maybe it's a bash script to pilot a C
reverse proxy, or a JEE API, or a small scala service
</details>

------------------------------------------------------------------------------

## JEE

<details>
Main API complex HTTP API & data models
</details>

------------------------------------------------------------------------------

## JSE

<details>
Simple queue management, no HTTP API
will be eventually replaced by something more suited with streams
like akka streams
</details>

------------------------------------------------------------------------------

## Scala

<details>
data management api. good modelisation, good perf
</details>

------------------------------------------------------------------------------

## Node Js

<details>
small services, was very good at managing push stuff at some point.
slowly rewritten as well
</details>

------------------------------------------------------------------------------

## Ruby & bash

<details>
good for system scripting
</details>

------------------------------------------------------------------------------

## Rust

<details>
good fit for many things, will partly replace other languages
small footprint, easy to deploy
</details>

------------------------------------------------------------------------------


## Try new things

<details>
some services are less critical, they're the best place to experiment without
risk: I've written stuff in go, no I know why I won't use it any more
</details>

------------------------------------------------------------------------------

## Polyglot persistence

------------------------------------------------------------------------------

## No central data model

<details>
no more central data model
</details>

------------------------------------------------------------------------------

## Drop your SQL monolith

<video src="/home/clement/Images/lol/bungee.webm" loop></video>

------------------------------------------------------------------------------

## Different datastore scaling

<details>
multiple data stores with different capabilities / scaling needs and
possibilities
</details>

------------------------------------------------------------------------------

# <small>Keep your monolith</small>

<video src="/home/clement/Images/lol/2001.webm" loop></video>

<details>
There are reasons to stay on a monolithic arch
</details>

------------------------------------------------------------------------------

## Increased complexity

<details>
  - more deployments
  - hidden failure modes
</details>

------------------------------------------------------------------------------

## More deployments

------------------------------------------------------------------------------

## Tricky failure modes

------------------------------------------------------------------------------

## Can you afford microservices?

<details>
Are you ready for microservices ?
There are prerequisites
</details>

------------------------------------------------------------------------------

## Rapid provisionning

<video src="/home/clement/Images/lol/cats.webm" loop></video>

<details>
Lots of applications, designed to ease scale out => you need to make room for
a new instance very quickly
</details>

------------------------------------------------------------------------------

## Basic monitoring

<video src="/home/clement/Images/lol/computer-glasses-code.webm" loop></video>

<details>
Lots of application, you need to know when one fails.
</details>

------------------------------------------------------------------------------

# <small>Rapid application deployment</small>

![](./assets/catapult.gif)


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

<video src="/home/clement/Images/lol/chain.webm" loop></video>

------------------------------------------------------------------------------

## Automate builds

------------------------------------------------------------------------------

## <small>Automate config injection</small>

------------------------------------------------------------------------------

## Automate deployments

------------------------------------------------------------------------------

## <small>Automate whole env provisionning</small>

------------------------------------------------------------------------------

## Don't share state

<details>
Each microservice is responsible for its own state
no shared access to a DB
end of the "SQL store + multiple applications writing in it"
</details>

------------------------------------------------------------------------------

## Make state explicit

------------------------------------------------------------------------------

## No persistent local state

------------------------------------------------------------------------------

## Put sessions in a proper DB

------------------------------------------------------------------------------

## Use S3 for files

------------------------------------------------------------------------------

## Use explicit synchronization

<details>
don't write your own transaction system in mongodb
</details>

------------------------------------------------------------------------------

## <small>Use zk, etcd, consul for transactions</small>

------------------------------------------------------------------------------

## The hard parts

<details>
  Network is fragile, errors happen
</details>

------------------------------------------------------------------------------

## Complexity is still here

------------------------------------------------------------------------------

## Complexity is outside the code

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

## Make boundaries explicit

------------------------------------------------------------------------------

## ORMs

<details>
"vietnam of computer science"
</details>

------------------------------------------------------------------------------

## RMI

<details>
let's pretend the network doesn't exist
</details>

------------------------------------------------------------------------------

## <small>Hidden complexity == tech dept</small>

<details>
if a system seems less complex than its domain, then there's accidental
complexity hiding somewhere and you won't find it until it's too late
</details>

------------------------------------------------------------------------------

## Hexagonal architecture

<details>
Each microservice or DB is an implementation. Clear zoning. Your topology
manager does the plugging
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

------------------------------------------------------------------------------

## <small>Make micro-services topology-agnostic</small>

<details>
  - rabbitMQ instead of HTTP to make a service topology-agnostic
</details>

------------------------------------------------------------------------------

## Boundaries

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

## Language-specific serde

<video src="/home/clement/Images/lol/dog-stick-stuck.webm" loop></video>

------------------------------------------------------------------------------

## Breaks polyglotism

------------------------------------------------------------------------------

## Poor tooling and documentation

<video src="/home/clement/Images/lol/hammer.webm" loop></video>

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
serialization system
best contendent for a greenfield project
</details>

------------------------------------------------------------------------------

## Schema definition language

------------------------------------------------------------------------------

<small>
```json
{"namespace": "example.avro",
 "type": "record",
 "name": "User",
 "fields": [
     { "name": "name"
     , "type": "string"
     },
     { "name": "favorite_number"
     , "type": ["int", "null"]
     },
     { "name": "favorite_color"
     , "type": ["string", "null"]
     }
 ]
}
```
</small>

------------------------------------------------------------------------------

## Compact serialization

<details>
clever binary encoding
separated schema for better compression
</details>


------------------------------------------------------------------------------

<small><small><small><small>
```json
{"name": "Douglas",   "favorite_number": 42, "favorite_color": "red"}
```

```json
{"name": "Launcelot", "favorite_number": 12, "favorite_color": "blue" }
```

```
  Offset  00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F
00000000  0E 44 6F 75 67 6C 61 73 54 06 72 65 64           .DouglasT.red   
00000000  12 4C 61 75 6E 63 65 6C 6F 74 18 08 62 6C 75 65  .Launcelot..blue
```
</small></small></small></small>

------------------------------------------------------------------------------

## Cross-language

<details>
support in many languages
</details>

------------------------------------------------------------------------------

## Cross-paradigm

<details>
deserializes to json
codegen not mandatory
</details>

------------------------------------------------------------------------------

## Partial reading

------------------------------------------------------------------------------

```javascript
const resolver =
  partialSchema
    .createResolver(completeSchema);

const partialMessage =
  resolver
    .fromBuffer(
      completeBuffer,
      resolver,
      true);
```

------------------------------------------------------------------------------

## Schema evolution

------------------------------------------------------------------------------

## Protocol definition

------------------------------------------------------------------------------

```json
{
  "namespace": "com.acme",
  "protocol": "HelloWorld",
  "doc": "Protocol Greetings",
```

------------------------------------------------------------------------------

```json
  "types": [
    { "name": "Greeting",
      "type": "record",
      "fields": [
        {"name": "message",
         "type": "string"}
      ]
    },
```

------------------------------------------------------------------------------

```json
    {"name": "Curse",
     "type": "error",
      "fields": [
        {"name": "message",
         "type": "string"}
      ]
    }
  ],
```

------------------------------------------------------------------------------

```json

  "messages": {
    "hello": {
      "doc": "Say hello.",
      "request": [
        {"name": "greeting",
         "type": "Greeting" }],
      "response": "Greeting",
      "errors": ["Curse"]
    }
  }
}
```

------------------------------------------------------------------------------

# <small>Evolution strategies</small>

![](./assets/evolution.gif)

<details>
proper definition of boundaries will make clear when evolutions are local or
modify the communication protocol
</details>

------------------------------------------------------------------------------

# Stop-the-world

<video src="/home/clement/Images/lol/well-fuck.webm" loop></video>

<details>
more convenient if you can afford it (small number of parts affected, non
critical part, small traffic).
Stop everything, update, restart
</details>

------------------------------------------------------------------------------

## Two-step

<video src="/home/clement/Images/lol/blind-juggling.webm" loop></video>

<details>
Deploy a forward compatible evolution service by service
Remove transition code service by service
</details>

------------------------------------------------------------------------------

## Wrap up

------------------------------------------------------------------------------

## Automate

------------------------------------------------------------------------------

## Don't share state

------------------------------------------------------------------------------

## Don't ignore boundaries

# I'm online!

- [\@clementd](https://twitter.com/clementd) on twitter
- [cltdl.fr/blog](http://cltdl.fr/blog)
- [clever cloud](http://clever-cloud.com)

