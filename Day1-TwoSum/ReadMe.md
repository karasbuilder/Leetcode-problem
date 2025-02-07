# Two Sum Problem

## Problem Statement
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

### Constraints:
- Each input has **exactly one** valid solution.
- The same element **cannot** be used twice.
- The answer can be returned in **any order**.

## Examples

| Example | Input | Output | Explanation |
|---------|-------|--------|-------------|
| 1 | `nums = [2,7,11,15], target = 9` | `[0,1]` | `nums[0] + nums[1] = 2 + 7 = 9`, so return `[0,1]`. |
| 2 | `nums = [3,2,4], target = 6` | `[1,2]` | |
| 3 | `nums = [3,3], target = 6` | `[0,1]` | |

## Constraints
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- **Only one valid solution exists.**

## Optimal Solution
### Time Complexity: **O(n)**
A more efficient solution than **O(n²)** is possible using a **hash map**:

## Follow-Up
Can you come up with an algorithm that runs in **less than O(n²) time complexity**?
- The hash map approach above achieves **O(n)** time complexity, which is optimal for this problem.

## Solution:
### Solution 1: Brute Force
- Loop through the array and check for each pair of elements if their sum is equal to the target.
- If found, return the indices of the two elements.
- Time Complexity: **O(n²)**
```typescript
function twoSum(nums: number[], target: number): number[] {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    return [];
}
``` 
### Solution 2: Hash Map or Record
- Create a hash map to store the indices of the elements.
- Loop through the array and check if the difference between the target and the current element is present in the hash map.
- If found, return the indices of the two elements.
- Time Complexity: **O(n)**
```typescript
function twoSum(nums: number[], target: number): number[] {
    const map = new Map<number, number>();
    for (let i = 0; i < nums.length; i++) {
        const diff = target - nums[i];
        if (map.has(diff)) {
            return [map.get(diff), i];
        }
        map.set(nums[i], i);
    }
    return [];  
}
```
=> Note: We can use Record instead map in typescript
```typescript
function twoSum(nums: number[], target: number): number[] {
    const map: Record<number, number> = {};
    for (let i = 0; i < nums.length; i++) {
        const diff = target - nums[i];
        if (map[diff] !== undefined) {
            return [map[diff], i];
        }
        map[nums[i]] = i;
    }
    return [];  
}
```
- Record faster than Map in typescript some cases.

### Why is Record<number, number> (Object) Faster Than Map?
- JavaScript **engine optimizes objects** for quick property access.
- **Lower Overhead:** 
    - A `Map` stores keys and values separately, requiring extra memory and an internal hashing mechanism.
    - An object (`Record<number, number>`) directly maps numeric keys to values, reducing overhead.

### When to Use Record<number, number> Over Map<number, number>?

| Use Case | Use Record<number, number> (Object) | Use Map<number, number> |
|----------|-------------------------------------|-------------------------|
| Small, simple key-value lookups | ✅ Yes | ❌ No (unnecessary overhead) |
| Key is always a string or number | ✅ Yes | ❌ No (Objects only support string/number keys) |
| Dynamic keys (not known in advance) | ✅ Yes | ✅ Yes |
| Need advanced features (like iteration order, complex data types) | ❌ No | ✅ Yes |
| Keys need to be objects (not just numbers/strings) | ❌ No | ✅ Yes |
