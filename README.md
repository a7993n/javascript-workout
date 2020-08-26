<div align="center">
  <img height="60" src="./img/javascript-logo.png">
  <h1>JavaScript Workout 💪🏼</h1>


<span>This is a collection of short JavaScript programming solutions that you will encounter everyday.

As with any programming language, JavaScript has its own way of solving problems. Knowing how to do basic data type conversion or array manipulations will make you deliver your solutions faster. 😊

I hope this helps you to be more efficient JavaScript developer🤟💀🤟

Feel free to reach out to me🤙 <br />

<a href="https://www.mydatahack.com" target="_blank">Blog</a> || <a href="https://github.com/aws-lambda-template-generator" target="_blank">Open Source Project</a> || <a href="https://thehondas.bandcamp.com/" target="_blank">Band Camp</a>

If you want to make a suggestion or contribute to this, feel free to pull the repo and make a pull request!

</span>
<br />
<h1>Topics</h1>
<p><b>(1) Array of objects</b></P>
<p><b>(2) Array</b></P>
<p><b>(3) String format</b></P>
<p><b>(4) Spread Syntax</b></P>
</div>
<br />

---

### (1) ARRAY OF OBJECTS
---

<b>1. Create an array of number from an array of an object and do calulation</b>

input 
```javascript
const input = [{"name": "name A", "score": 2},
{"name": "name B", "score": 1},
{"name": "name C", "score": 4},
{"name": "name D", "score": 5}]
```

output
```javascript
# (1) Create an array
[2, 1, 4, 5]

# (2) Return Sum of the array
12

# (3) Return Max
5
```

<details><summary><b>Answer</b></summary>

<b>Array.prototype.map</b> will create an array of the value from the selected key in the JSON object. 

<b>Array.prototype.reduce</b> will accumulate the number. The firt argument is the accumulator function and second argument is the starting value.

<b>Function.prototype.apply</b> takes this value as a first argument and an array as a second argument. It will apply the function to the array. For example, Math.sum.apply(null, [1, 2, 3]) will sum up all the numbers in the array. Math.sum works with Math.sum(1, 2, 3). But, to make it work with an array, we need to use apply function.

```javascript
# (1)
input.map(x => x.score)

# (2)
imput.map(x => x.score).reduce((a, b) => a + b, 0)

# (3) 
Math.max.apply(null, input.map(x => x.score))
```
</details>

<b>2. Getting max datetime from a string from the object array</b>

input
```javascript
const input = [{datetime: '2020-04-29T03:23:48Z', spend: 300.00},
{datetime: '2020-06-03T23:26:43Z', spend: 300.00},
{datetime: '2020-05-30T17:28:14Z', spend: 300.00},
{datetime: '2020-06-27T18:21:07Z', spend: 300.00}]
```

output - return it as a Date object in the local time
```javascript
Sun Jun 28 2020 04:21:07 GMT+1000
```

<details><summary><b>Answer</b></summary>

We can convert the string into a local time with new Date(). Then use the technique from question 1 to create an datetime array and apply max.

```javascript
new Date(Math.max.apply(null, input.map(x => new Date(x.datetime))));
```
</details>

<b>3. Adding new key-value pair in all the objects in an array</b>

You have an array of an object with name. Can you add an unique id to all the objects?

input
```javascript
const input = [{name: 'John'}, {name: 'Tyson'}, {name: 'Joan'}]
```

output
```javascript
[{name: 'John', id: 1}, {name: 'Tyson', id: 2}, {name: 'Joan', id: 3}]
```

<details><summary><b>Answer</b></summary>

We can use the map and use the index to add an unique id that increments.

```javascript
input.map((data, index) => ({name: data.name, id: index + 1}));
```

</details>

<b>4. Sorting object array by a key</b>

input
```javascript
const input = [{ name: "John", score: "432"},
 { name: "Joe", score: "125"},
 { name: "Zoe", score: "320"},
 { name: "Ziggy", score: "532"},
 { name: "Dave", score: "211"},
 { name: "Sarah", score: "621"}
];
```

