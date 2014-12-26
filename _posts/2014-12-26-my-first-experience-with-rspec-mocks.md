---
layout: post
title: My First Experience with RSpec Mocks
---

"Writing a passing controller spec shouldn't take 2 hours!", I screamed inside my head at 7 in the morning on Christmas Eve.

I was trying to write a simple test for my people controller's create action:

{% highlight ruby %}
def create
  @person = Person.new(person_attributes)
  if @person.save
    redirect_to @person, notice: "Person created."
  else
    render :new
  end
end
{% endhighlight %}

In 2 hours all I had come up with was this incomplete "passing" test:

{% highlight ruby %}
context "when person is valid" do
  it "redirects to #show" do
    post :create, person: {first_name: "first_name"}
  end
end
{% endhighlight %}

The problem that I was having was that I couldn't figure out how get the `id` so that I could pass it to `person_path` and test that it was correctly redirecting to "#show".

I eventually got to this sloppy point where I'm forcing the person id a little too hard:

{% highlight ruby %}
context "when person is valid" do
  it "redirects to #show" do
    person = double(:person, id: 1)
    post :create, id: person.id, person: { first_name: "first_name" }
    expect(response).to redirect_to person_path(person.id)
  end
end
{% endhighlight %}

This still doesn't feel like the best solution, and I still feel like I have no idea what I'm doing.

If you actually read the documentation on RSpec mocks it might help a bit. Let's look at the the [Method Stubs](https://github.com/rspec/rspec-mocks#method-stubs) section:

> A method stub is an implementation that returns a pre-determined value.

This means that we can create a fake object, give it fake methods, and give those fake methods fake return values. This fake object with fake methods will need to match exactly how we do it in the controller, but by using mocks we can have faster tests because it doesn't actually touch the model validations.

The first thing we need to do is create a new instance of the Person Class just like we do in our controller. The first line in our controller create method looks like:

{% highlight ruby %}
@person = Person.new(person_attributes)
{% endhighlight %}

and so the first line in our spec will look like:

{% highlight ruby %}
person = Person.create(first_name: "first_name")
{% endhighlight %}

Now let's look at the second line in our controller create action:

{% highlight ruby %}
if @person.save
{% endhighlight %}

And we can mock this behavior with:

{% highlight ruby %}
allow(person).to receive(:save).and_return(true)
{% endhighlight %}

Notice there are 3 separate sections to the above line:

- `allow().to`
- `receive()`
- `and_return()`

Now that we have mocked this behavior I thought we could write our expect statement, but we can't just yet because we will get this failure when we run our test:

    Expected "http://test.host/people/1" to be === "http://test.host/people/2".

This brings my back to my origin problem in that the `id`'s don't line up. To fix this we need to mock the `Person` class and have it return the `person` object we created earlier:

{% highlight ruby %}
allow(Person).to receive(:new).with(first_name: "first_name").and_return(person)
{% endhighlight %}

Now that we have created this mock for the `Person` class, it won't actually use up the first `id` and leave it open for our controller to create a person with the `id` of '1'. Which solves our id missmatch problem.

Now when we can write our post request:

{% highlight ruby %}
post :create, person: { first_name: "first_name" }
{% endhighlight %}

and our expect statement we can pass in our person object to the `person_path()`:

{% highlight ruby %}
expect(response).to redirect_to person_path(person)
{% endhighlight %}

Here is what the complete test looks like:

{% highlight ruby %}
context "when person is valid" do
  it "redirects to #show" do
    person = Person.create(first_name: "first_name")
    allow(person).to receive(:save).and_return(true)
    allow(Person).to receive(:new).
    with(first_name: "first_name").
    and_return(person)

    post :create, person: { first_name: "first_name" }

    expect(response).to redirect_to person_path(person)
  end
end
{% endhighlight %}

This is not a requirement, but I think it makes the tests much more readable if you leave a blank like before the post request and a blank line before the expect statement.
