---
layout: post
title: Domain Anemia
date: 2016-06-03 19:49:36.000000000 -05:00
type: post
published: true
status: publish
categories: []
tags: []
meta:
  _edit_last: '1'
  _thumbnail_id: '375'
author:
  login: phil.ledgerwood
  email: phil@integrityinspired.com
  display_name: Philip Ledgerwood
  first_name: Philip
  last_name: Ledgerwood
---
I want you to think for a minute about your application's domain model - specifically, the domain objects.  I have a question for you:

Are your domain objects almost entirely collections of public properties with getters and setters?

If so, your domain may be suffering from Domain Anemia.  Let's look at a case study.

### Patient #1 - The Customer Class

{% highlight csharp %}
public class Customer
{
  public int CustomerId;
  public string FirstName { get; set; }
  public string LastName { get; set; }
  public string Address1 { get; set; }
  public string Address2 { get; set; }
  public string City { get; set; }
  public string State { get; set; }
  public string Zip { get; set; }
  public virtual ICollection<Order> Orders { get; set; }
}
{% endhighlight %}

Not terrible, right?  Some of the more foresighted among us might want to make a value object out of the Address, but you get the idea.  This is typical of what I see in many domains - objects that are almost exclusively collections of public getters and setters with maybe one or two object-specific methods to do calculations or validations.  This object can easily be serialized, bound to a UI, and given to an O/RM for database saving.

And we are well on the way to a [Transaction Script](http://martinfowler.com/eaaCatalog/transactionScript.html) or [Active Record](http://martinfowler.com/eaaCatalog/activeRecord.html), which are both great options for applications that do not need the complexity of a domain at the heart of the software.  My guess is, however, that your application can benefit from a model of the domain, and this is how you're trying to do it.  If all you're trying to do is create a nice UI to update a database, this'll work just fine.  Use the Transaction Script or Active Record patterns with abandon.

But if you're trying to model a business domain, an object like this is not going to cut it.  Why?  Among other reasons, a class like our Customer class above captures absolutely no business intent or business value.

Think about this - right now all those public setters allow any of those pieces of data to be changed.  Great, right?  Well, is it?

What we're missing from this object is any kind of intent or reasoning about why its state could change.  Why, for instance, would we as a business ever change a Customer's city?

Is it so that they'll get their marketing materials?  Invoices?  Products?  Do those need to be different addresses?

What would happen to make us change that city?  Did the Customer move?  Other than just fat-fingering the wrong data, are there any other business reasons why that city would need to change?

Right now, our domain object reflects none of that intent or knowledge.  Any of that data could be changed from anywhere for any reason.

Ok, so let's say we took all the setters away from the address-related fields and created a `ChangeAddress()` method that took in new information and set those values internally.  Does that fix things?

It's made them better, but once again, have we established any kind of business intent?  We've defined that addresses have no reason to change one bit at a time and must change as a unit.  That's a step forward and would probably push us toward a refactored class design where Address was a value type instead of five separate fields.  But we still have given the power to `ChangeAddress()` to any possible context.

But what if we did this?

{% highlight csharp %}
public class Customer
{
  public int CustomerId { get; set; }
  public string FirstName { get; set; }
  public string LastName { get; set; }
  private Address _mailingAddress;
  public Address MailingAddress { get { return _mailingAddress; } }
  public virtual ICollection<Order> Orders { get; set; }
  public void MoveTo(Address newAddress)
  {
    _mailingAddress = newAddress;
    OnCustomerMoved(new CustomerMovedEventArgs(CustomerId, newAddress));
  }
}
{% endhighlight %}

Notice what we accomplished by this design:

1. The bits of address data are not available to change by anyone for any reason.
2. We have explicitly defined why, for our business model, an address should change.
3. We have defined something that could happen to a Customer that has an impact on our system from a business perspective and can now handle that with any logic we choose.
4. We can broadcast this event to the rest of the system allowing them to react to the fact that a Customer has moved however they need to.

There are more things we could do with this code to improve it.  Why should a CustomerId change?  What about name stuff?  Is this a sufficient way to handle address changes?  But I just wanted to introduce the concept of an anemic domain model, why it weakens our applications, and how we can start down the road to recovery.
