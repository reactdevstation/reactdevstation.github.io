---
layout: post
title: Essential Array Functions
header-color: rgb(33, 33, 33);
image: "assets/img/thumbnails/react.png" #seo tag
tags: [ES6, JavaScript]
excerpt_separator: <!--more-->
# published: false
---

In this post, we are going to discuss essential JavaScript functions that every JS developer should know, in order to make their job easier and cleaner. We need to use these functions in order to effectively utilize the functional programming paradigm of JS.
<!--more-->

We'll be using **ES6 syntax** for the examples here, if you want to brush up the ES6 skills then [follow this link](/2020/03/18/es6-for-react.html). Following functions will be covered int this post.
* TOC
{:toc}

### map
> The map() function creates a new array generated from the results of callback function on every element within the array.

The most common array function in React eco-system, we often use to create JSX for the items in an array. Map function also provides the index along with the item to the **callback function**.

```javascript
let ls = [3, 5, 7] // 3, 5, 7
let lsMul2 = ls.map( item => item * 2 ) // [6, 10, 14]

// another case
let jsxList = ls.map( (item, index)=> <li key={index}>{item}</li> )
```
In the first case, we got a new array with array "ls" elements multiplied by 2. And in the second case we are creating JSX list items with key and value.
### filter
> The filter() method creates a new array with all elements that pass the test set by the callback function.

```javascript
let ls   = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let even = ls.filter( item => item % 2 === 0 ) // [2, 4, 6, 8, 10]
```
In this case, we create a new array that contains even numbers present in the array "ls".

### forEach
> The forEach() method executes a callback function once for each array element. 

The callback function in forEach should not contain return statements unlike map function.

```javascript
let ls = ['a', 'b']
ls.forEach(item => console.log(item))
```
It generates following output:
```output
a
b
```

The forEach method can also send index to the callback function.
### every and some
> The every() method tests whether all elements in the array pass the test set by the callback function. It returns a Bool.

This function is used to check that all the elements of an array fullfil a given condition. It returns true only if all the elements fulfil the condition, otherwise it returns false.

```javascript
let ls1 = [1, 4, 5, 7, 9]
let ls2 = [1, 4, 5, 20, 9]

// callback will return true if an item is less than 10
ls1.every(item => item < 10 ) // returns true
ls2.every(item => item < 10 ) // returns false
```

>The some() method tests whether at least one element in the array passes the test set in the callback function. It also returns a Bool.

The some() is opposite to the every() method. It returns true, if at-least a single element fulfills the condition set in the callback function, otherwise it returns false. 

```javascript
let ls1 = [1, 4, 5, 7, 9]
let ls2 = [1, 3, 5, 7, 9]

// callback will return true if at-lease on even number is present
ls1.some(item => item % 2 === 0 ) // returns true
ls2.some(item => item % 2 === 0) // returns false
```

### sort
> The sort() method sorts the elements of an array in place and returns the sorted array, default is in ascending order. Elements are first converted into strings and comparison is done on UTF-8 unit values. 

If we try to sort an array of numbers, we will get wrong result because number values are first converted to string and then compared. So we have to provide our custom comparator. We can also define comparators for comparing certain values in an object
```javascript
let numberComparator = (a, b) => a - b
let arr = [20, 10, 4, 1, 100]

// wrong order
arr.sort()
console.log(arr) // prints [1, 10, 100, 20, 4]

// correct order
arr.sort(numberComparator)
console.log(arr) // prints [1, 4, 10, 20, 100]
```

### reduce
> The reduce() method executes a reducer function as a callback on each element of the array, resulting in a single output value.

```javascript
let array1 = [1, 2, 3, 4]
let reducer = (accumulator, currentValue) => accumulator + currentValue;
console.log(array1.reduce(reducer))

let arr = [{id: 1, price: 10}, {id:2, price: 20}, {id:3, price: 30}]

let reducer = (accumulator, currentValue) => ({ totalPrice: accumulator.totalPrice + currentValue.price})
// passing a default value to the accumulator
arr.reduce(reducer, {totalPrice: 0})
```

On the start, accumulator gets the first element of array if accumulator is not provided in the reducer which is second parameter. But after that, accumulator gets the returned values of the reducer. In the first example, we are getting a simple sum. In the second example, we wanted to spice things up a little by creating an object and incrementally increasing its totalPrice property.


### includes
> The includes() checks to see if an elements exists in an array; returns bool.

```javascript
let arr = ['apple', 'orange', 'mango']
console.log(arr.includes('orange')) // true
console.log(arr.includes('strawberry')) // false
```

### splice
> The splice() method allows us to remove, add or modify elements of an array in-place.

Its parameters are
1. index
2. delete count: how many elements you want to remove
3. new elements to be added

```javascript
let fruits = ['Apple', 'Orange', 'Mango']

// when we want to add something, we specify delete count 0
fruits.splice(1, 0, 'Strawberry') // ['Apple', 'Strawberry' ,'Orange', 'Mango']
// removing element at index 3
fruits.splice(3, 1) // ['Apple', 'Strawberry' ,'Orange']
// replacing element
fruits.splice(2, 1, 'Melon') // ['Apple', 'Strawberry' ,'Melon']
// adding multiple items
fruits.splice(0, 0, 'Watermelon', 'Date') // ['Watermelon', 'Date' ,'Apple', 'Strawberry' ,'Orange']
```
We had to add a lots of examples because the splice() method can do a lots of things. First we can add items to the array, for that we have to set delete count as 0. Second we can replace elements, by adding elements at index and specifying delete index. We can delete elements by providing no elements and delete count.

Splice only returns the elements that are deleted from the array, otherwise it returns an empty array. All the modifications happen in original array.

### push and pop
>The push() method adds one or more elements to the end of original array and returns the new length of the array.

>The pop() method removes the last element from original array and returns that element.

```javascript
let fruits = ['Apple', 'Orange', 'Mango']
fruits.push('Melon') // ['Apple', 'Orange', 'Mango', Melon]
let length = fruits.push('Date', 'Strawberry') // ['Apple', 'Orange', 'Mango', Melon, 'Date', 'Strawberry']

// removing element from the end
fruits.pop() // ['Apple', 'Orange', 'Mango', Melon, 'Date']
```
### shift and unshift
> The shift() method removes the first element from original array and returns that removed element.
 
 > The shift() method adds an element to the start of the original array and returns the length of the array.

```javascript
let fruits = ['Apple', 'Orange', 'Mango']
fruits.shift() // ['Orange', 'Mango']

fruits.unshift('Date', 'Melon') // ['Date', 'Melon', 'Orange', 'Mango']
```