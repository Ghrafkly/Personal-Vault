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

When performing [[Uni/Software testing, quality and standards/1. Modules/Module 1#Black Box Testing|Black Box Testing]] we have no knowledge of the internal structure and are testing the behaviour of the software not how it solves a problem.

## Black Box Testing Techniques

### Functional Testing
Recall involves:  
- Function: a program can be considered a function in the sense that program inputs form its domain and program outputs form its range.
- Domain: the domain of a function is the set of values that we are allowed to plug into our function. This set is the x values in a function such as f(x).
- Range: the range of a function is the set of values that the function assumes. This set is the values that the function shoots out after we plug an x value in. They are the y values.

When testing against a known specification, we are conducting specification-based testing.

Now in boundary value testing, we assume the fault occurs at the extremes of the input values. There are two considerations. First, consider whether we will concern ourselves with invalid values. Second, consider when we assume fault occurs due to a single variable or due to two or more variables. Based on these considerations, we have
1. Normal BVT.
2. Robust BVT.
3. Worst-case BVT.
4. Robust worst-case BVT.
### Equivalence Class Testing
In boundary value testing, we do not get the chance of having a sense of complete testing and avoiding redundancy. Equivalence class testing is based on two considerations of BVT - robustness and single/multiple fault assumptions. Through this, two distinctions are created, one is a weak/strong distinction based on the single vs multiple fault assumptions results. Two is a normal/robust distinction based on invalid data yields. Based on these two distinctions we have the following types of equivalence class testing:
1. Weak Normal.
2. Strong Normal.
3. Weak Robust.
4. Strong Robust.

_**But what really is an Equivalence class?**_ An equivalence class is a partition of a set, where partition refers to a collection of mutually disjoint subsets, the union of which is the entire set. The benefit is that the entire set is represented which provides a form of completeness, and the disjointedness ensures avoidance of redundancy. 

_**How are the subsets determined?**_ The subsets are determined by an equivalence relation, the elements of a subset have something in common. 

_**How ECT is used?**_ The idea of equivalence class testing is to identify test cases by using one element from each equivalence class. Choose equivalence classes in a way that will reduce redundancy.

### Decision Table Based Testing
We use decision tables to represent and analyse complex logical relationships between variables. They are ideal where numbers of combinations of input variables are possible and finding an error or misinterpretation is easy using this representation. A complex boolean expression such as 
`(!A || B) && C (A && C)(B || C)` can be solved easily using a decision table. 

A decision table has four portions: the part to the left of the bold vertical line is the stub portion: To the right is the entry portion. The part above the bold horizontal line is the condition portion, and below is the action portion. Thus, we can refer to the condition stub, the condition entries, the action stub, and the action entries. A column in the entry portion is a rule. Rules indicate which actions, if any, are taken for the circumstances indicated in the condition portion of the rule. You will see an example in the video below.

But of all the functional testing methods, testing based on decision tables is the most rigorous because of their strong logical basis.

So DTBT is a form of testing where a decision table is used to represent a logical relationship between inputs, conditions, actions and rules. You need to practice to be able to create a good decision table. Nonetheless, it is cause-and-effect graphing where inputs are shown to the left side and rules to express the flow of the data to the right. The most one can learn from DTBT and cause-and-effect is that, if there is a problem at an output, the path back to the inputs that affected the output can be retracted. However, there is little support for identifying the test cases. 

#### Guidelines and observations

Guidelines and observations are suitable when there are:
- a lot of decision-making
- logical relationships among input variable conditions
- the cause-effect relationship between conditions and actions
- evaluations involving subsets of conditions.

Decision tables do not scale up very well and can be iteratively defined.