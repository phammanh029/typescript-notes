# Utility types

## Awaited
Return type from promise
```
type A = Awaited<Promise<string>>; => string
type B = Awaited<Promise<Promise<number>>>; => number
type C = Awaited<boolean | Promise<number>>; => number | boolean
async function testFn() => 3
ReturnType<typeof testFn> => Promise<number>
Awaited<ReturnType<typeof testFn>> => number
```
## Partial
make property optional
```
interface Todo {
  title: string;
  description: string;
}
Partial<ToDo> = {
    title?: string;
    description?: string
}
```

## Required<Type>
make all property of type to required
```
interface Props {
  a?: number;
  b?: string;
}
Required<Props> => {
  a: number;
  b: string;
}
```

## Readonly<Type>
Make the type become readonly on all props
```
interface Todo {
  title: string;
}
const todo: Readonly<Todo> = {
  title: "Delete inactive users",
};
 
todo.title = "Hello";
Cannot assign to 'title' because it is a read-only property.
```

## Record<Keys, Type>
construct type of key, value
```
interface CatInfo {
  age: number;
  breed: string;
}
 
type CatName = "miffy" | "boris" | "mordred";
 
const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: "Persian" },
  boris: { age: 5, breed: "Maine Coon" },
  mordred: { age: 16, breed: "British Shorthair" },
};
 
cats.boris;
```

## Pick<Type, Keys>
Pick type from type
```
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}
 
type TodoPreview = Pick<Todo, "title" | "completed">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
 
todo;
```

## Omit<Type, Keys>
create new type by omit props

```
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}
 
type TodoPreview = Omit<Todo, "description">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
  createdAt: 1615544252770,
};
```

## Exclude<UnionType, ExcludedMembers>
exclude props from type
```
type T0 = Exclude<"a" | "b" | "c", "a">; => b | c
type T2 = Exclude<string | number | (() => void), Function>; => string|number

```

## Extract<Type, Union>
extract from type that matched with the union
```
type T0 = Extract<"a" | "b" | "c", "a" | "f">;
```

## NonNullable<Type>
make type not nullable (null|undefined are not allowed)
```
type T0 = NonNullable<string | number | undefined>; => string|number
```

## Parameters<Type>
construct tuple type from types used in parameer of a function type Type
```
type T0 = Parameters<() => string>; # [] because no param

type T1 = Parameters<(s: string) => void>; # [s: string]

declare function f1(arg: { a: number; b: string }): void;
type T3 = Parameters<typeof f1>; # [arg: {
    a: number; b: string
}] => const x: T3 = [{a: 1, b: 'test'}]

```

## ConstructorParameters<Type>
constructor tuple type
```
type T0 = ConstructorParameters<ErrorConstructor>;# [message?: string]
```

## ReturnType<Type>
construct type from return type of the function type
```
declare function f1(): { a: number; b: string };
type T0 = ReturnType<() => string>; # string

type T4 = ReturnType<typeof f1>;# { a: number; b: string; }

```

## InstanceType<Type>
Constructs a type consisting of the instance type of a constructor function in Type.
```
class C {
  x = 0;
  y = 0;
}
type T0 = InstanceType<typeof C>;# C

```

## ThisParameterType<Type>
extract the type of this, return unknown if no this
```
function toHex(this: Number) {
  return this.toString(16);
}
 
function numberToString(n: ThisParameterType<typeof toHex>) {
  return toHex.apply(n);
}
```

# Intrinsic string manipulation types
## Uppercase<StringType>
```
type x = Uppercase<'abc'|'def'> # 'ABC'|'DEF'
```
## Lowercase<StringType>
## Capitalize<StringType>
## Uncapitalize<StringType>

## Enum at compile time
```
enum LogLevel {
    ERROR,
    WARN,
    INFO,
    DEBUG,
  }
   
  /**
   * This is equivalent to:
   * type LogLevelStrings = 'ERROR' | 'WARN' | 'INFO' | 'DEBUG';
   */
  type LogLevelStrings = keyof typeof LogLevel;
  ```

  ## runtime literal
  ```
  type a = '1'|'2'
  type b = 'b'
  const fn = (p: `${a}${b}`) => p: '1b'|'2b'
  ```