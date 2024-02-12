# Lab Report 3 :)

## Part 1 Bugs :/
### My chosen bug will be  ```reverseInPlace```


1. A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)

JUnit Test: 
```
@Test
  public void testReverseWithMoreNumbers(){
    int[] input1={1,2,3,4};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{4,3,2,1}, input1);
  }
```
   
2. An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
JUnit Test: 
```
@Test
  public void testReverseWithMoreNumbers(){
    int[] input1={0};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{0}, input1);
  }
```
   
3. The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)

Symptom of #1:
```
JUnit version 4.13.2
..E....E
Time: 0.004
There were 2 failures:
1) testReverseWithMoreNumbers(ArrayTests)
arrays first differed at element [2]; expected:<2> but was:<3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseWithMoreNumbers(ArrayTests.java:16)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<2> but was:<3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more
```

Symptom of #2:
```
JUnit version 4.13.2
.....
Time: 0.003

OK (5 tests)

```   
4. The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
   
Below is the code without any changes. 
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
After my debugging the code came out to this: 
```
static void reverseInPlace(int[] arr) {
    int[] temparr = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      temparr[i] = arr[arr.length - i - 1];
    }
    
    for(int j =0; j<arr.length;j++){
      arr[j]=temparr[j];
    }
  }
```
FIX: The before implementation of ```reverseInPlace``` reversed up until the halfway point. From then on it would copy elements that
were already changed. My implementation makes use of a temporary array to ensure the reversal of every element. Then another for loop
is used to copy the elements to the original array. 

## Part 2 - Researching Commands (boo)
### My chosen command will be ```find```


