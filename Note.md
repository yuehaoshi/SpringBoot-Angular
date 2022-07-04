# Installation
https://github.com/darbyluv2code/fullstack-angular-and-springboot/blob/master/install-angular-tools/mac/install-mac.md

# Definitions

Traditional Application:
Each user action results in a full HTML page load

Single Page Application
Partial Update instead of full page load on user actions, e.g. google maps, gmails

**Angular** is a framework for building modern single-page applications, e.g., Citi Bank, MSBox (www.madewithangular.com)

# TypeScript
TypeScript, a superset of JavaScript and ECMAScript
Web Browser donot understand TS, need to use tsc to convert .ts to .js (tsc mydemo.ts), and then run js code through node (node mydemo.js)
Define Variables:
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
Print:
```
console.log(found);
console.log("The grade is" + grade);
console.log("Hi "+ firstName + " " + lastName);
//use template strings
console.log(`Hi ${firstName} ${lastName}`)

export {};
//https://bobbyhadz.com/blog/typescript-cannot-redeclare-block-scoped-variable#:~:text=The%20error%20%22Cannot%20redeclare%20block,block%20and%20use%20ES%20modules.
```
Run ts file:
```
tsc filename.ts
node filename.js
```
Loops:
```
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
Classes:
```

```
