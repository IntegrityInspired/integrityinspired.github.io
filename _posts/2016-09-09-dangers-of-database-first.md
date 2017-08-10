---
layout: post
comments: true
title: The Dangers of Designing the Database First
date: 2016-09-09 18:22:09.000000000 -05:00
type: post
published: true
status: publish
categories: []
tags: []
meta:
  _edit_last: '1'
  _thumbnail_id: '394'
  et_like_count: '5'
author:
  login: phil.ledgerwood
  email: phil@integrityinspired.com
  display_name: Philip Ledgerwood
  first_name: Philip
  last_name: Ledgerwood
---
Before application development was a common business practice, we had the database.

The role of the database in organizations was to store tabular data in a ledger or Rolodex style.  You would ask the database questions about the data that it stored, and it would tell you the answer, thus giving rise to names like "Oracle" and "Access."  Databases received exalted titles like "single source of truth."  You queried the data using the database's own query language, and if you had permissions, you could manipulate the data in the same way.  The genius of relational databases was that they allowed us to store a unique record of data only one time, which cut down significantly on data entry errors such as putting in the same customer name but spelling the last name slightly wrong.  This was called "data integrity."

It wasn't long before organizations discovered the utility of sharing their data and allowing more people to enter it, but for various reasons did not want to require people to learn SQL.  Microsoft's Access product allowed people, with very little effort, to create forms over the underlying database to reduce or eliminate the need for a query-er or a data entry-ist to use SQL for their operations; they could just go through the visual form.  A few enterprising types learned VBA which allowed them to automate some common tasks in Access, and it wasn't long before people made little proto-applications in this way.  Similar technologies cropped up for other database management systems as well.

Up until this point, keep in mind that the purpose of the database was to store tabular data and answer queries about it.  The notion of data integrity was purely about the data itself - you didn't want 2 digit phone numbers or the same address being spelled slightly different ways on different orders.  The GUIs placed over databases abstracted away the SQL, but they still existed to maintain and query tabular data.

But now, people began to want to write applications to do things.  Databases and forms were simple and the technology to build a logical grouping of these things already existed.  And that's just what people did.

Here's the core issue, however: tabular data is woefully inadequate to model the vast majority of business operations.

Imagine that I gave you an accounting ledger and said, "Everything about your job, I want you to do in this ledger."  Unless you were an accountant, you probably wouldn't be very happy with this.  Ledgers are designed to hold specific data structures for ease of reference, not "do" things.  Even accountants can't make the ledger calculate.  They use the data in the ledger for calculations, but all the ledger can be is a data storage mechanism in a particular format.  It would be ridiculous to suggest that I could take a pet grooming business, a grain trading company, a government agency that regulated environmental policies, and a heart surgeon's practice and use a ledger to accomplish all their business operations.

And yet, we seem to think that a database is an ideal place to model these things.

The complexities of subject matter and judgement get boiled down to rules that can join grids of data.  "Data integrity" is no longer about making sure there are no problems with the data itself, but has expanded to include a host of business-defined logical rules that have nothing to do with storage and retrieval.  Stored procedures, functions, and triggers get thrown into the mix to try to fill in the logical gaps that absolutely resist replication in a purely tabular format, and rather than stop and ask, "Maybe I'm using the wrong tool for the job," we keep adding things to the tool to try to make our job fit.

There is one and only one kind of application where it makes sense to start with database design, and that is this: Is storing and retrieving records of tabular data the primary purpose of this application?

If the answer is yes, by all means, design the database first and design screens around data access and retrieval.

But for the vast majority of applications, the point of the application is not to store and retrieve data, but to accomplish some business function.  I need an application to schedule appointments.  I need an application to process orders.  I need an application to help me manage my sales pipeline.  I need an application to remind me when to take my pills.  And so on.

