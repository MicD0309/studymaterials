# Binary Search Optimization & Edge Cases

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

## The Standard Template

```typescript
function binarySearch(nums: number[], target: number): number {
    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {
        // Prevent potential overflow
        const mid = Math.floor(left + (right - left) / 2);

        if (nums[mid] === target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
```

## Search Space Minimization Template
Sometimes, you aren't searching for an exact number, but rather the *first* or *last* element satisfying a condition.

### 1. Find First Occurrence (Lower Bound)
```typescript
function findFirst(nums: number[], target: number): number {
    let left = 0;
    let right = nums.length; // Notice right is nums.length

    while (left < right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (nums[mid] >= target) {
            right = mid; // Search left half
        } else {
            left = mid + 1; // Search right half
        }
    }
    return left;
}
```

### 2. Find Last Occurrence (Upper Bound)
```typescript
function findLast(nums: number[], target: number): number {
    let left = 0;
    let right = nums.length;

    while (left < right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (nums[mid] > target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left - 1;
}
```

## Complexity
- **Time Complexity:** $O(\log n)$
- **Space Complexity:** $O(1)$
