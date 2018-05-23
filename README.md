# fast-sort

[![Build Status](https://travis-ci.org/snovakovic/js-flock.svg?branch=master)](https://travis-ci.org/snovakovic/js-flock)
[![Code quality](https://api.codacy.com/project/badge/grade/fe5f8741eaed4c628bca3761c32c3b68)](https://www.codacy.com/app/snovakovic/js-flock/dashboard?bid=4653162)
[![Codacy Badge](https://api.codacy.com/project/badge/Coverage/f0ea30fd63bd4bc88ea3b0965094ced1)](https://www.codacy.com/app/snovakovic/js-flock?utm_source=github.com&utm_medium=referral&utm_content=snovakovic/js-flock&utm_campaign=Badge_Coverage)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://opensource.org/)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)

[![NPM Package](https://nodei.co/npm/fast-sort.png)](https://www.npmjs.com/package/fast-sort)


Blazing fast array sorting that **outperforms lodash sorting by ~2x** (in some cases it's more then 5x).
Take a look at the benchmark section for more information about performance.

fast-sort is part of [js-flock](https://www.npmjs.com/package/js-flock) library exported as single module. Please reference [js-flock](https://github.com/snovakovic/js-flock) github repository for source code, issue opening, contributing or giving a star ;)


Under the hood sort use a [native JavaScript sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort).
Usage of native sort implies that sorting is not necessarily [stable](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability) and it also implies that input array is modified(sorted) same as it would be when applying native sort.


### Fast sort higlights

* Sorting an array of objects by one or more properties
* Sorting flat arrays
* Easy to read syntax for asc and desc sorting
* Faster then other sort alternatives
* Undefined and null values are always sorted to bottom of list no matter if ordering is ascending or descending.


### Example

```javascript
  import sort from 'fast-sort';

  sort([1,4,2]).asc(); // sort array in ascending order [1, 2, 4]
  sort([1,4,2]).desc(); // sort array in descending order [4, 2, 1]

  // Sort persons [Object] ascending by lowercase firstName
  sort(persons).asc((p) => p.firstName.toLowerCase());

  // Sort persons by multiple properties
  sort(persons).desc([
    (p) => p.firstName, // Sort by first name
    (p) => p.lastName, // Persons that have same firstName will be sorted by lastName
    (p) => p.dob // Persons that have same firstName and lastName will be sorted by dob
  ]);

  // Sorting values that are not sortable will return same value back
  sort(null).asc(); // => null
  sort(33).desc(); // => 33
```

### Benchmark

Benchmarking sort is not an easy task as there is so many different scenarios that can happen while sorting.
Because of that 5 different benchmarks have been created to test how fast-sort is behaving on different inputs and sort scenarios.
Each benchmark is run with different array sizes from small 100 items to large 100 000 items.

Every run of benchmark outputs different results but the results are constantly better then lodash sort and in following benchmark score ranges from 1.37x to 13.51x faster then lodash sort. This will vary on each benchmark run but it should not vary too much.


#### Benchmark scores

Benchmark has been run on:

* 16 GB Ram
* Intel® Core™ i5-4570 CPU @ 3.20GHz × 4
* Ubuntu 16.04
* Node 8.9.1

![benchmark results](https://github.com/snovakovic/fast-sort/raw/master/benchmark.jpg)


#### Running benchmark

To run benchmark on your PC follow steps from below

1) git clone https://github.com/snovakovic/js-flock.git
2) cd js-flock
3) npm install
4) npm run benchmark:sort

In case you notice any irregularities in benchmark or you want to add sort library to benchmark score
please open issue [here](https://github.com/snovakovic/js-flock/issues)
