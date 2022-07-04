
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