output - sort it in descending order
```javascript
0: {name: "Sarah", score: "621"}
1: {name: "Ziggy", score: "532"}
2: {name: "John", score: "432"}
3: {name: "Zoe", score: "320"}
4: {name: "Dave", score: "211"}
5: {name: "Joe", score: "125"}
```

<details><summary><b>Answer</b></summary>
<b>Array.prototype.sort</b> takes a callback function as a sorter. We can write a simple call back function and pass it.

```javascript
const sorter = (key) => {
  return (a, b) => {
    if (a[key] > b[key]) {
      return -1;
    } else if (a[key] < b[key]) {
      return 1;
    } else {
      return 0;
    }
  }
}

input.sort(sorter('score'));
```

</details>

<b>5. Sorting object array by multipe keys</b>

We sorted an object array by a key in the previous question. What if the score is tie and want to sort it by the second key, name.

input
```javascript
const input = [{ name: "John", score: "432"},
 { name: "Joe", score: "125"},
 { name: "Zoe", score: "320"},
 { name: "Ziggy", score: "532"},
 { name: "Dave", score: "211"},
 { name: "Sarah", score: "621"},
 { name: "Alex", score: "320"}];
```

output - see when the sore is the same, it's sorted by name.
```javascript
0: {name: "Sarah", score: "621"}
1: {name: "Ziggy", score: "532"}
2: {name: "John", score: "432"}
3: {name: "Alex", score: "320"}
4: {name: "Zoe", score: "320"}
5: {name: "Dave", score: "211"}
6: {name: "Joe", score: "125"}
```

<details><summary><b>Answer</b></summary>

Apply the same method for the previous question. When the first key is the same, we can add another logic to sort it by the second key. Reference <a target="_blank" href="https://www.mydatahack.com/sorting-json-by-multiple-keys-with-javascript/">here</a>

```javascript
function rankingSorter(firstKey, secondKey) {
  return function(a, b) {  
    if (a[firstKey] > b[firstKey]) {  
      return -1;  
    } else if (a[firstKey] < b[firstKey]) {  
      return 1;  
    }  
    else {
      if (a[secondKey] > b[secondKey]) {  
        return 1;  
      } else if (a[secondKey] < b[secondKey]) {  
        return -1;  
      } else {
        return 0;
      }
    } 
  }  
}

input.sort(rankingSorter('score', 'name'));
```
</details>

---
### (2) ARRAY
---

<b>1. Create an array with a sequence of number</b>

output
```javascript
[0, 1, 2, 3, 4]
```

<details><summary><b>Answer</b></summary>

We can use either spread operator or Array from() and key() for ES6✌

For a reference, knowing how to use the Set object is great. Interestingly, this is not supported by IE11. If you do Array.from(new Set([1, 2, 3])), you will get an empty array without an error. Use set polyfill for IE11 support.

```javascript
[ ...Array(5).keys() ]

Array.from(Array(5).keys())

Array.from(new Set([0, 1, 2, 3, 4]))
```

</details>

---
### (3) STRING FORMAT
---

<b>1. Currency Format</b>

input
```javascript
const amount = 2398622.26
```

output
```javascript
'$2,398,622.26'
```

<details><summary><b>Answer</b></summary>

By using toLocaleString(), we can format currency with one line🤯

```javascript
amount.toLocaleString("en-US", {
  style: "currency",
  currency: "USD"
});
```

There is a great blog post about natvively formatting JavaScript Numbers <a>here</a>. The image below is from that blog post.

<img alt="formatting-number-cheatsheet" src="./img/format-js-numbers-crop.png" width="900"/>

If you want to do this without native API, it gets really intense...

```javascript
const formatAmount = (amount) => {
  const splitAmount = amount.split('.')
  const dollar = splitAmount[0]
  const decimal = splitAmount[1]
  const index = dollar.length / 3
  const dollarArray = []
  for (let i = 1; i <= index + 1; i++) {
    const startIndex = dollar.length - (i * 2) - 1 - (i - 1)
    const finalStartIndex = startIndex < 0 ? 0 : startIndex
    dollarArray.push(dollar.substring(finalStartIndex, startIndex + 3))
  }
  return `$${dollarArray.reverse().join(',')}.${decimal}`
}
```
</details>

