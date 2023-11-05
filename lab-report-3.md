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

### 3. Symptom
Output when running failure-inducing input:

<img src="lab-report-3-images/failure.png" alt="drawing" width="800">

Output when running non-failure-inducing input:

<img src="lab-report-3-images/no_failure.png" alt="drawing" width="400">

### 4. Bug
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

### `grep`

#### Option 1: `-i` (ignore-case)

Ignore case distinctions in patterns and input data, so that characters that differ only in case match each other.

Example 1:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -i "Women" technical/911report/*.txt
technical/911report/chapter-1.txt:    Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied themselves for work. Some made their way to the Twin Towers, the signature structures of the World Trade Center complex in New York City. Others went to Arlington, Virginia, to the Pentagon. Across the Potomac River, the United States Congress was back in session. At the other end of Pennsylvania Avenue, people began to line up for a White House tour. In Sarasota, Florida, President George W. Bush went for an early morning run.
technical/911report/chapter-12.txt:                opportunities to women-these cures must come from within Muslim societies
technical/911report/chapter-12.txt:                greater freedom, women and girls are emerging from subjugation, and 3 million
technical/911report/chapter-12.txt:                embattled ally. They perceive an autocratic government that oppresses women,
technical/911report/chapter-12.txt:                activity and limit employment opportunities for young Saudis. Women find their
technical/911report/chapter-12.txt:                issues as the concept of jihad, the position of women, and the place of non-Muslim
technical/911report/chapter-12.txt:                illiterate, two-thirds of them women. One-third of the broader Middle East lives on
technical/911report/chapter-12.txt:                    the Middle East region's illiteracy rate in half by 2010, targeting women and
technical/911report/chapter-13.1.txt:            The men and women of the World War II generation rose to the challenges of the 1940s
technical/911report/chapter-13.5.txt:                young American women, Heather Mercer and Dayna Curry of the organization "Shelter
technical/911report/chapter-2.txt:                the West. Furthermore, the repression and isolation of women in many Muslim
technical/911report/chapter-3.txt:                and women using advanced technology that was developed, authorized, and paid for by
technical/911report/chapter-3.txt:                professional men and women.
technical/911report/chapter-3.txt:                university gone to war. Its men and women tended to judge one another by the
technical/911report/chapter-3.txt:                Taliban's record on women's rights.
technical/911report/chapter-6.txt:                vehicles, they quickly determined that women and children were inside and called off
technical/911report/preface.txt:                and equal rights for women. It makes no distinction between military and civilian
```
As we can see, the `-i` option ignores the case of the search. Without this command, the search would have only output the line from `technical/911report/chapter-12.txt:                activity and limit employment opportunities for young Saudis. Women find their` because it is the only line that contains "Women", with a capitalized "W". However, with this command added, we were able to find all lines that contain "Women" in any form of capitalization. 

Example 2:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -i "freedom" technical/911report/*.txt
technical/911report/chapter-10.txt:                    Freedom."
technical/911report/chapter-12.txt:                greater freedom, women and girls are emerging from subjugation, and 3 million
technical/911report/chapter-12.txt:                Muslims that we must encourage reform, freedom, democracy, and opportunity, even
technical/911report/chapter-12.txt:                The United Nations has rightly equated "literacy as freedom."
technical/911report/chapter-12.txt:                manifestation of our belief in freedom, democracy, global economic growth, and the
technical/911report/chapter-13.5.txt:                Protecting America's Freedom in the Information Age (Markle Foundation, 2002) (both
technical/911report/chapter-2.txt:                Sudanese, clearly thought that he had new freedom to publish his appeals for jihad.
technical/911report/chapter-2.txt:                in Afghanistan a freedom of movement that he had lacked in Sudan. Al Qaeda members
```
Similarly, the `-i` option allows us to find all lines that contain "freedom" in any form of capitalization. We can see that we found lines that contain either "freedom" or "Freedom".


#### Option 2: `-v` (invert-match)

Invert the sense of matching, to select non-matching lines.


#### Option 3: `-l` (files-with-matches)

Suppress normal output; instead print the name of each input file from which output would normally have been printed.  Scanning each input file stops upon first match.


#### Option 4: `-w` (word-regexp)

Select only those lines containing matches that form whole words.  The test is that the matching substring must either be at the beginning of the line, or preceded by a non-word constituent character.  Similarly, it must be either at the end of the line or followed by a non-word constituent character.  Word-constituent characters are letters, digits, and the underscore.  This option has no effect if -x is also specified.


