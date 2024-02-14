# Lab Report 3 :)

## Part 1 Bugs 😑
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

## Part 2 - Researching Commands 😁
### My chosen command will be ```find```
#### Four Interesting Command Line Options for ```find```
1. ```find . -iname```

    This is similar to that of ```find -name``` but now it is case insensitive which would be extremely useful if you don't remember the exact naming of a certain file/directory/etc. The "."        makes the computer look in the current working directory which is ```technical/```

    Ex. 1
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -iname "GOVERNMENT"
   ./government
   ```

   Ex. 2
   
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -iname "BIOmeD"
   ./biomed
   ```
2. ```find . -atime -n``` (With "n" being some number, could be "+" or "-" as well)

   This allows us to find files that have been access less n days ago. This would be helpful in situations where we do not remember what files we were using it would show what files we
   have recently accessed and give us an idea of what possible files they were.

   Ex. 1 (There was more than what was included in the code block but I cut it down just to not make this too long 😬)
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -atime -1
   ./government/About_LSC/Progress_report.tx
   ./government/About_LSC/Strategic_report.txt
   ./government/About_LSC/Special_report_to_congress.tx
   ./government/About_LSC/commission_report.tx
   ./government/About_LSC/ONTARIO_LEGAL_AID_SERIES.tx
   ./government/About_LSC/State_Planning_Report.tx
   ./government/Env_Prot_Agen/multi102902.txt
   ```

   Ex. 2
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -atime +1
   .
   ./government
   ./government/About_LSC
   ./government/About_LSC/LegalServCorp_v_VelazquezSyllabus.txt
   ./government/About_LSC/Comments_on_semiannual.txt
   ./government/About_LSC/CONFIG_STANDARDS.txt
   ./government/About_LSC/LegalServCorp_v_VelazquezDissent.txt
   ./government/About_LSC/LegalServCorp_v_VelazquezOpinion.txt
   ./government/About_LSC/diversity_priorities.txt
   ./government/About_LSC/reporting_system.txt
   ./government/About_LSC/Protocol_Regarding_Access.txt
   ```
   
3. ```find . -type [f|d]```

   This command line option proves useful if you are only looking to work with files or directories. 
   Ex. 1
      ```
      (base) josesandoval@Joses-MacBook-Pro technical % find . -type f
      ./plos/journal.pbio.0030021.txt
      ./plos/journal.pbio.0020224.txt
      ./plos/pmed.0020048.txt
      ./plos/pmed.0020060.txt
      ./plos/pmed.0020074.txt
      ./plos/journal.pbio.0020146.txt
      ./plos/pmed.0020114.txt
      ./plos/pmed.0010028.txt
      ```
      Ex. 2
      ```
      (base) josesandoval@Joses-MacBook-Pro technical % find . -type d
      .
      ./government
      ./government/About_LSC
      ./government/Env_Prot_Agen
      ./government/Alcohol_Problems
      ./government/Gen_Account_Office
      ./government/Post_Rate_Comm
      ./government/Media
      ./plos
      ./biomed
      ./911report
      ```

4. ```find . -maxdepth n -name '<filename>'```

   This gives the arguments limitations into how far(much depth) it should look for the specific file. This would prove useful in cases where you don't want to look throughout your whole computer but
   rather a smaller section of it.

   Ex. 1
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -maxdepth 2 -name About_LSC
   ./government/About_LSC
   ```
   Ex. 2
   ```
   (base) josesandoval@Joses-MacBook-Pro technical % find . -maxdepth 2 -name chapter-11.txt
   ./911report/chapter-11.txt
   ```
> For all my command line options I used the same source\
> I found out about this source by simply searching up “find command-line options” on [google.com](https://www.google.com/)\
> Citation: [https://www.computerhope.com/unix/ufind.htm](https://www.computerhope.com/unix/ufind.htm)


