# `Op`s, `Container`s and `Graph`s
In `graphcalc`, calcualtions are carried out in a form of graph.

For example, consider this calculation:

```c++
x = a + b
```

The variables, `a` and `b` are treated as `Container` regardless of its type. They can be anything which adding is possible, such as `int`, `float`, `std::complex`, and Eigen `Matrix`.

The operator, `+` is treated as `Op`. `Op`s can have one or more `Container`s as input, and output one `Container` as output.

Also, there is a `Graph` which contains every `Op`s and `Container`s, forming a computation graph. A `Graph` is responsible of feeding the variable to the computation graph and getting the result.

## The `Op` class

The `Op` class is an abstract class serving as base class of all kinds of operations like `Add`, `MatMul`, and `Conv`.

### Method signatures

- `Op.calc -> Container` (abstract): calculates result from inputs

## The `Container<T>` class

The `Container<T>` class serves as a wrapper of 'basic' types of C++, and matrices of Eigen.

### Fields

- `name: std::string`: the name of the container.
- `value: T`: the value contained by `Container<T>`.

### Method signatures

- `Container<T>(name: std::string, value: T)`: a constructor of the class.

- `Container<T>.unpack -> T`: unpacks the type which is contained by `Container<T>`.

## The `Graph` class

The `Graph` class contains all `Op`s and `Container`s, feeds inputs as a `std::map` of `std:string` matched with `Container`, and gives output as a type of `Container`.

### Method signatures

- `Graph.run(input: std::map<std::string, Container>) -> Container`: runs the computation graph with given inputs.