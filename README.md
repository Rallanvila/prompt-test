# Code review standards

## Code review on syntax

- Check for typos, spelling and grammatical errors.

## Code review general code standards

- Unnecessary `console.log` should be removed.
- If ternary operator is used, a maximum of 5 code lines for that ternary is
  allowed. Else, prefer IIFE for regular code. For JSX, split into two separate
  conditionals instead.
- Ensure to use `typeof [variable] === 'undefined'` instead of
  `[variable] === undefined`.
- When doing fallbacks, use nullish coalescing `??` over short-circuiting `||`.
- When using array methods such as `.map`, `.reduce`, `.find` and contains
  conditionals inside, all exit points must have a `return` specified.

## Code review on Typescript code

- Report any Typescript errors found.
- `as` is not permitted. The only exception is `as const`.
- Where possible, typings should be normalized. Typings should avoid being too
  complex unions.

## Code review on code ordering inside file

When looking at a code file, it should be organized as follows top-down:

- Regular imports
- Interface definitions
- `makeStyles`, if any.
- `const` static variables, if any.
- The React component definition function.

## Code review on functions

- Check that destructure is not done on the parameters or arguments of
  functions. The only exception is the last argument of `createAsyncThunks`.

## Code review on `makeStyles`

- `makeStyles` is based on Material-UI v4 CSS-in-JSS styling syntax.
- Check that CSS class keys created in `makeStyles` are all used inside the
  React component of the same file. Report any that are unused and can be
  removed.
- Report if `flexDirection: 'column'` is used and tell user to modify the CSS to
  use CSS Grid instead, or other appropriate CSS that does not involve using
  `flexDirection: 'column'`.
- Report if the code contains CSS selectors/keys that use any type of combinator
  such as descendant or sibling selector. These are not permitted and must have
  an associated code comment above it explaining why it is used.

## Code review on CSS in `makeStyles`

- when using CSS flexbox, they need to explicitly apply a flex for each child in
  the flexbox.- For flex items, use `flexBasis` instead of `width`.
- Make sure to use `rem` not `px`.
- Try to enforce BEM naming conventions for class names.

## Code review on React components

- If the component has props destructured, the destructure must be done in the
  first line of the component.
- Avoid conditionally `return null` in the final JSX of the React component;
  prefer conditionally render the component instance used. However,
  `return null` is fine if is in an IIFE deciding what JSX to return.
- Component definitions must be typed with `FC`.
- Follow consistent component code structure:
  - Descructured props, `useStyles()`, hooks, selectors, constants, helper
    functions, `useEffect()`s, and finally, returning the JSX.
- When importing interfaces or types, use `import type` or `import { type }`.
- Do not attach native JavaScript event listeners directly.
- Report if code causes mutations.
- Provide context when using lazy-loaded slices and flag any issues.
- When using `.length` as a conditional, they must be explicitly checked using a
  comparator such as `>`, `>=`, `<`, `<=` or `===`.
  - e.g. Must use `children.length > 0`, not `!children.length`.
- Imports must be absolute paths, not relative paths.

## Code Review on Accessibility (a11y)

- Ensure aria-\* attributes are correct for custom components; no fake ARIA
  roles where native elements suffice.
- Inputs must have accessible labels; flag placeholders used as labels.

## Nice to haves

- Suggest places where we can use dynamic imports.
- Where possible, use `typeof` to reuse existing types instead of restating
  basic typings.
