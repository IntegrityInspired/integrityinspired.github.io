---
layout: post
title: The New DDD - Dumbing Down Developers
date:
type: post
published: false
status: draft
categories: []
tags: []
meta:
  _edit_last: '2'
author:
  login: phil.ledgerwood
  email: phil@integrityinspired.com
  display_name: Philip Ledgerwood
  first_name: Philip
  last_name: Ledgerwood
---
[caption id="" align="alignright" width="350" class="zemanta-img"][![Portrait of Henry Ford (ca. 1919)]({{ site.baseurl }}/assets/350px-Henry_ford_1919.jpg "Portrait of Henry Ford (ca. 1919)")](http://commons.wikipedia.org/wiki/File:Henry_ford_1919.jpg) Portrait of Henry Ford (ca. 1919) (Photo credit: Wikipedia)[/caption]

The importance of the early 1900s to how you do work, today, cannot be overstated - at least for America.  The things that happened in that time period have dictated the shape of entire corporations, business processes, and defined project management.

There were two tsunamis that washed over the American work force in that time, and instead of receding, they created a new ocean that we still swim in, today.  Insofar as other parts of the world have been influenced by American industrialism, the effects have been global.  Those two things are:

1. The rise of [Scientific Management](https://en.wikipedia.org/wiki/Scientific_management) (Taylorism) as defined by Frederick Taylor
2. The rise of Henry Ford and his production methods

Entire books can and have been written on the profound influence these forces have had on how organizations do their work.  "Influence" is probably not a strong enough word.  Those forces have influenced work the same way dams influence the flow of water.

I want to focus on just one facet for this article.

Prior to Taylor, it was common for workers to be what we might think of as tradesmen.  The same people who built motors also fixed motors and designed better motors.  Creativity, judgement, and diagnostic abilities that come from experience were part and parcel of the people who produced a Thing.

Taylor realized that you could actually save a lot of money if you had a small number of employees who had the "knowledge" side of the work while the bulk of your employees were simply manual producers who executed on what the knowledge side provided.  You could pay the manual producers far less money, because at that point, they are simply replicating movements and operating machines to create what someone else had mapped out for them.

When Henry Ford applied this principle, it was originally an HR nightmare.  Workers quit in droves.  Ford stated that he had to hire almost a thousand people for every hundred he wanted to maintain.  Getting paid less probably had something to do with it, but historical sources indicate that most workers resisted this new system because it reduced their dignity.  They were no longer experts who knew their product inside and out and could be counted on to make judgement calls, adjustments, suggestions, etc.  Now, they were just a body capable of performing the motions necessary to produce something.

This division between the few who handle the intellectual work and the many who handle the manual execution of what the intellectuals have produced informs a lot of work practices, and software development has not been immune.

Software development has inherited a lot from manufacturing practices, for better or worse.  Perhaps the most infamous example is NASA's efforts in the 60's to write software for the Apollo spacecraft.  NASA, used to developing hardware, ran their software development the same way.  They hired massive amounts of coders and a much smaller number of "engineers" to design the software.  The engineers designed, and the coders coded.  According to NASA's own historical documents, the code ended up being of so poor quality that a much larger amount of time needed to be spent on verification and led them to conclude "more programmers do not mean faster development."  Their solution to this problem was more rigorous documentation and more levels of verification - in other words, removing even more responsibility from the programmers and placing it in the hands of the engineers.

I wish I could say this legacy has taught us something, but as a consultant who gets around to a variety of organizations, I see this trend not only still in existence but becoming more entrenched.  Organizations have "architects" who design the software and "coders" who code whatever the architect designed, typically according to a standards document that they did not produce.  Someone who may or may not be good at software development does all the thinking, and the developers do all the executing.

This is anecdotal, of course, but I see this trend growing.  Creativity, judgement calls, and a fully-orbed knowledge of the software and the business needs that drive it are reserved for a select few, while this sort of knowledge is actively kept from the coders.  Sometimes entire jobs exist to keep coders from actually having to think outside their box.

While this may make a sort of bottom-line, short-term economic sense for organizations, it's very risky for long-term health.

On the developer side of things, this makes you essentially an interchangeable part.  If you know C#, all you have to do is write the C# that someone has told you to write.  You can do that at any company, and you can easily be replaced with anyone else who can do the same thing.  You will become incapable (or never develop the capability) of hearing someone's business need and translating that into useful, well-written software.  You just have to type stuff a C# compiler can understand.

This is a trend I am observing in developers both young and old.  Our developers, collectively, are getting dumber.  They are not getting less intelligent, but they are losing the capabilities that tradesmen have.  They are getting worse at solving problems when their code doesn't work.  They are getting worse at being able to decide between multiple paths to the same solution, or whether a proposed solution is appropriate or best.  Those are the things left to "architects."  They may know more languages, but they have lost the ability to author software.  They aren't authors; they are copyists.  I foresee a day in the not too distant future when "programmer" will be a functional synonym for "can copy and paste from [Stack Overflow](http://stackoverflow.com/)."

But will there be anybody left who can post solutions to Stack Overflow?  Who will do this?  The solution designers who can't code or the coders who can't design solutions?

The point is, if all you can do is code what someone else tells you to code, there is no reason you can't be replaced with somebody cheaper.  The only value you are providing is the sheer, repetitive movements of typing lines of code, and somebody fresh out of school or in another country can also provide that.  This situation is not your fault, but it is a direct consequence of the division of labor.

On the organizational side of things, you do get some benefits from this state of affairs.  People who just type code are cheaper than people who design good software.  Their interchangeability allows you to pick the risk vs. price slot you're comfortable with and get those lines of code from whatever source is cheapest.  If Cathy Coder leaves the company, you can replace her with Carol Coder, and it's not like you've lost tons of business knowledge in that transaction, because all Cathy was responsible for was producing (or re-producing, in most cases) something that preceded her.  Anybody else can come in, look over what's been done before them, and after getting warm to it, can code just the same.

But you are playing a very dangerous game, here.

The reason we diversify our investments is to minimize the risk.  When you centralize your designing/authoring/judgement calling skill into a few people, the loss of even one of those people has a tremendous effect on your production, as does the incompetence of one of those people.  I could tell you story after story of organizations who were sure that their architect was amazing, only to get in there and discover that what they had designed was a time bomb (not literally, of course, but there's a first time for everything).  They had designed a system that would not scale using risky practices to create inefficient software that only the worst coders would possibly be willing to work on.

But who knew?  The other coders?  Who had the knowledge necessary to collaborate with or critique the architect?  Nobody, and it puts the organization at their mercy.

Even if you manage to land yourself a good architect (and in my software development journey of almost two decades, and all the architects I've ever met, I can think of one, maybe two who were good at it), what happens if they leave?  You can't just rotate another developer into their position; the odds are good that any given developer is woefully inadequate to make strategic, author-level decisions about your system.  It would be like asking the guy who operates the machine that presses car hoods to design a better car.

And then there is the overhead of interchangeability.  Just like you could replace most of your developers with any other developers, they can also do what they do anywhere else, and they are free to go where the money is.  You write code for this guy, write code for that guy - it's all the same.  Are you willing to absorb the cost of regularly cycling in and cycling out employees?  Remember Ford who had to hire almost a thousand people for every hundred he wanted to keep?

And if you want to lower that turnover, your options are pretty limited.  Typically, this results in offering more and more money to less and less skilled people, which I think nails the Kansas City market pretty well, and organizations are turning to outsourcing to relieve this pressure.

The problem is not the developers.  The problem is the system.  We have created this.  We have taken intelligent, talented, and skilled individuals and taken away from them everything that requires intelligence, talent, and skill.  We have done this in the name of "saving money" or "maximizing efficiency" only to realize that now it takes forever to hire a developer who can actually author software.  We have bred that ability right out of them, telling them exactly what to do and how to do it and how fast it needs to be done and withholding from them the power and the opportunity to be collaborators in all of that.  The people who find value in operating at that level will go somewhere else (or just complain a lot), leaving you with everyone else who can't develop their feature because they need someone to give them an example they can copy, paste, and tweak.

It makes good sense for everyone to make your architects code and your coders architect.  It makes everyone stronger.
