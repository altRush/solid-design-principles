# SOLID Design Principles in TypeScript

### Single Responsibility Principle

A class should have only one responsibility or job. This helps to keep classes focused and easy to understand.

```typescript
function srpDemo() {
  class Cookie {
    private flavor: string;

    constructor(flavor: string) {
      this.flavor = flavor;
    }

    getFlavor(): string {
      return this.flavor;
    }
  }

  class MilkDipper {
    dipCookie(cookie: Cookie): void {
      const flavor = cookie.getFlavor();
      console.log(
        `Dipping the ${flavor} cookie into the milk and savoring that sweet taste!`
      );
    }
  }

  const cookie = new Cookie('Chocolate Chip');
  new MilkDipper().dipCookie(cookie);
}

srpDemo();
```

### Open/Closed Principle

Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This means that you should be able to add new functionality to a class without having to modify the existing code.

```typescript
function ocpDemo() {
  interface Toy {
    play(): void;
  }

  class DancingRobot implements Toy {
    play(): void {
      console.log('Robot: The clanking robot slam-dances wildly!');
      this.adjustHydraulics();
    }

    adjustHydraulics() {
      console.log('Robot: Adjusting hydraulics...');
    }
  }

  class SingingDinosaur implements Toy {
    play(): void {
      this.snack();
      console.log('Dinosaur: The giant dinosaur roars into a song!');
    }

    snack() {
      console.log(
        'Dinosaur: Eating some lesser creatures as a pre-performance snack...'
      );
    }
  }

  class ToyPlayer {
    playWithToys(toys: Toy[]): void {
      for (const toy of toys) toy.play();
    }
  }

  new ToyPlayer().playWithToys([new DancingRobot(), new SingingDinosaur()]);
}

ocpDemo();
```

### Liskov Substitution Principle

Subtypes should be able to replace their supertypes without changing the program. This principle ensures that inheritance objects are well-designed and don't introduce unexpected behavior.

```typescript
function lspDemo() {
  class Animal {
    protected name: string;

    constructor(name: string) {
      this.name = name;
    }

    getName(): string {
      return this.name;
    }

    makeSound(): string {
      return 'Animal sound!';
    }
  }

  class Cat extends Animal {
    makeSound(): string {
      return 'Meow!';
    }
  }

  function greetAnimal(animal: Animal): void {
    console.log(`Hello, ${animal.getName()}!`);
    console.log(animal.makeSound());
  }

  const animal = new Animal('Any Animal');
  greetAnimal(animal);

  const cat = new Cat('Whiskers');
  greetAnimal(cat);
}

lspDemo();
```

### Interface Segregation Principle

Clients should not be forced to depend on interfaces they do not use. This principle encourages you to split larger interfaces into smaller, more specific interfaces.

```typescript
function ispDemo() {
  interface Dancer {
    dance(): void;
  }

  interface Juggler {
    juggle(): void;
  }

  interface Singer {
    sing(): void;
  }

  class SimpleDancer implements Dancer {
    dance(): void {
      console.log('Just a plain simple dancer dancing...');
    }
  }

  class MultitalentedPerformer implements Dancer, Juggler, Singer {
    dance(): void {
      console.log("Can't compete with my dancing skillz!");
    }

    juggle(): void {
      console.log("Can't compete with my juggling skillz!");
    }

    sing(): void {
      console.log("Can't compete with my singing skillz!");
    }
  }

  const dancer = new SimpleDancer();
  dancer.dance();

  const performer = new MultitalentedPerformer();
  performer.juggle();
}

ispDemo();
```

### Dependency Inversion Principle

High-level modules should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions. This principle helps to decouple modules and make them more reusable.

```typescript
function dipDemo() {
  interface FoodProvider {
    provideFood(): void;
  }

  class PizzaRestaurant implements FoodProvider {
    provideFood(): void {
      console.log("Man, that's some tasty pizza!");
    }
  }

  class IceCreamTruck implements FoodProvider {
    provideFood(): void {
      console.log('Some sick ice cream!');
    }
  }

  class Foodie {
    private foodProvider: FoodProvider;

    constructor(foodProvider: FoodProvider) {
      this.foodProvider = foodProvider;
    }

    consumeFood(): void {
      this.foodProvider.provideFood();
    }
  }

  const pizzaLover = new Foodie(new PizzaRestaurant());
  pizzaLover.consumeFood();

  const icecreamLover = new Foodie(new IceCreamTruck());
  icecreamLover.consumeFood();
}

dipDemo();
```

---

#### References:

- https://dev.to/iamrule/solid-principles-explained-28da
- https://github.com/mikaelvesavuori/5-minutes-or-less-solid/
