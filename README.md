# Iterator Pattern in C#

## Introduction
The Iterator Pattern is a design pattern that allows sequential access to the elements of an aggregate object without exposing its underlying representation. In C#, this pattern is particularly useful in handling collections of objects.

## Concept
The Iterator Pattern involves two key components:
1. **Iterator**: An interface that defines the operations for accessing and traversing elements.
2. **Aggregate**: The collection object that implements the Iterator interface.

The main advantage of using the Iterator Pattern is that it decouples the collection objects from the traversal logic.

## Implementation in C#

### Iterator Interface
First, we define the `Iterator` interface:

```csharp
public interface IIterator<T>
{
    bool HasNext();
    T Next();
}
```

### Concrete Iterator
Next, we implement a concrete iterator for a specific collection type:

```csharp
public class ConcreteIterator<T> : IIterator<T>
{
    private readonly List<T> _collection;
    private int _current = 0;

    public ConcreteIterator(List<T> collection)
    {
        _collection = collection;
    }

    public bool HasNext()
    {
        return _current < _collection.Count;
    }

    public T Next()
    {
        return _collection[_current++];
    }
}
```

### Aggregate Interface
The aggregate interface provides a method to create an iterator:

```csharp
public interface IAggregate<T>
{
    IIterator<T> CreateIterator();
}
```

### Concrete Aggregate
Finally, we create a concrete aggregate that implements the `IAggregate` interface:

```csharp
public class ConcreteAggregate<T> : IAggregate<T>
{
    private readonly List<T> _items = new List<T>();

    public IIterator<T> CreateIterator()
    {
        return new ConcreteIterator<T>(_items);
    }

    public void Add(T item)
    {
        _items.Add(item);
    }
}
```

## Example Usage
Here's how you can use these classes:

```csharp
var aggregate = new ConcreteAggregate<string>();
aggregate.Add("Item 1");
aggregate.Add("Item 2");
aggregate.Add("Item 3");

var iterator = aggregate.CreateIterator();
while (iterator.HasNext())
{
    Console.WriteLine(iterator.Next());
}
```
