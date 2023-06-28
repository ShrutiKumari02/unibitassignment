#  Unibit-Assignment

## Question
Given an array of integers and a target value, you must determine which two integers' sum
equals the target and return a 2D array. Then merge the array into a single array with sorting (
ascending ) order, in the next step double the target value and find again the combination of
digits (can be multiple digits ) that are equal to the double targeted value and returned into a 2D
array.
Sample Input : [1, 3, 2, 2, -4, -6, -2, 8];
Target Value = 4,
Output: First Combination For “4” : [ [1,3],[2,2],[-4,8],[-6,2] ];
Merge Into a single Array : [-6,-4,1,2,2,2,3,8];
Second Combination For “8” : [ [ 1,3,2,2], [8,-4,2,2],....,[n,n,n,n] ]
<br/>
<br/>
## Answer
```
function findTwoSum(nums, target) {
    const map = new Map();
    const result = [];
  
    for (let num of nums) {
      let complement = target - num;
      if (map.has(complement)) {
        let complementList = map.get(complement);
        for (let pair of complementList) {
          result.push([...pair, num]);
        }
      }
  
      if (!map.has(num)) {
        map.set(num, []);
      }
      for (let pair of map.get(num)) {
        result.push([...pair, num]);
      }
      map.get(num).push([num]);
    }
  
    return result;
  }
  
  function mergeArrays(arrays) {
    const mergedArray = arrays.flat().sort((a, b) => a - b);
    return mergedArray;
  }
  
  function findCombination(nums, target) {
    const result = [];
    findCombinationHelper(nums, target, [], result, 0);
    return result;
  }
  
  function findCombinationHelper(nums, target, current, result, start) {
    if (target === 0) {
      result.push([...current]);
      return;
    }
  
    if (target < 0) {
      return;
    }
  
    for (let i = start; i < nums.length; i++) {
      if (i > start && nums[i] === nums[i - 1]) {
        continue;
      }
      current.push(nums[i]);
      findCombinationHelper(nums, target - nums[i], current, result, i + 1);
      current.pop();
    }
  }
  
  function convertTo2DArray(list) {
    const array = new Array(list.length);
    for (let i = 0; i < list.length; i++) {
      const sublist = list[i];
      array[i] = new Array(sublist.length);
      for (let j = 0; j < sublist.length; j++) {
        array[i][j] = sublist[j];
      }
    }
    return array;
  }
  
  function printTwoDArray(arr) {
    for (let row of arr) {
      console.log(row);
    }
  }
  
  function printArray(arr) {
    console.log(arr);
  }
  
  const nums = [1, 3, 2, 2, -4, -6, -2, 8];
  const target = 4;
  
  const firstCombination = findTwoSum(nums, target);
  console.log(`First Combination For "${target}": `);
  printTwoDArray(firstCombination);
  
  const mergedArray = mergeArrays(firstCombination);
  console.log("Merge Into a single Array: ");
  printArray(mergedArray);
  
  const secondCombination = findCombination(mergedArray, target * 2);
  console.log(`Second Combination For "${target * 2}": `);
  printTwoDArray(secondCombination);
  
```
## Output 💻
![Screenshot (331)](https://github.com/ajaykumar2pp/Unibit-Assignment/assets/102378038/3f7a3a89-825c-458b-a300-4ab726805b82)

> ##  Time Complexity of the code  : O(2^n)
