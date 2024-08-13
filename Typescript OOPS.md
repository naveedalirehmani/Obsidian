
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