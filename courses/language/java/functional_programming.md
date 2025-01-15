# Functiona Interface

an interface with exactly one abstract method. Functional interface use @FunctionalInterface annotation.

Java provides many pre-defined fucntional interface such as Supplier, Consumer, Predicate, Function

```java
@FunctionalInterface
public interface Animal {
    public void speak(String s);
}

public class Myclass {
    public static void main(String... args) {
        //old way
        Animal oldAnimal = new Animal() {
            @Override
            public void speak(String s) {
                System.out.println(s)
            }
        }
        oldAnimal.speak();

        //new way - lamda expression
        Animal newAnimal = s -> System.out.println("new")
        newAnimal.speak()

        //method reference
        Animal refAnimal = s -> System.out::println; //compiler already know number and types of the param, also return type
        refAnimal.speak();
    }
}
```

## Common Functional Interfaces

Functional interface is in java.util.Function.* package

```java
Supplier<T> : get() : T // return T
Supplier<LocalDateTime> dtImpl = () -> LocalDateTime.now()
System.out.println(dtImpl.get()) // prints date and time

Consumer<T> : accept(T) : void // accept T
BiConsumer<T, U> : accept(T, U) : void // accept T, U
BiConsumer<String, Integer> greet = (name, year) -> System.out.println("Hello, " + name + "! Happy New Year " + year);
greet.accept("Spartan", 2025);
//Helper method: andThen()
BiConsumer<String, Integer> bye = (name, year) -> System.out.println("Bye, " + name + "! Year " + year);
BiConsumer<string, Integer> combGreet = greet.andThen(bye);
combGreet.accept("Spartan", 2024);
greet.andThen(bye).accept("Spartan", 2023); //another way

//Predicate has one abstract method: boolean test(T t)
Predicate<T> : test(T) : accept T and return boolean
BiPredicate<T, U> : test(T, U) : accept T, U and return boolean
Predicate<Integer> gt10 = n -> n > 10;
System.out.println(gt10.test(12)) //returns true
//Helper method: and(), or(), negate()

Function<T, R> : apply(T, R) : R //accept T and return R
BiFunction<T, R> : apply(T, U, R) : R //accept T, U and return R
Function<Integer, Double> square = n -> (double)(n*n)
System.out.println(square.apply(5)) //prints 25.0
//Helper method: andThen(), compose()
Function<Integer, Integer> square = n -> n*n;
Function<Integer, Integer> triple = n -> 3*n;
square.andThen(triple).apply(5) //5*5, 3*25 = 75 : square first, and then triple
square.compose(triple).apply(5) //(3*5) * (3*5) = 225 : triple first, then square

UnaryOperator<T> : apply(T) : T //accept T and return T
BinaryOperator<T, T> : apply(T, T) //accept T, T and return T
BinaryOperator<Double> add = (a,b) -> a+b;
System.out.println(add.apply(2.5,5.5)) //prints 8.0
```

## Functional Interfaces for primitive

Primitive functional interfaces are faster, so use it wherever possible

```java
BooleanSupplier : getAsBoolean() : boolean
//similar - DoubleSupplier, IntSupplier, LongSupplier
DoubleConsumer : accept(double a) : void
//similar - DoublePedicate, DoubleFunction, DoubleUnaryOperator
DoubleFunction<R> : apply(double value) : R //accept double, return R
ToDoubleFunction<T> : applyAsDouble(T t) : double //accpet T, return double
DoubleToIntFunction : applyAsInt(double value) : int //accept double, return int
DoubleUnaryOperator : applyAsDouble(double value) : double
ObjDoubleConsumer<T> : accept(T t, double value) : void // basically BiConsumer that always accept double as one param
```
