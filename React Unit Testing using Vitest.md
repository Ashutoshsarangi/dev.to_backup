## Introduction

Types of Testing 

1. Unit Testing
2. Component Testing
3. Integration Testing
4. E2E Testing

**Unit Testing**

- Here I am using Vitest for the unit testing rather than jest.

Vitest is a modern test runner that is designed to work well with Vite, a build tool for React, Vue, etc

**Speed:**

- Vitest is designed to be fast. It takes advantage of Vite's fast module server to quickly run tests in parallel using native **ES modules**, which can result in faster test execution times compared to Jest.

**ESM Support:**

- Vitest has built-in support for ES modules, allowing you to write tests using native ESM syntax without needing to transpile your code

**Vite Compatibility:**

- If you're already using Vite in your project, using Vitest for testing can make your setup simpler and more consistent, as they're designed to work well together.

**Mocking:**

- Vitest provides a simple and intuitive API for mocking modules, which can make your tests easier to write and understand.

``` React
import { expect, describe, it, vi, beforeEach, afterEach } from "vitest";
import * as ApiHelper from "./Api.helpers";

// Here we need to import these in every test file, but there is a provision to do it in global level

//lets say we want to spy some API calls
 spyGetAllCategory = vi
        .spyOn(ApiHelper, "getAllCategory")
        .mockResolvedValue([
          {
            id: "12",
            name: "asda",
          },
        ]);

      spyGetQuestions = vi.spyOn(ApiHelper, "getQuestions").mockResolvedValue([
        {
          type: "my",
          difficulty: "easy",
          category: "common",
          question: "How are you ?",
          correct_answer: "C",
          incorrect_answers: ["A", "B", "D"],
        },
      ]);
    });

    afterEach(() => {
      vi.restoreAllMocks();
    });

// how to test it
 it("getQuestions", async () => {
      await ApiHelper.getQuestions({ category: "simple", difficulty: "easy" });
      expect(spyGetQuestions).toHaveBeenCalledOnce();
      expect(spyGetQuestions).toHaveResolvedWith([
        {
          type: "my",
          difficulty: "easy",
          category: "common",
          question: "How are you ?",
          correct_answer: "C",
          incorrect_answers: ["A", "B", "D"],
        },
      ]);
    });

```


few Other scenarios where you will write unit test cases

``` React
 describe("getDynamicOptions", () => {
    it("getDynamicOptions, Only checking the Length", () => {
      const arr = ["ABC", "DEF", "IJK", "XYZ"];
      expect(getDynamicOptions(arr).length).toBe(4);
    });

    it.fails("getDynamicOptions, Here it would fail", () => {
      const arr = ["ABC", "DEF", "IJK", "XYZ"];
      expect(getDynamicOptions(arr)).toEqual(["ABC", "DEF", "IJK", "XYZ"]);
    });
  });
```


**Example on toContainEqual**

```React
describe("updateResponseWithIds", () => {
    it("updateResponseWithIds should have correctAnswerId", () => {
      const questions = {
        type: "abc",
        difficulty: "easy",
        category: "film",
        question: "Hey there, How are you ?",
        correct_answer: "B",
        incorrect_answers: ["A", "D", "C"],
        id: "easy_0",
        renderOption: ["A", "D", "B", "C"],
      };
      const dataSet = {
        response: "ABC",
        responseId: "easy_0",
      };
      expect(
        updateResponseWithIds(questions, dataSet)["easy_0"]
      ).toContainEqual({
        correctAnswerId: "RESPONSE_easy_0_2",
        correct_answer: "B",
        userAnswerId: "easy_0",
        user_answer: "ABC",
      });
    });
  });
```


**toMatchObject and toContainEqual**

- These are two different matchers in Vitest that are used for different purposes:

**toMatchObject:**

- This matcher is used to check that a JavaScript object matches a subset of the properties of an object.
- It will match received objects with properties that are not in the expected object.

``` React
test('toMatchObject example', () => {
  const received = { a: 1, b: 2, c: 3 };
  expect(received).toMatchObject({ a: 1, b: 2 });
});
//In this example, the test will pass because received object has at least the properties { a: 1, b: 2 }.

```

**toContainEqual:**

- This matcher is used when you want to check that an array or iterable contains a value that equals a given value.

```React
test('toContainEqual example', () => {
  const received = [{ a: 1, b: 2 }, { a: 2, b: 1 }];
  expect(received).toContainEqual({ a: 1, b: 2 });
});
//In this example, the test will pass because received array contains an object that equals { a: 1, b: 2 }.
```


**In summary,** 

- **toMatchObject** is used to check that an object has a subset of properties, while **toContainEqual** is used to check that an array contains a specific value.


**vi.mock vs vi.fn vs vi.spyOn**

vi.mock, vi.fn, and vi.spyOn are functions provided by Vitest, a modern test runner, for creating mock functions and spying on function calls. 

**vi.mock:**

- This function is used to create a mock module. You can use it to mock the return value of a module for testing purposes.

```React
import { mock } from 'vitest'

mock('./module-to-mock', {
  mockedFunction: () => 'mocked value',
})
```

**vi.fn:**

- This function is used to create a mock function. You can use it to replace a function in your code with a mock function that you can assert on.

```React
import { fn } from 'vitest'

const mockFunction = fn(() => 'mocked value')
```

**vi.spyOn:**

- This function is used to create a spy on a function. This allows you to track calls to the function and replace its implementation for testing purposes.

```React
import { spyOn } from 'vitest'

import * as objectToSpyOn from './random.utils.js

spyOn(objectToSpyOn, 'methodToSpyOn').mockImplementation(() => 'mocked value')

// after that we need to restore it
 vi.restoreAllMocks();

```


I hope this is clear, Feel free to reach out to me, if there would be any concerns.


Reference:-

1. https://vitest.dev/api/vi.html#vi-mock
