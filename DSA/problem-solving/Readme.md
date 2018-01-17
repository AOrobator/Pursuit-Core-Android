# Title: DSA Review
Tags: dsa, problem solving

# Objectives

- Review Unit 4 Final App
- Review problem solving techniques.
- Apply problem solving techniques to past dsa problems.
- Practice using unit tests to verify solutions.

# Resources

- [Hacker Rank](https://www.hackerrank.com/)
- [Khan Academy](https://www.khanacademy.org/computing/computer-science/algorithms/)

## App Problem and Review

[Github](https://github.com/C4Q/AC-AndroidTest-U4Final)

- The test app displays color names, colored in their color names.
- Deeper review of sorting will happen later in the lecture.
- Better review of Networking will happen again tomorrow.

## Highlights

* Using Retrofit vs AsyncTask vs OkHttp
[Retrofit](https://github.com/Luminarydoom/AC-AndroidTest-U4Final/blob/master/app/src/main/java/nyc/c4q/androidtest_unit4final/MainActivity.java)
[OkHttp](https://github.com/7sco/AC-AndroidTest-U4Final/blob/master/app/src/main/java/nyc/c4q/androidtest_unit4final/MainActivity.java)
[AsyncTask](https://github.com/STaverasAC/AC-AndroidTest-U4Final/blob/master/app/src/main/java/nyc/c4q/androidtest_unit4final/MainActivity.java)

* Implementing selection sort vs bubble sort


#### Oh My Grades!
- If you think your app does all these things (and it builds), slack me.
- If you made commits before 10pm but didn't get to push it, you may do so and slack me.


# Problem statement

> Create a function `selectEvenNumbers` that will take in an array of numbers and return an array of only even numbers. If there are no even numbers, return the empty array.

Skeleton app: https://github.com/C4Q/AC-Android-DSA-Problems

# 1. Read the problem at least three times (or however many makes you feel comfortable)

* **You can’t solve a problem you don’t understand.** 
* There is usually a difference between the problem and the problem you think you are solving. 
* It’s easy to start reading the first few lines in a problem and assume the rest of it because it’s similar to something you’ve seen in the past.

#### Ask questions like:
* *How can a computer tell what is an even number?* Divide that number by 2 and see if its remainder is 0.
* *What are the data types of the elements in the array?* Numbers

# 2. Identify what needs to be done

* Be **clear** about what the problem is.

#### Ask questions like:
* *What is the goal of `selectEvenNumbers`? What am I returning at the end of this function?* The goal is to take all the even numbers and return them in an array. If there are no even numbers, return an empty array.

# 3. For a complex programming problem, break the problem up into simpler pieces

* A problem could be made of different components that come together to form the solution.
* Start with telling the computer how to solve the simplest problem.

#### Ask questions like:
* *What are the different components of `selectEvenNumbers`?* 1) Deciding if a number is even or not. 2) Creating an array of even numbers
* *What is the simplest version of the problem?* An array that contains just one even number and we return it. Or no even numbers at all and we return empty array. What other simpler scenarios are there?

# 4. Write Pseudocode

* Writing out pseudocode that you can translate into code will help with defining the structure of your code and make coding a lot easier.
* **Don’t get caught up with the syntax. Focus on the logic and steps.**

Here is an example of pseudocode that has more words:
```
function selectEvenNumbers

create an array evenNumbers and set that equal to an empty array

for each element in the given array
  see if that element is even
    if element is even (if there is a remainder when divided by 2)
      add to that to the array evenNumbers

return evenNumbers
```

Here is an example of pseudocode that has fewer words:
```
function selectEvenNumbers

evenNumbers = []

for i = 0 to i = length of evenNumbers
  if (element % 2 === 0) 
    add to that to the array evenNumbers

return evenNumbers
```

# 5. Test your code
* Work through the solution manually with sample data (preferably while in pseudocode)
* Think up edge cases and corner cases for your solution.

#### Ask questions like:
* *How do I verify my solution is correct?* Write unit tests. Walk through the solution with sample data manually.
* *What are some corner cases I need to be aware of?* Are negative numbers even or not? Are decimals even or not? Is 0 even or not? Is there a limit to even numbers?

# 5. Practice, Practice, Practice.

**DSA Problem 1:**

Given an array of integers, write a method called int[] removeDupes(int[] input) that returns a new array of just the unique values.

You may use additional data structures in your solution.

```
removeDupes(new int[]{1, 2, 3, 4, 5, 1, 2, 3}); 

// returns {4, 5} 

removeDupes(new int[]{7, 7, 7, 7, 7}} 

// returns {}
```

**DSA Problem 2:**

Given a string, write a method called countTheLetters takes a string input and returns a map containing a count for each of the letters in the string.

```
countTheLetters("dog");
// returns a map containing the pairs {d: 1, o: 1, g: 1}

 countTheLetters("elephant"); 
// returns a map containing the pairs {e: 2, l: 1, p: 1, h: 1, a: 1, n: 1, t: 1} 

countTheLetters("llama");
// returns a map containing the pairs {l: 2, a: 2, m: 1}
```

**In class exercise**: Implement `selectEvenNumbers`. 

Submit your implementation code or a link to it for in-class exercise.

# 6. SelectionSort Review

How we could have implemented `selectionSort` following the steps above.


# Summary

* When solving a problem 

1. Read the problem at least three times (or however many makes you feel comfortable)

2. Identify what needs to be done

3. For a complex programming problem, break the problem up into simpler pieces

4. Write Pseudocode

5. Test your code