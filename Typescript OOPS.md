
### 1. Basic Class Definition

First, let's define a simple class:

```ts
class Animal {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    makeSound(): void {
        console.log(`${this.name} makes a sound`);
    }
}

```

### 2. Extending a Class

You can create a new class that extends the `Animal` class. This new class will inherit the properties and methods of `Animal`:

```ts
class Dog extends Animal {
    breed: string;

    constructor(name: string, breed: string) {
        super(name);  // Call the constructor of the base class (Animal)
        this.breed = breed;
    }

    makeSound(): void {
        super.makeSound();  // Call the method from the base class
        console.log(`${this.name} barks`);
    }

    displayBreed(): void {
        console.log(`${this.name} is a ${this.breed}`);
    }
}

```

### 3. Using the Extended Class

You can create instances of the `Dog` class and use its methods:

```ts
const myDog = new Dog('Rex', 'German Shepherd');

myDog.makeSound();      // Output: Rex makes a sound
                        //         Rex barks
myDog.displayBreed();   // Output: Rex is a German Shepherd

```

### 4. Access Modifiers

TypeScript provides three access modifiers: `public`, `private`, and `protected`.

- `public`: Default modifier. Accessible from anywhere.
- `private`: Accessible only within the class it is defined.
- `protected`: Accessible within the class and subclasses.

Example:

```ts
class Animal {
    protected name: string;

    constructor(name: string) {
        this.name = name;
    }

    makeSound(): void {
        console.log(`${this.name} makes a sound`);
    }
}

class Dog extends Animal {
    private breed: string;

    constructor(name: string, breed: string) {
        super(name);
        this.breed = breed;
    }

    displayBreed(): void {
        console.log(`${this.name} is a ${this.breed}`);
    }
}

```

In this example, `name` is protected, so it can be accessed in the `Dog` class but not outside it. `breed` is private, so it can only be accessed within the `Dog` class.

### 5. Abstract Classes

An abstract class is a class that cannot be instantiated and is typically used as a base class. It can contain abstract methods that must be implemented by derived classes:

```ts
abstract class Animal {
    protected name: string;

    constructor(name: string) {
        this.name = name;
    }

    abstract makeSound(): void;  // Abstract method

    move(): void {
        console.log(`${this.name} is moving`);
    }
}

class Dog extends Animal {
    makeSound(): void {
        console.log(`${this.name} barks`);
    }
}

const myDog = new Dog('Rex');
myDog.makeSound();  // Output: Rex barks
myDog.move();       // Output: Rex is moving

```
