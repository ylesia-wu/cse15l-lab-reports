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
Similarly, the `-i` option allows us to find all lines in `chapter-10.txt` that contain "freedom" in any form of capitalization. We can see that we found lines that contain either "freedom" or "Freedom".

*Source: https://man7.org/linux/man-pages/man1/grep.1.html

#### Option 2: `-L` (files-without-match)

Suppress normal output; instead print the name of each input file from which no output would normally have been printed.

Example 1:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -L "women" technical/911report/*.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-5.txt
technical/911report/chapter-7.txt
technical/911report/chapter-8.txt
technical/911report/chapter-9.txt
```
Comparing to the output that we observed above, the `-L` option gives us exactly the files that do not contain "women". It is to be noted that, since we are not giving the `-i` option anymore, the search is now case-sensitive. 

Example 2:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -L "freedom" technical/911report/*.txt
technical/911report/chapter-1.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-3.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-8.txt
technical/911report/chapter-9.txt
technical/911report/preface.txt
```
Similarly, the `-L` option gives us all files that do not contain "freedom".

*Source: https://man7.org/linux/man-pages/man1/grep.1.html

#### Option 3: `-l` (files-with-matches)

Suppress normal output; instead print the name of each input file from which output would normally have been printed.  Scanning each input file stops upon first match.

Example 1:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -l "women" technical/911report/*.txt 
technical/911report/chapter-1.txt
technical/911report/chapter-12.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-2.txt
technical/911report/chapter-3.txt
technical/911report/chapter-6.txt
technical/911report/preface.txt
```
The `-l` option gives us all files that contain "women". We can compare this output with the output from the `-i` example and be sure that the output indeed correctly includes all such files.

Example 2:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -l "freedom" technical/911report/*.txt
technical/911report/chapter-12.txt
technical/911report/chapter-2.txt
```
Comparing with the output from the example for the `-L` option, we can confirm that these two files are the only two files that contain "freedom".

*Source: https://man7.org/linux/man-pages/man1/grep.1.html

#### Option 4: `-w` (word-regexp)

Select only those lines containing matches that form whole words.  The test is that the matching substring must either be at the beginning of the line, or preceded by a non-word constituent character.  Similarly, it must be either at the end of the line or followed by a non-word constituent character.  Word-constituent characters are letters, digits, and the underscore.  This option has no effect if -x is also specified.

Example 1:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -w "Free" technical/911report/*.txt
technical/911report/chapter-12.txt:            The U.S. government has announced the goal of working toward a Middle East Free Trade
technical/911report/chapter-13.3.txt:                2002-30037H, May 15, 2002; Steven Emerson, American Jihad (Free Press, 2002), pp.
technical/911report/chapter-13.3.txt:                Terror (Free Press, 2004), p. 234. On the CSG and the Small Group, see Samuel Berger
technical/911report/chapter-13.4.txt:                Bernstein, "Germans Free Moroccan Convicted of a 9/11 Role," New York Times, Apr. 8,
technical/911report/chapter-13.4.txt:            149. Richard Clarke, Against All Enemies: Inside America's War on Terror (Free Press,
technical/911report/chapter-13.5.txt:                Supreme Court has not yet decided to resolve this "circuit split." See Detroit Free
technical/911report/chapter-13.5.txt:            60. Richard A. Clarke, Against All Enemies: Inside America's War on Terror (Free
technical/911report/chapter-13.5.txt:                But World Embraces Democratic Values and Free Markets," June 3, 2003 (online at
```
By observing the output carefully, we can notice that this search with the `-w` option only gives us files that contain exactly the word "Free", in the correct form of capitalization. It does not give us any lines that contain "Freedom" instead of "Free" because, in this case, "Free" will not be a whole word but is, instead, a sub-part of another word.

Example 2:
```
ylesia@Ylesia-MacBook-Air docsearch % grep -w "men" technical/911report/*.txt
technical/911report/chapter-1.txt:    Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied themselves for work. Some made their way to the Twin Towers, the signature structures of the World Trade Center complex in New York City. Others went to Arlington, Virginia, to the Pentagon. Across the Potomac River, the United States Congress was back in session. At the other end of Pennsylvania Avenue, people began to line up for a White House tour. In Sarasota, Florida, President George W. Bush went for an early morning run.
technical/911report/chapter-1.txt:    While Atta had been selected by CAPPS in Portland, three members of his hijacking team-Suqami, Wail al Shehri, and Waleed al Shehri-were selected in Boston. Their selection affected only the handling of their checked bags, not their screening at the checkpoint. All five men cleared the checkpoint and made their way to the gate for American 11. Atta, Omari, and Suqami took their seats in business class (seats 8D, 8G, and 10B, respectively). The Shehri brothers had adjacent seats in row 2 (Wail in 2A, Waleed in 2B), in the firstclass cabin. They boarded American 11 between 7:31 and 7:40. The aircraft pushed back from the gate at 7:40.
technical/911report/chapter-1.txt:    Washington Dulles: American 77. Hundreds of miles southwest of Boston, at Dulles International Airport in the Virginia suburbs of Washington, D.C., five more men were preparing to take their early morning flight. At 7:15, a pair of them, Khalid al Mihdhar and Majed Moqed, checked in at the American Airlines ticket counter for Flight 77, bound for Los Angeles. Within the next 20 minutes, they would be followed by Hani Hanjour and two brothers, Nawaf al Hazmi and Salem al Hazmi.
technical/911report/chapter-1.txt:    The four men passed through the security checkpoint, owned by United Airlines and operated under contract by Argenbright Security. Like the checkpoints in Boston, it lacked closed-circuit television surveillance so there is no documentary evidence to indicate when the hijackers passed through the checkpoint, what alarms may have been triggered, or what security procedures were administered. The FAA interviewed the screeners later; none recalled anything unusual or suspicious.
technical/911report/chapter-1.txt:    The four men boarded the plane between 7:39 and 7:48. All four had seats in the first-class cabin; their plane had no business-class section. Jarrah was in seat 1B, closest to the cockpit; Nami was in 3C, Ghamdi in 3D, and Haznawi in 6B.
technical/911report/chapter-1.txt:    The 19 men were aboard four transcontinental flights.
technical/911report/chapter-11.txt:                if the men left the country. On January 14, the head of the CIA's al Qaeda unit
technical/911report/chapter-13.1.txt:            The men and women of the World War II generation rose to the challenges of the 1940s
technical/911report/chapter-13.2.txt:                men had the same last name and had assigned seats on row 9 (i.e., the Ghamdis), and
technical/911report/chapter-13.4.txt:                entranced during a prayer that both men began to cry. FBI report of investigation,
technical/911report/chapter-13.5.txt:                later, two men helped Hamlan cross the Pakistan- Afghanistan border.
technical/911report/chapter-13.5.txt:                that it was unable to connect the men's activities to terrorism. Matthew interview
technical/911report/chapter-13.5.txt:                problematic. The most likely means of successfully finding the men in the short time
technical/911report/chapter-13.5.txt:                disrupted the plot, even if the men had not been physically located before September
technical/911report/chapter-13.5.txt:                line of 20 men and the 4 survivors, see FDNY interview, transcript 13, Battalion 11,
technical/911report/chapter-2.txt:                attractive to educated young men, the countries became economically stagnant and
technical/911report/chapter-2.txt:                of young men without any reasonable expectation of suitable or steady employment-a
technical/911report/chapter-2.txt:                sure prescription for social turbulence. Many of these young men, such as the
technical/911report/chapter-2.txt:                humanities and social sciences. Many of these young men, even if able to study
technical/911report/chapter-2.txt:                families of their own, some of these young men were easy targets for radicalization.
technical/911report/chapter-2.txt:                men with no marketable skills but with deeply held Islamic views.
technical/911report/chapter-3.txt:                that the men in the dock were not the only plotters. Materials taken from Ajaj
technical/911report/chapter-3.txt:                not happen by accident. Recent wars have been waged and won decisively by brave men
technical/911report/chapter-3.txt:                professional men and women.
technical/911report/chapter-3.txt:                university gone to war. Its men and women tended to judge one another by the
technical/911report/chapter-3.txt:                cigars and Mafia hit men, Americans heard testimony about a secret visit to Tehran
technical/911report/chapter-5.txt:                Western-educated men who had recently arrived in Kandahar. Though they hailed from
technical/911report/chapter-5.txt:                two men became close friends and became identified with their shared extremist
technical/911report/chapter-5.txt:                group of men from various Arab countries studying in Germany who, while lacking
technical/911report/chapter-5.txt:                generalized suspicion that visa applicants from Yemen-especially young men applying
technical/911report/chapter-5.txt:                on a terrorist watchlist, and none of these four men was. Concerns that Binalshibh
technical/911report/chapter-6.txt:                components with a close friend. The chemicals were so caustic that the men kept
technical/911report/chapter-6.txt:            In Bangkok, CIA officers received the information too late to track the three men as
technical/911report/chapter-6.txt:            Early in chapter 5 we introduced, along with Khalid Sheikh Mohammed, two other men
technical/911report/chapter-6.txt:                It was also disseminated among many young men in Saudi Arabia and Yemen, and caused
technical/911report/chapter-6.txt:                Tajikistan border with two men whom the Northern Alliance leader had been told were
technical/911report/chapter-7.txt:                the two men had contact with each other. Similarly, Thumairy's claim not to know
technical/911report/chapter-7.txt:                know where Hanjour stayed; a few days later, both men left San Diego. Before
technical/911report/chapter-7.txt:                Majed Moqed. These two men had been sent to America to serve as muscle hijackers and
technical/911report/chapter-7.txt:                six men living there-Nawaf al Hazmi, now joined by his younger brother Salem,
technical/911report/chapter-7.txt:            Saudi authorities interviewed the relatives of these men and have briefed us on what
technical/911report/chapter-7.txt:                years before the attacks. Their families often did not consider these young men
technical/911report/chapter-7.txt:                obstacles. Now 19 men waited in nondescript hotel rooms to board four flights the
technical/911report/chapter-9.txt:                some of these men.
technical/911report/chapter-9.txt:                single file in a line of approximately 20 men. Four survived.
technical/911report/chapter-9.txt:                mall concourse, trying to reach the SouthTower. Many of these men were thrown off
technical/911report/chapter-9.txt:                mission in the Marriott, "I would never think of myself as a leader of men if I had
```
Similarly, we can observe that lines with only the word "women" but not "men" is not included in the output because the `-w` option is looking for lines that include the exact word "men".

*Source: https://man7.org/linux/man-pages/man1/grep.1.html
