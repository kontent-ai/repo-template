# Typescript Project Guidelines

## General Code Quality
- Always prefer functions and composition over classes and inheritance
- Do not use OOP unless necessary in API, e.g. web components
- Use functional programming principles like pure functions, immutable data structures, higher-order functions, and function composition
- Always prefer "const" over "let" unless necessary
- Always prefer "unknown" type over "any"
- Use early returns to reduce nesting
- Use clear, self-documenting variable and function names
- Prefix event parameters with "on" (e.g., `onClick`)
- Prefix event handler implementation with "handle" (e.g., `handleClick`)
- Always prefix boolean variables with `should`, `is`, `has`, `does`, or similar
- Define all type properties as readonly:
  ```typescript
  type Type = {
    readonly id: Uuid;
    readonly items: ReadonlyArray<Item>;
    readonly ids: ReadonlySet<Uuid>;
  }
  ```
- Do not overuse emojis
- Use comments only for necessary implementation details
- When adding a new npm package, always use npm view <package> version to get the newest possible version.

## React-Specific Rules
- Prefer local useState over global state
- Define component props like `type Props = { }` and use directly in component parameters
- Do not use `React.FC` or `FC` types and remove them
- Instead of `PropsWithChildren`, use `{ readonly children: ReactNode; }`. The children must never be optional using the question mark operator
- Do not use React prefix in imports (GOOD: `ReactNode` BAD: `React.ReactNode`)
- Only write functional components
- To resolve import name collision, use `Component` suffix in import alias
  ```typescript
  // File: /containers/ItemEditor.tsx
  import { A as AComponent } from '../components/A.tsx';
  
  export const A = () => <AComponent />;
  ```
- Do not add empty lines in JSX code.
- Only React components defined at the module level can return JSX
  ```typescript
  // BAD - hooks must not work with JSX:
  const useCard = () => <div>...</div>;
  // BAD - JSX must not be rendered in plain functions:
  const renderCard = () => <div>...</div>
  // BAD - hooks must not return a component
  const useModal = () => {
    const Modal = () => <div>...</div>;
    return Modal;
  };
  ```
- Do not create JSX variables or render functions in component closures. Instead:
  - Inline the JSX for simple cases
  - Extract to individual small components within the module for complex cases

## Import Organization
- Always include file extensions in relative imports

## Project Memories
- ALWAYS keep the `’` character when encountered in code or text - it must be preserved exactly as is
- Apply all rules to existing code in modules you modify.
