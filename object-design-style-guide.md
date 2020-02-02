# Object Design Style Guide

By Matthias Noback.

4. [Manipulating objects](#manipulating-objects)

## 4. Manipulating objects
### 4.1 Entities: Identifiable objects that track changes and record events
- An entity needs to be identifiable. When creating it, we give it an identifier.
- Given that the state of an entity changes over time, entities are mutable objects.

### 4.2 Value objects: Replaceable, anonymous, and immutable values
