# NodeJS-Testing

### Describe:

- This would help the wrap multiple tests in one.

```ts
describe('Math Function',()=>{
    test(.....)
    test(.....)
    test(.....)
    test(.....)
})
```

### Expect:

- Here you would be expecting the result what it would be, if it matches then test case will pass or else it will fail.

```js
import { add } from "./src/math";

test("should add 2 numbers", () => {
  expect(add(1, 2).toBe(3)); // if add function returns 3 then test pass.
});
```

### AfterEach:

- This function in exceuted after every test case beginning.

```javascript
describe("test", () => {
    
  afterEach(() => {
    jest.clearMocks();
  });


  test(.....)
  test(.....)
  test(.....)
  test(.....)
});
```

### Jest Mock:

- 
