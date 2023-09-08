## 1. Levels of Testing
![[2. V-Model.png]]
## 2. Unit Testing
Let's say you have a project with ten Java classes. Some of these classes are entity classes and some are control classes. We can begin by testing each of the entity classes. A class named student is required to be tested. It has the following private attributes:
- Name
- Address
- Contact
- DOB
- Course

To test this class, you want to test all of these attributes through their accessors and mutators to ensure input and output are exactly as anticipated. A strategy is to be built to test these attributes through methods.

The benefits of unit testing are as follows:
1. Unit testing helps teams identify defects early at development time otherwise small defects will lead to larger problems in the later stage.
2. As units are tested in isolation, it allows for easy detection of defects.
3. As you see the code pass or fails to improve, unit testing promotes confidence in code.
4. Encourage code review between team members.

## 3. Best Practices
1. Make test cases independent of each other & without side effects. Side effects such as unreachable branches (statements never reached).
2. Make test cases independent of **execution order.** Order can be specified in JUnit. You should be able to run any test cases, in any order and all the test cases.
3. Test **only one thing** in a test. This is one of the mistakes new developers make. You should not test more than one thing in one test case. Otherwise, you will end up finding a problem but not the cause. For example, You should not write a test case that tests 'age is not greater than 100 and name is not more than 30 characters long'. Separate them and run them in isolation as age and name do not have anything to do with each other.
4. **setUp()** helps you create instances of the classes, populate values, etc. **test()** is the annotation used to identify a method as a test cases in a test class. **tearDown()** provides an opportunity to perform a clean-up after each test case is done running.
5. Name tests sensibly & consistently: Test cases should be named not very long but also not too short For example: 'testNameIsNotGreaterThan30Characters' is acceptable, and 'testNameIsofLength' is not acceptable as one will have to look at the code to find the boundary value but also is not consistent. The key is to strategise the naming of the test cases and be consistent throughout.
6. Write descriptive messages in assertions or displays: You may not find value in this standard when writing only a couple of test cases but in this unit and your future, you will write test cases in hundreds and you will appreciate your team writing descriptive assertions and displays so you know exactly what test failed.
7. **Categorise** tests, i.e. unit-, integration-, system- or short- or long-running
8. **Do no**t hard-code file locations in the FS
9. Mock external dependencies such as files, database, URL, etc: Mocking the data is a great way of making testing quick and easy, however, we vary that you do not want to spend a lot of time mocking the data and have no implementation (TDD reference) and hence causing code smell.

## 4. Triangle Problem
Let's look at the following example. The example depicts a program that carries out the following task:

>[!question]
>Given 3 inputs, (a, b, c) with each of the variables in the range [1,200], decide whether the three values can form a triangle and if they do, what triangle will they form?

Let's take following test case:
- a = 60
- b = 60
- c = 60

We know a triangle with equals lengths will make an equilateral triangle. But in this example, the 'black boxed' program is expected to check that and form a triangle, if possible. That's our expectation. We do not know how and what the code is doing. Only that we would expect the program to do correct based on the description provided. The following image highlights the example.

![[2. Triangle Test.png]]

[[Module 1#Black Box Testing]] 
