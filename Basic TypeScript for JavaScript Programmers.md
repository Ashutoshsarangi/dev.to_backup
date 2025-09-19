### 1. **Basic Type Annotation**
   ```ts
   let helloWorld: string = "Hello World";
   
   function (nums: Array<number>): Promise<number>{
   }
   ```

### 2. **Interfaces**
   - Declaring and using interfaces.
   - Extending interfaces.
   - Declaration merging.

### 3. **Types**
   - Declaring types.
   - Using intersections.
   - Function types.

### 4. **When to Use `type` vs `interface`**
   ``` ts
type User = {
  name: string;
  age: number;
};

type Admin = User & {
  role: string;
};

interface User {
  name: string;
  age: number;
}

interface Admin extends User {
  role: string;
}


interface User {
  name: string;
}

interface User {
  age: number;
}

// Resulting type: { name: string; age: number }
   ```

🧠 When to Use What?
Use interface when:

- You're working with object-oriented code.
- You want to take advantage of declaration merging.
- You're defining public APIs or libraries.
Use type when:

- You need to define union, tuple, or primitive types.
- You want to create complex compositions using intersections.

---

### 5. **Type Inference**

TypeScript can automatically infer types based on the assigned value:

```ts
let message = "Hello"; // inferred as string
let count = 42;        // inferred as number
```

You can mention that **explicit typing is optional** when the context provides enough information.

---

### 6. **Union and Literal Types**

```ts
type Status = "success" | "error" | "loading";

function showStatus(status: Status) {
  console.log(status);
}
```

Useful for modeling finite states.

---

### 7. **Optional and Readonly Properties**

```ts
interface User {
  name: string;
  age?: number; // optional
  readonly id: number; // cannot be changed
}
```

---

### 8. **Enums**

```ts
enum Role {
  Admin,
  User,
  Guest
}

const userRole: Role = Role.Admin;
```

Great for defining named constants.

---

### 9. **Generics**

```ts
function identity<T>(arg: T): T {
  return arg;
}

const output = identity<string>("Hello");
```

Generics allow you to write reusable and type-safe code.

---

### 10. **Type Assertions**

```ts
let someValue: unknown = "this is a string";
let strLength = (someValue as string).length;
```

Useful when you know more about the type than TypeScript does.

Reference:-

1. https://www.typescriptlang.org/docs/handbook