<b>2. Datetime formatting</b>

Formatting the datetime string below into a local time.

input

``` javascript
'2020-06-28T23:59:01Z'
```

output - this is the local time (AEST for me)

``` javascript
'29/06/2020 09:59:01 AM'
```

<details><summary><b>Answer</b></summary>

Let's give it a go by using <a target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat">Intl.DateTimeFormat.</a> This will give you '29/06/2020'.

``` javascript
new Intl.DateTimeFormat('en-AU').format(new Date('2020-06-28T23:59:01Z'));
```

Now, Intl.DateTimeFormat has options. Let's pass the options.

```javascript
const options = {
  year: 'numeric', month: 'numeric', day: 'numeric',
  hour: 'numeric', minute: 'numeric', second: 'numeric',
  hour12: true,
  timeZone: 'Australia/Sydney' 
};

const formatted = new Intl.DateTimeFormat('en-AU', options).format(new Date('2020-06-28T23:59:01Z'));
```

The above will give us the output of '29/06/2020, 9:59:01 am'. We need to format this.

```javascript
formatted.toUpperCase().split(', ').join(' ');
```

That's it🤙

If you want to do this without native API, it gets long🐢

``` typescript
formatUtcToLocal(timestamp: string): string {
  const localTime = new Date(timestamp)
  const year = localTime.getFullYear()
  const month = this.formatSingleDigit(localTime.getMonth() + 1)
  const day = this.formatSingleDigit(localTime.getDate())
  const hour = this.formatSingleDigit(this.convertHour(localTime.getHours()))
  const minutes = this.formatSingleDigit(localTime.getMinutes())
  const seconds = this.formatSingleDigit(localTime.getSeconds())
  const amOrPm = localTime.getHours() > 12 ? 'PM' : 'AM'

  return `${day}/${month}/${year} ${hour}:${minutes}:${seconds} ${amOrPm}`
}

formatSingleDigit(value: number): string {
  const formattedMonth = `0${value}`
  return formattedMonth.substring(formattedMonth.length - 2, formattedMonth.length)
}

convertHour(hour: number): number {
  if (hour > 12) {
      return hour - 12
  }
  return hour
}
```
</details>

---
### (4) SPREAD SYNTAX
---

Spread syntax is cool. Use spread syntax for all the questions. Let's build spread syntax muscle memory!

<b>1. Spread with arrays</b>

input
```javascript
const fruits = ['apple', 'banana', 'blueberry'];
const vegs = ['lettus', 'tomato']
```

Without spread, we would use concat to combine two arrays. Use spread syntax to concat two arrays.

output
```javascript
['apple', 'banana', 'blueberry', 'lettus', 'tomato']
```

<details><summary><b>Answer</b></summary>

```javascript
const combined = [ ...fruits, ...vegs ];

// it is the same as
const combined = fruits.concat(vegs);
```
</details>

<b>2. Add object to an array</b>

Create a new object with a new fruit added and preserve original fruits array the same.

input
```javascript
const fruits = [{ id: 1, item: 'apple' }, { id: 2, item: 'orange' }];
const newFruit = { id: 3, item: 'banana' };
```

output
```javascript
// Create a new object called newFruits
[{ id: 1, item: 'apple' }, { id: 2, item: 'orange' }, { id: 3, item: 'banana' }]
```

<details><summary><b>Answer</b></summary>

```javascript
const newFruits = [ ...fruits, newFruit];
```

If you use Array.push() as below, it will modify the original array fruits. With spreading, we can preserve the original array.

```javascript
fruits.push(newFruit);
```
</details>

<b>3. Create an array from a set</b>

We can use spread syntax to create an iterable array from a set.

input
```javascript
const fruitSet = new Set();
set.add('apple');
set.add('orange');
set.add('banana');
```

output - create a new array called fruitArray
```javascript
['apple', 'orange', 'banana']
```

