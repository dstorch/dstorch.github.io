+++
draft = false
title = 'Experience'
+++

## Professional Experience

#### MongoDB

MongoDB is the leading document database management system. I've worked on query processing
at MongoDB for over a decade, and I'm in the top 12 contributors to the MongoDB server by commit count.
The [projects](#projects) section below gives a flavor of the topics I've worked on during my tenure.
At MongoDB, I've grown from an entry level software engineering role into my current role as a Senior Staff Engineer:

Title | Timeframe
------|----------
Senior Staff Engineer, Query Processing | Feb 2022 - present
Staff Software Engineer, Query Processing | Nov 2020 - Feb 2022
Lead Software Engineer, Query Processing | Dec 2015 - Nov 2020
Software Engineer, Query Processing | Aug 2013 - Dec 2015

## Projects

##### Cost-based optimization

Historically, MongoDB's query optimizer has used an unconventional empirical approach to cost alternative
plans. The system generates a set of alternative plans, with a set of heuristics to constrain the search
space to a reasonably small number of plans. These plans then undergo the so-called "multi-planning"
process -- each plan is partially executed in a round robin fashion in order to collect runtime statistics,
which are fed into a ranking formula. This design has served MongoDB well for years for several reasons:
* It is simple, easy to understand, and easy to debug/diagnose in customer support contexts.
* It has "early out" behavior which ensures that the optimization process terminates promptly for key-value
style queries which are common in document databases.
* Statistics are derived empirically and thus cannot become stale and do not need to be managed.

At the same time, the multi-planning approach has several drawbacks:
* It can be led astray by correlations in the data as described <a href="https://jira.mongodb.org/browse/SERVER-20616">here</a>.
* In edge cases, partial plan execution can run for too long and become expensive.
* It reduces the number of plan alternatives that the optimizer can explore.

In early 2024, myself and others developed and proposed a roadmap to address
these shortcomings by introducing cost-based optimization to MongoDB alongside
the multi-planner. This initiative is under active development and involves
several lines of work: introducing and calibrating a new cost model,
implementing various cardinality estimation approaches, and adding more
sophisticated query optimizer performance and correctness testing.

##### Slot-based execution engine

The slot-based execution engine (SBE) is MongoDB's next-generation query execution
engine. It is being improved and released iteratively by slowly expanding the set of
MongoDB Query Language (MQL) features which it can support. I was involved in the early
phases of developing SBE and putting it into production. One of SBE's primary design goals is to
offer a set of core primitives for document processing which by composition can express
the rich query processing behaviors available to end-users of the database system. A second
key design principle is to gain performance through late materialization -- it permits the
construction of execution plans which "shred" documents into the relevant values up front,
compute over those values, and re-materialize the resulting documents as late as possible.
For expression execution SBE compiles expressions to a customized bytecode and
implements a VM to execute the bytecode.

##### Explain

I designed and implemented MongoDB's support for <a
href="https://www.mongodb.com/docs/manual/reference/command/explain/">explain</a>.
This is a critical debugging and diagnostic tool used extensively to understand
the behavior of the query engine. This could be either for tuning query
performance during application development, diagnosing customer performance
problems, or internally by MongoDB's developers for testing or for analyzing
bugs.

##### Plan cache

Query systems generally cache query plans chosen by the optimizer in order to
avoid re-optimizing repetitive queries issued by the client. This typically
involves auto-parameterization -- replacing certain query constants with
parameter markers -- such that queries which share the same "shape" can benefit
from a single cache entry. I implemented MongoDB's first plan cache, which
remains in production today in largely its original form.

##### And more

In addition to the projects above, I've contributed to the following:
* Adding support for unicode <a href="https://www.mongodb.com/docs/manual/reference/collation/">collation</a> to the MongoDB Query Language.
This allows applications to take advantage of locale-specific string comparison rules for natural language.
* <a href="https://json-schema.org/">JSON Schema</a> support in MongoDB.
* Migration from MongoDB's legacy wire protocol to <a href="https://www.mongodb.com/docs/manual/reference/mongodb-wire-protocol/#std-label-wire-op-msg">OP_MSG</a>, the RPC protocol it uses today.
* Design of the format used to log updates for replication.
* Storage of schema metadata indicating which fields are arrays, and consumption of this metadata in the query optimizer
in order to make key optimization decisions.
* Introduction of a <a href="https://www.mongodb.com/docs/manual/reference/command/setFeatureCompatibilityVersion/">feature compatibility version</a>
designed to facilitate a smooth upgrade/downgrade process.

## Education

Brown University | Sc.B. Computer Science | 2009 - 2013

## Patents

I hold the following patents related to my work at MongoDB:

* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US20240427767A1/en" target="_blank"> Terlecki, Neupauer, Mihaylov, Korshunov, Boros, Katchaounov, and Storch.
<em>Query processing system</em>. U.S. Patent Application 2024/0427767 A1. Filed 2024.</a>
* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US11698981B2/en" target="_blank"> White, Benvenuto, Albertson, Storch, and Horowitz. <em>
Systems and methods for client-side and field-level encryption with dynamic schema databases</em>. U.S. Patent 11,698,981 B2. Filed 2020.</a>
* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US10872095B2/en" target="_blank"> Horowitz, Storch, and Swanson. <em>
Aggregation framework system architecture and method</em>. U.S. Patent 10,872,095 B2. Filed 2018.</a>
* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US10997211B2/en" target="_blank">Merriman, Horowitz, Mintz, Nelson, Kumar, Storch, et al.<em>
Systems and methods for database zone sharding and API integration</em>. U.S. Patent 10,997,211 B2. Filed 2018.</a>
* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US11537667B2/en" target="_blank"> Horowitz, Storch, and Stearn. <em>
System and interfaces for performing document validation in a non-relational database</em>. U.S. Patent 11,537,667 B2. Filed 2017.</a>
* <a class="link-secondary text-decoration-none" href="https://patents.google.com/patent/US10585867B2/en" target="_blank"> Horowitz, Storch, Hirschhorn, and Rassi.<em>
Systems and methods for generating partial indexes in distributed databases</em>. US. Patent 10,585,867 B2. Filed 2017.</a>