# Part 1
The bug I chose is in the method `ReverseInPlace`
1. A failure-inducing input
   ```
   @Test 
	public void testReverseInPlace3() {
    int[] input1 = {1,2,3,4,5};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{5,4,3,2,1}, input1);
   }
   ```
2. An input that doesn't induce a failure
   ```
   @Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
   }
   ```
3. The symptom of the two tests above
   ![Image](Lab3-part1a.png)
   ![Image](Lab3-part1b.png)
4. Code before and after:
   Code before:
   ```
   static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
   }
   ```
   Code after:
   ```
   static void reverseInPlace(int[] arr) {
    int[] newArray1 = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray1[i] = arr[i];
    }
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray1[newArray1.length - i - 1];
    }
   } 
   ```
5. The issue with the old code is that the copy process changes the `arr` itself when reversing it. In my new code, I first make a copy of `arr` and reverse it using its original elements.

# Part 2
## Command Less
1. The command line option `-N` displays line numbers at the beginning of each line
  * Example 1:
    ```
    Tonys-MBP:technical shenda$ less -N biomed/ar149.txt
    ... a bunch of lines ...
    459         macrophage inflammatory protein; OA = osteoarthritis; PBMC
    460         = peripheral blood mononuclear cells; PE = phycoerythrin;RA
    461         = rheumatoid arthritis; RANTES = regulated upon activation,
    462         normal T cell expressed and secreted; RT-PCR = reverse
    463         transcriptase-polymerasechain reaction; SCL = stromal cell
    464         line; SRBC = sheep red blood cells; TNF-α = tumor necrosis
    465         factor-α.
    466
    467
    468
    ```
  * Example 2:
    ```
    Tonys-MBP: technical shenda$ less -N 911report/preface.txt
    ... a bunch of lines ...
    97                 for the American people. We recognize the formidable challenges that lie ahead.
    98             We also approach the task of recommendations with humility. We have made a limited
    99                 number of them. We decided consciously to focus on recommendations we believe to be
    100                 most important, whose implementation can make the greatest difference. We came into
    101                 this process with strong opinions about what would work. All of us have had to
    102                 pause, reflect, and sometimes change our minds as we studied these problems and
    103                 considered the views of others. We hope our report will encourage our fellow
    104                 citizens to study, reflect-and act.
    105             Thomas H. Kean, chair
    106             Lee H. Hamilton, vice chair
    107         
    108
    ```

    The prompt I gave to ChatGPT was "command-line options for command less."
    It outputted "-N or --LINE-NUMBERS: Displays line numbers at the beginning of each line."
    
2. The command line `-S` chops long lines that do not fit in the screen.
   * Example 1:
     ```
     Tonys-MBP: technical shenda$ less -S 911report/chapter-1.txt
     ... a bunch of lines ...
     	Second, NEADS did not have accurate information on the location of United 93. Presumably FAA would have provided such information>

    	Third, NEADS needed orders to pass to the pilots. At 10:10, the pilots over Washington were emphatically told, "negative clearan>

    	NORAD officials have maintained that they would have intercepted and shot down United 93. We are not so sure. We are sure that t>

    	The details of what happened on the morning of September 11 are complex, but they play out a simple theme. NORAD and the FAA were>

    	At 10:02 that morning, an assistant to the mission crew commander at NORAD's Northeast Air Defense Sector in Rome, New York, was>

    	He was, and is, right. But the conflict did not begin on 9/11. It had been publicly declared years earlier, most notably in a de>
     ```
   * Example 2:
     ```
     Tonys-MBP: technical shenda$ less -S 911report/chapter-6.txt
     ... a bunch of lines ...
     Funding still needed to be located. The military component remained unclear. Pakistan
                remained uncooperative. The domestic policy institutions were largely uninvolved.
                But the pieces were coming together for an integrated policy dealing with al Qaeda,
                the Taliban, and Pakistan.
     ```

   The prompt I gave to ChatGPT was "command-line options for command less."
   It outputted "-S or --chop-long-lines: Causes long lines to be chopped (truncated) rather than wrapped. That is, the portion of a long line that does not fit in the screen width 
   will not be shown."

3. The command line `-V` displays version information for `less`
   * Example 1:
     ```
     Tonys-MBP:technical shenda$ less -V biomed/ar149.txt
     less 581.2 (POSIX regular expressions)
     Copyright (C) 1984-2021  Mark Nudelman
     less comes with NO WARRANTY, to the extent permitted by law.
     For information about the terms of redistribution,
     see the file named README in the less distribution.
     Home page: https://greenwoodsoftware.com/less
     ```
   * Example 2:
     ```
     Tonys-MBP:technical shenda$ less -V 911report/preface.txt
     less 581.2 (POSIX regular expressions)
     Copyright (C) 1984-2021  Mark Nudelman
     less comes with NO WARRANTY, to the extent permitted by law.
     For information about the terms of redistribution,
     see the file named README in the less distribution.
     Home page: https://greenwoodsoftware.com/less
     ```

   The prompt I gave to ChatGPT was "command-line options for command less."
   It outputted "-V or --version: Displays version information for less."

4. The command line `-s` squeezes multiple adjacent blank lines into a single blank line.
   * Example 1:
     ```
     Tonys-MBP:technical shenda$ less -s biomed/ar149.txt
     ... a bunch of lines ...
             normal T cell expressed and secreted; RT-PCR = reverse
        transcriptase-polymerasechain reaction; SCL = stromal cell
        line; SRBC = sheep red blood cells; TNF-α = tumor necrosis
        factor-α.
     ```
     * Example 2:
       ```
       Tonys-MBP:technical shenda$ less -s 911report/preface.txt
       ... a bunch of lines ...
           We also approach the task of recommendations with humility. We have made a limited
                number of them. We decided consciously to focus on recommendations we believe to be
                most important, whose implementation can make the greatest difference. We came into
                this process with strong opinions about what would work. All of us have had to
                pause, reflect, and sometimes change our minds as we studied these problems and
                considered the views of others. We hope our report will encourage our fellow
                citizens to study, reflect-and act.
            Thomas H. Kean, chair
            Lee H. Hamilton, vice chair
       ```
       The prompt I gave to ChatGPT was "command-line options for command less."
       It outputted "-s or --squeeze-blank-lines: Squeezes multiple adjacent blank lines into a single blank line. This can make viewing files with large gaps more pleasant."
     
     
    
  