<b>4. Create an array from a string</b>

We can also use spread to create an array from a string.

input
```javascript
const str = 'spread';
```

output
```javascript
['s', 'p', 'e', 'a', 'd']
```

<details><summary><b>Answer</b></summary>

```javascript
const strArray = [ ...str ];
```
</details>

<b>5. Copying an object</b>

We can spread an object to copy and update. It is the equivalent of Object.assign().

input
```javascript
const original = { id: 1, fruit: 'apple' }
```

output - create an copy of the original, copied.

<details><summary><b>Answer</b></summary>

```javascript
const copied = { ...original };
```

This is the equivalent of
```javascript
const copied = Object.assign({}, original);
```
</details>

<b>6. Adding a new property on an exisitng object</b>

Add a new property to an exisitng object in an immutable fashion.

input
```javascript
const fruit = { id: 1, name: 'apple' }
```

output
```javascript
{ id: 1, name: 'apple', sweet: true }
```

<details><summary><b>Answer</b></summary>

```javascript
const updatedFruit = { ...fruit, sweet: true }
```

We can do the spread if the added proerty is an object as below.

```javascript
const add = { sweet: true }
const updatedFruit = { ...fruit, ...add }
// Then this will create the object with a new property
{ id: 1, name: 'apple', sweet: true }
```
</details>

<b>7. Updating a property on an exisitng object</b>

Update an existing property to create a new object in an immutable fashion.

input
```javascript
const fruit = { id: 1, name: 'apple' }
```

output
```javascript
{ id: 1, name: 'banana' }
```

<details><summary><b>Answer</b></summary>

```javascript
const updatedFruit = { ...fruit, name: 'banana' }
```

We can update the property of the object from an object with spread, too!

```javascript
const update = { name: 'banana' }
const updatedFruit = { ...fruit, ...update }
// this will update the property
{ id: 1, name: 'banana' }
```
</details>

<b>8. Spread with nested object</b>

Spread with nested object gets hairy. See if you can add a new property to the nested object as below.

input
```javascript
const fruit = { 
  id: 1, 
  item: {
    name: 'apple',
    sweet: true 
  }
}
```

output - add an price property to item
```javascript
{ 
  id: 1, 
  item: {
    name: 'apple',
    sweet: true,
    price: 1.0
  }
}
```

<details><summary><b>Answer</b></summary>

Nested objects need to be spread. In another word, we can spread the inner object, item, to retain the existing property.

```javascript
const newFruit = { ...fruit, item: { ...fruit.item, price: 1.0 } }
```

</details>

<b>9. Spread function call</b>

Spread can be used in a function call. We have a function called addAll. This will take 3 parameters. If we have an array of 3 numbers, how can we use the function?

```javascript
const addAll = (a, b, c) => a + b + c;

// use addAll function on the array below
const input = [1, 2, 3]
```

<details><summary><b>Answer</b></summary>

This is a cool use case. We can in fact pass the spread input.

```javascript
addAll(...input);
```

This is the same as using apply(). But, spread makes it shorter.

```javascript
addAll.apply(null, input)
```
</details>
<br />

---

### REFERNCES
---

There is a greate JavaScript questions to get to know the language better. Your JavaScript knowledge will skyrocket🚀 Check out <a target="_blank" href="https://github.com/lydiahallie/javascript-questions">javascript-questions</a>

I subscribe to <a target="_blank" href="https://javascriptweekly.com/">JavaScript Weekly.</a> It's a weekly email informing you on what is happening on JS landscape as well as useful JS tips! Highly recommended.

There are many code challenges websites. My recommendation is <a target="_blank" href="https://edabit.com/challenges">edatbit.com</a>. If you are comforatble with JavaScript, go to the expert level. These intereting bite-size challenges will be a holiday for your mind🌴

You can get to build framework and library free JS apps from <a target="_blank" href="https://javascript30.com/">JavaScript30.com</a>. It's free.

I am copy and pasting emoji from <a target="_blank" href="https://unicode.org/emoji/charts/full-emoji-list.html">this website</a>🥰