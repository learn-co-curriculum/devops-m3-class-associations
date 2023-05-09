# Class Associations

## Learning Goals

- Learn how to relate different classes to each other.
- Differentiate association, aggregation, and composition.

## Introduction

Now that we know all about SQL and how to create relationships, let's look at
how we can do the same with Python!

In the last module, we learned about how we can create classes that inherit
attributes and methods from a parent, enabling children classes to receive those
features.

However, some relationships between classes and objects are not as
straightforward as parent-child relationships. For instance, the job titles
"Curriculum Developer" and "Instructor" fall under the broader category of
"Jobs", but they also have associated concepts such as "Duties" and "Schedules".
In such cases, we can't rely solely on inheritance to solve these issues.
Nevertheless, we can still use the same Python techniques that you're already
familiar with to create a wide variety of relationships.

We will delve into the various types of relationships and explore how to
leverage Python to establish them.

## Association

**Association** refers to a relationship where two objects are related, but not
in a way that one object owns the other. For example, a library has an
association with the books it stores, but it doesn't own the books.

Let's look at an example! Assume we want to do some food shopping. There would
be a `Shopper` class and a `GroceryItem` class as shown below.

```py
class GroceryItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class Shopper:
    def __init__(self, name):
        self.name = name

```

Currently, these two classes have no relationship to each other. In order to
form an association, the `Shopper` class will need to have a list attribute to
store the related `GroceryItem` objects. In this case it does not make sense
for the `GroceryItem` to know about the `Shopper`.

Let's look at the code now that we have added a list attribute to associate the
`GroceryItem` to the `Shopper` class:

```py
class GroceryItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class Shopper:
    def __init__(self, name):
        self.name = name
        self.grocery_items = []


```

In this example, the `Shopper` class has a `grocery_items` attribute, which is a
list of `GroceryItem` objects. Here's how you can use these classes:

```py
# Create a shopper and some grocery items
shopper = Shopper("Alice")
item1 = GroceryItem("apple", 1)
item2 = GroceryItem("orange", 2)

# Add the grocery items to the shopper's list
shopper.grocery_items.append(item1)
shopper.grocery_items.append(item2)

# Print the shopper's grocery list
for item in shopper.grocery_items:
    print(item.name, item.price)

# => apple 1
# => orange 2
```

Now that we have established how to associate multiple classes with each other
to form a relationship, let's talk about two subsets of association: composition
and aggregation!

## Composition

**Composition** is a "has-a" relationship. For example, a computer has a CPU.
In this example, there is a dependency. A CPU does not exist without a
computer. The dependency that the child has on the parent is what makes this
an example of composition.

```py
class CPU:
  def __init__(self, cpu_type):
    self.cpu_type = cpu_type

class Computer:
  def __init__(self, cpu_type):
    self.CPU = CPU(cpu_type)

```

## Aggregation

**Aggregation** is a relationship where one object is part of another object
and the first object can exist independently. For example, a player is part of
a team, but the player can still exist without a team or join another team.

```py
class Player:
    def __init__(self, name, position):
        self.name = name
        self.position = position

class Team:
    def __init__(self, name):
        self.name = name
        self.players = []
        
```

## Conclusion

In this lesson, we learned how we can relate classes to each other using
associations. There are two special cases of associations called composition
and aggregation. The difference between the three are as follows:

- An association is when one object, A, has a relationship with another object,
  B.
  - Think of a shopper buying a grocery item.
- Composition is a form of association where object A has ownership over
  object B. Therefore, if object A ceases to exist, then object B also ceases
  to exist.
  - Think of a computer having a CPU. If the computer were to crash, then the
    CPU would also cease to exist.
- Aggregation is a form of association where object A is part of object B, but
  object A can standalone and still exist.
  - Think of a sports' player and a team. If the team were to disband, the
    player would still exist and could join a new team.

## Resources

- [Difference between Association, Composition, and Aggregation](https://javarevisited.blogspot.com/2014/02/ifference-between-association-vs-composition-vs-aggregation.html#axzz81F0KQheO)
- [UML Association vs Aggregation vs Composition](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-aggregation-vs-composition/)
