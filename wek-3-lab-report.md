# CSE 15L Lab Report 3

## Part 1 - Bugs

The method I picked out was the bug in ArrayExamples.java, whihc was the *reverseInPlace* method.

![Image](lab-3-images/reverse1.png)

A failure inducing output for that method was when I tried to reverse numbers decreasing by one, which was when I tried:

```
int[] input2 = {9,8,7};
assertEquals(new int[] {7,8,9}, input2);
```

An input that doesn't have a failure is when there is on element in the array, such as:

```
int[] input1 = {3};
assertEquals(new int[] {3}, input1);
```

The problem in the method was really just how it accessed and tried to reverse the data, as it seemed to not change the data much at all:

![Image](lab-3-images/reverse2.png)

To fix this, I made a temporary array with the same data values, changed the values in there, and then made the original array the same as the temporary array

Before the method looked like this:

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

Now it looks like this:

```
static void reverseInPlace(int[] arr) {
    int[] temp = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      temp[i] = arr[i];
    }
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = temp[temp.length - 1 - i];
    }
  }
```
This fix adresses the issue because the array is now easlily able to get the reversed items into the correct order by copying over from the temp array rather than do it in its own array, which it can't when it is changing the values inide itself already

