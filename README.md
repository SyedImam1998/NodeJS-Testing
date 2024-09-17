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

```javascript
// tests/servicesWithDescribeAndAfterEach.test.js
const { fetchData } = require("../src/services");

jest.mock("../src/services");

describe("fetchData function tests", () => {
  // This will run after each test within this describe block
  afterEach(() => {
    jest.clearAllMocks();
  });

  test("fetchData should return mock data 1", () => {
    fetchData.mockReturnValue("mock data 1");
    expect(fetchData()).toBe("mock data 1");
    expect(fetchData).toHaveBeenCalledTimes(1);
  });

  test("fetchData should return mock data 2", () => {
    fetchData.mockReturnValue("mock data 2");
    expect(fetchData()).toBe("mock data 2");
    expect(fetchData).toHaveBeenCalledTimes(1); // This will pass because the mock state is cleared
  });

  test("fetchData should be called once in this test", () => {
    fetchData.mockReturnValue("another mock data");
    fetchData();
    expect(fetchData).toHaveBeenCalledTimes(1); // This will pass
  });
});
```

### Clear All Mocks:

Purpose: This function is used to clear any mocks that were set up during a test. It ensures that mocks don’t carry over from one test to another, preventing unintended interactions.

When to Use: Use jest.clearAllMocks() in afterEach when you have multiple tests that might share mocked functions or modules. It’s a good way to reset everything after each test.

### Jest Mock:

- Purpose: This is a type assertion in TypeScript that tells Jest to treat a function as a mock. It’s useful when you need to mock a function and access its mock-specific properties like .mockReturnValue() or .mockImplementation().

- When to Use: Use jest.Mock when you want to make sure a function behaves as a mock in a TypeScript project.

- Suppose you are writing tests for a function and that function is calling another function. So here we can use Jest mock where we can mock that internally called jest mock

```javascript

// src/util/add
function add(num1,num2){
  return num1+num2; 
}

// src/numbers
function numbers(num1,num2){
  const result=add(num1,num2);
  return result;
}


//

jest.mock('../src/util/add');

describe('...',()=>{

  it('return result',()=>{
    (add as jest.Mock).mockReturnedValue(3);
    const result=number(1,2);
    expect(result).toEqual(3)
  })
})


```


### SpyOn:

- Purpose: This function is used to spy on a method of an object, allowing you to track its calls, arguments, and return value without replacing the actual implementation.

- When to Use: Use jest.spyOn when you want to monitor how a method of an object is used during a test while keeping the original implementation intact.


```javascript

/// here getNotificationsByAssetId is called inside the getNotifications
//code 
const getNotifications=(assetId)=>{
  BatteryLib.getNotificationsByAssetId(assetId,defaultFields);
}

it('getNotification should return',async()=>{
  const spyOnGetBatteryNotifications=jest.spyOn(BatteryLib,'getNotificationsByAssetId').mockResolvedValueOnce(mockBatteryNotifications);

  const assetId='oooooooooooooooooo';
  const result=await getNotifications(assetId);
  expect(spyOnGetBatteryNotifications).toHaveBeenCalledWith(assetId,defaultFields);
  expect(result).toEqual([])
})

```
