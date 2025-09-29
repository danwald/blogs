---
title: "DDD: Summary"
datePublished: Mon Sep 29 2025 17:14:26 GMT+0000 (Coordinated Universal Time)
cuid: cmg5e20g7000102lehok8cxnx
slug: ddd-summary
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1754724715565/5349e204-4d97-40a4-b3f0-877445e9f6ea.png
tags: design, architecture, domain-driven-design

---

Here is a summary / cliff’s notes of the [Domain Driven Design Quickly](http://www.infoq.com/minibooks/domain-driven-design-quickly) eBook

* **Domain** is what you trying to encode for which is owned by domain experts/specialist of the area
    
* The **domain model** is an *abstraction* represents the domain you’re trying to capture from the owners
    
* The *domain model* should be described and communicated within a **ubiquitous language**
    
* An **analyst model** is independently derived from the domain not considering software and design
    
* **Layers of DDD**: *UI; Application; Domain; Infrastructure;*
    
* **Entities** are *components* that have *identities* and are *mutable*
    
* **Value Objects** are *immutable attributes* or *components* that enrich entities and immutable
    
* **Aggregates** is a single unit of change that own several entities of a domain model
    
* An **Aggregate root** is an entity conduit for external requests policing change to a model
    
* **Services** provide functionally at the application level or domain level with Aggregates
    
* **Factories** are used to create complicated aggregates and tightly coupled to to the domain
    
* **Repositories** are an abstraction of storage, retrieval and reconstitution of entities, coupled with infrastructure
    
* *Iterative and continuous* **Refactoring** provide deeper insights, refine inconsistencies or missing components while avoiding a rigid design and improving to an incisive, deep model
    
* Make **constraints** (invariables), **process** (methods or services) and (composable) **specifications** explicit
    
* A **Bounded Context** is a logical frame allowing model evolution, isolation by module, team, code and DB schemas. CI fosters independent, pure and unified growth but doesn’t handle Inter-model relationships which should be well defined
    
* A **Context Map** show relationships between bounded contexts capture the whole unified domain model
    
* To reduce duplication, a **Shared Kernel** is a overlapping subset of the domain model shared by teams
    
* Establish a **Customer/Supplier** relationship between dependent teams with the former defining integration tests for the latter to improve speed
    
* **Conformist** are customers that work within a one-sided supplier relationship building on a model that’s given provided there is a rich interface that fulfill their needs.
    
* An **Anticorruption layer** is a proxy between our clients and a 3rd party (legacy) systems. It’s usually implemented with **Facades** that our clients interface with which internally use their own adapters with translators to facilitate inter system communication and maintain separation and purity
    
* A **separate ways** strategy is employed to split an application that has disparate bounded contexts
    
* An **open host service** wraps a external service as a set of services made available to several of our clients that use it. The protocol is open and avoids a translator per client. Esoteric clients can have a translator to the protocol
    
* **Distillation** separates the essential parts of a large domain from generic sub domains used is several places. The core distillation is iterative and should be the main focus. Sub domains can use off the shelf solutions, be outsourced, use existing models or an in house solution
    

References:

* [http://www.infoq.com/minibooks/domain-driven-design-quickly](http://www.infoq.com/minibooks/domain-driven-design-quickly)
    
* [https://domaindrivendesign.org/](https://domaindrivendesign.org/)
    
* [Domain Design Design Book](https://amzn.to/3J3z1Th)
    
* [Main image via Claude](https://claude.ai/public/artifacts/8eb6d485-0e8d-4fd1-869b-de5ae075b07f)