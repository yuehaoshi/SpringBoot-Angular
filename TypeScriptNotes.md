
# TypeScript
TypeScript, a superset of JavaScript and ECMAScript
Web Browser donot understand TS, need to use tsc to convert .ts to .js (tsc mydemo.ts), and then run js code through node (node mydemo.js)
## Fundamentals
### Define Variables
```typescript
let <variableName>: <type> = <initial value>;
let found: boolean = true;
let grade: number = 88.6;
let firstName: string = 'A';
let lastName: string = "B";
//Assign to different values
found = false;
//But Typescript is strongly typed, so "dound = 0" will raise type mismatch error
//"any" type can be assigned by any type of value, but becareful for losing type-safety
let myData: any = 50.0;
myData = false
```
### Print
```typescript
console.log(found);
console.log("The grade is" + grade);
console.log("Hi "+ firstName + " " + lastName);
//use template strings
console.log(`Hi ${firstName} ${lastName}`)

export {};
//https://bobbyhadz.com/blog/typescript-cannot-redeclare-block-scoped-variable#:~:text=The%20error%20%22Cannot%20redeclare%20block,block%20and%20use%20ES%20modules.
```
### Run ts file
```typescript
tsc filename.ts
node filename.js
```
### Loops
```typescript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
let reviews: number[] = [5, 5, 4.5, 1, 3];
for (let i = 0; i < reviews.length; i++) {
    console.log(reviews[i]);
}
reviews.push(0.5);
for (let review of reviews) {
    if (review == 5) console.log(`${review}, full score!`);
    else console.log(review);
}
export{};
```
## Classes
### Building Classes
Properties are public by default;
Access Modifiers:
| Modifier  | Definition                            |
|-----------|---------------------------------------|
| public    | Accessible to all classes (default)   |
| protected | Accessible to current and sub-classes |
| private   | Accessible to current class only      |

```typescript
class Customer01 {
    firstName: string;
    lastName: string;
    //default are public
}
//create an instance
let myCustomer01 = new Customer01();
myCustomer01.firstName = "A";
myCustomer01.lastName = "B";
console.log(`${myCustomer01.firstName} ${myCustomer01.lastName}`)

// Using a constructor
class Customer02 {
    firstName: string;
    lastName: string;
    //default are public
    constructor(theFirst: string, theLast: string) {
        this.firstName = theFirst;
        this.lastName = theLast;
    }
}
let myCustomer02 = new Customer02("C", "D");
console.log(`${myCustomer02.firstName} ${myCustomer02.lastName}`)
```
### Accessors (Get/Set)
```typescript
class Customer {
    // private _firstName: string;
    // private _lastName: string;
    // constructor(theFirst: string, theLast: string) {
    //     this._firstName = theFirst;
    //     this._lastName = theLast;
    // } //These lines are equivilant to:
    constructor(private _firstName: string,
                private _lastName: string) {}
    //Defines properties and assigns properties automaticly, minimize boilerplate coding
    public get firstName(): string {
        return this._firstName;
    }
    public set firstName(value: string) {
        this._firstName = value;
    }
    public get lastName(): string {
        return this._lastName;
    }
    public set lastName(value: string) {
        this._lastName = value;
    }
}
let myCustomer = new Customer("C", "D");
console.log(`${myCustomer.firstName} ${myCustomer.lastName}`)
```
### Import and Export Class
File: Customer.ts
```typescript
export class Customer {...}
```
File: Driver.ts
```typescript
import { customer } from './Customer';
//Leave off .ts, can use relative directory path
let myCustomer = new Customer('A', 'B');
```
## Inheritance
File: shape.ts
```typescript
export class Shape {
    constructor(private _x: number, private _y: number) {
    }
    public get x(): number {
        return this._x;
    }
    public set x(value: number) {
        this._x = value;
    }
    public get y(): number {
        return this._y;
    }
    public set y(value: number) {
        this._y = value;
    }
    getInfo(): string {
        return `x=${this._x}, y=${this._y}`;
    }
}
```
File: circle.ts
```typescript
import {Shape} from './shape';
export class Circle extends Shape {   
    constructor(theX: number, theY: number, private _radius: number) {
        super(theX, theY); //Call superclass constructor
    }
    //theX and theY are Regular parameters, _radius is Parameter Property
    public get radius(): number {
        return this._radius;
    }
    public set radius(value: number) {
        this._radius = value;
    }
    //Override getOnfo Method:
    getInfo(): string {
        return super.getInfo() + `, _radius=${this._radius}`;
    }
}
```
File: ArrayDriver.js
```typescript
import { Shape } from './shape';
import { Circle } from './circle'
let myShape = new Shape(10, 15);
let myCircle = new Circle(5, 10, 20);
//declare array
let theShapes: Shape[] = [];
theShapes.push(myShape);
theShapes.push(myCircle);
for (let tempShape of theShapes) {
    console.log(tempShape.getInfo());
}
```
### Abstract Class
Cannot create instance of abstract class directly, only concrete subclasses
File: shape.ts
```typescript
export abstract class Shape{
    ...
    abstract calculateArea(): number; //Abstract method
}
let myShape = new Sape; //This is not working
```
File: circle.ts
```typescript
import {Shape} from './shape';
export class Circle extends Shape {   
    ...
    calculateArea(): number {
        return Math.PI * Math.pow(this._radius, 2);
    }
}
```
### Interface
Interface is a kind of abstract class, everything inside is abstract undefined method, 
subclass inheritancing this interface have to have all methods defined.
File: coach.ts
```typescript
export interface Coach {
    getDailyWorkout(): string;
}
```
File: CricketCoach.ts
```typescript
import { Coach } from "./coach";
export class CricketCoach implements Coach {
    getDailyWorkout(): string {
        return "Practice!";
    }
}
```
