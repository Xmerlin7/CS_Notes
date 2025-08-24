- union types
```TypeScript
let stringOrNumber: string | number;
```
- Array types
```TypeScript
let arr: string[];
let arr: (string | number)[];
```
- Object types
```TypeScript
let obj : {
userName: string
age: number
isAdmin: booleans
phone?: number // (optional property) notRequired to define the object
}
obj = {
userName = "Merlin",
age = 23
//error for not assigning isAdmin property
}

let obj2 : {
isString : bolean
theme: "dark" | "light"
}
const userObj : obj2 = {
	isString: true,
	theme: "pink" //error
}
```

- Any types
```TypeScript
let arr: any
arr = [true, "seif", 15]
```

---
- Functions 
```TypeScript
//define return type
let fn = (): string => {
	return (sting)
}
//define it's parameters and its return
let fn2 = (name : string): void => {
	return(name)// error
}

// Defining a 'User' type
type User = {
  name: string;     // 'name' is required and must be a string
  age?: number;     // 'age' is optional and, if provided, must be a number
};

// Function to greet the user
function greet(user: User): string {
  return `Hello, ${user.name}!`;  // Safely accessing the 'name' property
}

```
---
- INTERFACES
```typescript
interface IUser {
  name: string;
  age: number;
}

interface IAdmin extends IUser {
  permission: bolean;
}
const perm : IAdmin = {
	name :"tom",
	age: 23,
	permission: true
}
```

---
- Generics
```typescript
// Defining a generic interface
interface Response<T> {
  data: T;          // The data can be of any type defined when using the interface
  error?: string;   // Optional error message
}

// Using the generic interface with different types
const userResponse: Response<{ name: string; age: number }> = {
  data: { name: "Seif", age: 15 },
  error: undefined,
};

const productResponse: Response<{ id: number; title: string }> = {
  data: { id: 1, title: "Laptop" },
  error: "Failed to load product.",
};

// Function to handle the response
function handleResponse<T>(response: Response<T>): void {
  if (response.error) {
    console.error("Error:", response.error);
  } else {
    console.log("Data:", response.data);
  }
}

// Example usage
handleResponse(userResponse);      // Output: Data: { name: 'Seif', age: 15 }
handleResponse(productResponse);   // Output: Error: Failed to load product.


```
