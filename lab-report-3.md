# Lab Report 3

## Part 1 - Bugs

### 1. Failure-inducing input
```
@Test 
public void testReverseInPlace() {
  int[] input = {1, 2, 3, 4, 5};
  ArrayExamples.reverseInPlace(input);
  assertArrayEquals(new int[]{5, 4, 3, 2, 1}, input);
}
```

### 2. Non-failure-inducing input
```
@Test 
public void testReverseInPlace() {
  int[] input = {1};
  ArrayExamples.reverseInPlace(input);
  assertArrayEquals(new int[]{1}, input);
}
```

### 3. symptom
Output when running failure-inducing input:

<img src="lab-report-3-images/failure.png" alt="drawing" width="800">

Output when running non-failure-inducing input:

<img src="lab-report-3-images/no_failure.png" alt="drawing" width="400">

### 4. bug
Before:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < (arr.length/2); i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

The original bug was that, after successfully reversing the array, the code kept swapping the second half of the array with the first half of the array, which resulted in a symmetric array instead of correctly reversing the original array. The fix I did was stopping the swapping after getting through half of the array since the entire array would have already been successfully reversed.

## Part 2 - Researching Commands