In all of those circumstances, and many more, trying to model that in tabular data and build up from there is literally ridiculous.  Those are all business operations, not grids of data.  Your database manages grids of data.  That was all it was ever supposed to do and, to this day, it remains the only things databases are good at.  They are a tool that occupies a place in your software development effort, but they cannot model businesses or business processes, they cannot handle business logic, they cannot make decisions, they cannot make sure the data complies with "business rules."  Or rather, they can do all those things if do you enough violence to the business to cram it into the tool and bolt a few things onto the database that it's bad at.

Yet, many of us were taught to start with the database when building an application, which is the exact wrong way to start.  It virtually guarantees that your application is going to be difficult to work with, counter-intuitive to use, and in many cases flat out wrong.  **People do not want to use software to maintain data; they want to use software to get something done.**

We start, then, with what the person wants to get done.  We start with the person and move into the software.  What are the things you need to get done?

Then, since the application exists to help them get those things done, we design screens for them that make that process as easy as possible.  This probably does not look like a database query result with action links.  Once again, the goal for most applications (or at least most parts of an application) is not to maintain database tables - it's to perform a function or see the information necessary to do a job that can't be reduced to software rules.

As we build an application starting with the user and what they want to get done (and how they want to get it done), then of course we need this application to be able to work when you turn it back on.  It can't obliterate all the work you did and start with an empty slate.  It has to persist the state of things that it works with.  This is a requirement of many applications, and a database can be a good way to do that.

It's also not the only way to do that.  State can be persisted in memory, in cookies, in XML files, in non-relational databases, on disk - there are all kinds of ways to persist state outside the life of an individual application-using session, but now we are talking about an implementation detail.  Now we are in a prime position to decide on the best mechanism(s) we want to use to persist the state of the application and the most efficient structures for doing so.  Maybe those structures will look a lot like our screens.  Maybe they won't.  It doesn't matter, because at that point, we are designing purely for efficient data storage and retrieval, which is precisely the purpose of a database and the job function it optimally performs.

If persistent storage is your last consideration rather than your first, you will discover that your UI is more intuitive for your users and your logic lives where it is most flexible and useful - in the brain of your user and the algorithms of your application.  You will find that your databases are faster and leaner, unencumbered with complex relationships to multiple tables that exist purely to make an organic business model fit into a series of connected grids (which, incidentally, also describes a lot of UI out there), focused on the task of persisting and retrieving state-driven data instead of processing the infinite variety of business rules that exist.

Your application, too, will be easier to expand, change, and maintain as the logic will be expressed in algorithmic language close to the actual business decision rather than a language used to query grids of records.  Many changes to business logic will require no database changes at all, because the database is simply focused on storing and retrieving the raw stuff the application needs from session to session.

Do you have considerations for your data beyond mere storage?  Do you need reporting?  Do you need to share your data?

First, I would argue that most "data sharing" needs come from a database-first design.  Instead of storage being driven by the application, the storage becomes the central model of the business, and therefore all applications need to share it because they work with the same business domain.  Anyone who has known the joy of adding extra fields to a table because "we have a batch process that X, Y, Z" or can't refactor a table into a better design because "Application Alpha uses that field" knows what I mean.  If our data storage were first defined by a person's need as facilitated by software, we'd probably have a lot fewer scenarios where data needed to be shared.

But they would happen, and not only that, but sometimes we need data compiled into other formats for things like reporting and archiving, and data migration mechanisms are great for this kind of thing and give you all sorts of flexibility.  Write your reports off an optimized reporting database.  Have your application do all its reads from a read-optimized database and all its writes to a write-optimized database.  Databases are good at sharing and restructuring their data into other data storage.  They are very bad at trying to serve multiple business interests with the same entities.

With app production rising exponentially in today's world, these database-first practices need to go.  Not only do they slow you down, trying to use them will most likely do a great deal of violence to a business model to make them fit, will be much slower than databases used purely for storage, and they make change expensive and prohibitive.

And your screens will be ugly.  Did I mention that?
