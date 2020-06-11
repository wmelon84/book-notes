# Object Design Style Guide

By Matthias Noback.
 
- [1 Programming with objects A primer](#1-programming-with-objects-a-primer)
- [2 Creating services](#2-creating-services)
- [3 Creating other objects](#3-creating-other-objects)
- [4 Manipulating objects](#4-manipulating-objects)
- [5 Using objects](#5-using-objects)
- [6 Retrieving information](#6-retrieving-information)
- [7 Performing tasks](#7-performing-tasks)

## 1 Programming with objects A primer
> TODO
## 2 Creating services
> TODO
## 3 Creating other objects
> TODO
## 4 Manipulating objects
### 4.1 Entities: Identifiable objects that track changes and record events
- An entity needs to be identifiable. When creating it, we give it an identifier.
- Given that the state of an entity changes over time, entities are mutable objects.

### 4.2 Value objects: Replaceable, anonymous, and immutable values
Value objects are completely different:
- Much smaller (just one or two properties)
- Represent part/aspect of an entity
- Wrap one or more primitive-type values

If we want to transform it to some other value, we should just instantiate a new copy, which represents the modified value.

## 7 Performing tasks
### 7.1 Use command methods with a name in the imperative form
- The name of such a method should indicate that the client can order the object to perform the task that the method name indicates.
- When looking for a good name, you should always use the imperative form.

### 7.2 Limit the scope of a command method, and use events to perform secondary tasks
- When performing a task, make sure you don’t do too much in one method.
- Use events as the link between commands that belong together, but we don't want the client to call explicitly, and we don't want to mix them in one method. (Is there any native implementation of event dispatcher in Java?)
- A possible disadvantage of using events is that the primary action and its secondary effects may be implemented in remote parts of the code base.

### 7.3 Make services immutable from the outside as well as on the inside
- Make sure none of your services update internal state influences its behavior like this.

### 7.4 When something goes wrong, throw an exception
- The same rule for retrieving information also counts for performing tasks: when some- thing goes wrong, don’t return a special value to indicate it; throw an exception instead.

### 7.5 Use queries to collect information and commands to take the next steps

### 7.6 Define abstractions for commands that cross system boundaries

### 7.7 Only verify calls to command methods with a mock
