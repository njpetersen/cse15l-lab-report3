## eryfer ##

### step 1
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.ArrayList;
import java.util.List;

public class ListTests {

    @Test
    public void testMerge(){
        
        List<String> list1 = new ArrayList<>();
        list1.add("c");
        List<String> list2 = new ArrayList<>();
        list2.add("a");
        list2.add("b");
        list2.add("d");
        list2.add("e");

        List<String> listComparison = new ArrayList<>();
        listComparison.add("a");
        listComparison.add("b");
        listComparison.add("c");
        listComparison.add("d");
        listComparison.add("e");

        assertEquals(listComparison, ListExamples.merge(list1,list2));
    }
}
```
### step 2
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.ArrayList;
import java.util.List;

public class ListTests {

    //testMerge1 method not shown for clarity, it would be here

    @Test
    public void testMerge2(){
        
        List<String> list1 = new ArrayList<>();
        list1.add("a");
        list1.add("b");
        list1.add("d");
        list1.add("e");
        List<String> list2 = new ArrayList<>();
        list2.add("c");

        List<String> listComparison = new ArrayList<>();
        listComparison.add("a");
        listComparison.add("b");
        listComparison.add("c");
        listComparison.add("d");
        listComparison.add("e");

        assertEquals(listComparison, ListExamples.merge(list1,list2));
    }
}
```
### step 3
![OutputCode](output1.jpg)
### step 4
```
// Takes two sorted list of strings (so "a" appears before "b" and so on),
// and return a new list that has all the strings in both list in sorted order.
static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }
```
vs 
```
// Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1; //this line is changed from index1 to index2
    }
    return result;
  }
```
### Step 5
As indicated by the runtime error from step 3, the bug in this program had to do with infinitely executing code. This infinitely executing code occured in the third while loop, where the condition `index2 < list2.size()` runs infinitely unless index2 is incremented. The original code erroneously incremented index1 instead of index2, which not only causes the while loop to never be excited, but also makes no logical sense to increment (since the third while loop adds the elements of list2 not list1). Changing the code `index1 +=1` to `index2 +=1` solves this problem by allowing the while loop to be exited and also iterating through list2 instead of list1.

## Researching commands - less command ##
### less -N command
ex1:
The command `less -N 911report/chapter-1.txt` produces the output:  
```     
        1  
        2     
        3         
        4 "WE HAVE SOME PLANES"
        5 
        6     Tuesday, September 11, 2001, dawned temperate and nearly cloudless i
        6 n the eastern United States. Millions of men and women readied themselve
        6 s for work. Some made their way to the Twin Towers, the signature struct
        6 ures of the World Trade Center complex in New York City. Others went to
        6 Arlington, Virginia, to the Pentagon. Across the Potomac River, the Unit
        6 ed States Congress was back in session. At the other end of Pennsylvania
        6  Avenue, people began to line up for a White House tour. In Sarasota, Fl
        6 orida, President George W. Bush went for an early morning run.
        7 
        8     For those heading to an airport, weather conditions could not have b
        8 een better for a safe and pleasant journey. Among the travelers were Moh
        8 amed Atta and Abdul Aziz al Omari, who arrived at the airport in Portlan
        8 d, Maine.
        9         
        10 INSIDE THE FOUR FLIGHTS
        11 
        12 Boarding the Flights
        13 
:
```
ex2:
The command `less -N biomed/rr74.txt` produces the output:
```
      1 
      2   
      3     
      4       
      5         Introduction
      6         NO, which may be synthesized by any of the three
      7         isoforms of NOS, is a vasodilator of the pulmonary
      8         circulation in many mammals. NO has been proposed as a
      9         modulator of vascular tone and structure in the pulmonary
     10         circulation, and previous studies using NOS inhibitors [ 1,
     11         2] suggested that inhibition of NO increases acute hypoxic
     12         pulmonary vasoconstriction. Chronic NOS inhibition did not
     13         lead to development of pulmonary hypertension [ 3],
     14         however, possibly because of a decrease in cardiac output.
     15         These discrepancies have been addressed in recent studies
     16         using mice that are deficient in NOS isoforms.
     17         Three isoforms of NOS are found in the lung. The
     18         principle isoform that is found in the pulmonary
     19         vasculature is eNOS [ 4]. iNOS is expressed in airway
     20         epithelium, and airway and vascular smooth muscle [ 5, 6],
     21         whereas nNOS is expressed in the bronchial epithelium and
     22         lung nervous tissue [ 4, 5, 7, 8]. Thus, all three NOS
     23         isoforms could contribute to modulation of pulmonary
:
```

The command line option `-N` adds numbers to the left side of the output indicating what line from the original file each line outputted by the less command represents. This has the use of clearing up confusion as to where exactly a line starts or ends in the original file when looking at the output, and can also be used to determine the number of lines in a file.

### less -f
ex1: 
The command `less -f 911report` produces the output:
```
read error  (press RETURN)
```
pressing the return key changes the output to:
```
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
(END)
```

ex2:
The command `less -f biomed/rr74.txt` produces the output:
```
     
        Introduction
        NO, which may be synthesized by any of the three
        isoforms of NOS, is a vasodilator of the pulmonary
        circulation in many mammals. NO has been proposed as a
        modulator of vascular tone and structure in the pulmonary
        circulation, and previous studies using NOS inhibitors [ 1,
        2] suggested that inhibition of NO increases acute hypoxic
        pulmonary vasoconstriction. Chronic NOS inhibition did not
        lead to development of pulmonary hypertension [ 3],
        however, possibly because of a decrease in cardiac output.
        These discrepancies have been addressed in recent studies
        using mice that are deficient in NOS isoforms.
        Three isoforms of NOS are found in the lung. The
        principle isoform that is found in the pulmonary
        vasculature is eNOS [ 4]. iNOS is expressed in airway
        epithelium, and airway and vascular smooth muscle [ 5, 6],
        whereas nNOS is expressed in the bronchial epithelium and
        lung nervous tissue [ 4, 5, 7, 8]. Thus, all three NOS
        isoforms could contribute to modulation of pulmonary
:
```

### less -M
ex1:
The command `less -M biomed/rr74.txt`
```
      
        Introduction
        NO, which may be synthesized by any of the three
        isoforms of NOS, is a vasodilator of the pulmonary
        circulation in many mammals. NO has been proposed as a
        modulator of vascular tone and structure in the pulmonary
        circulation, and previous studies using NOS inhibitors [ 1,
        2] suggested that inhibition of NO increases acute hypoxic
        pulmonary vasoconstriction. Chronic NOS inhibition did not
        lead to development of pulmonary hypertension [ 3],
        however, possibly because of a decrease in cardiac output.
        These discrepancies have been addressed in recent studies
        using mice that are deficient in NOS isoforms.
        Three isoforms of NOS are found in the lung. The
        principle isoform that is found in the pulmonary
        vasculature is eNOS [ 4]. iNOS is expressed in airway
        epithelium, and airway and vascular smooth muscle [ 5, 6],
        whereas nNOS is expressed in the bronchial epithelium and
        lung nervous tissue [ 4, 5, 7, 8]. Thus, all three NOS
        isoforms could contribute to modulation of pulmonary
biomed/rr74.txt lines 1-23/426 5%
```

ex2:
The command `less -M government/Alcohol_Problems/Session2-PDF.txt` outputs:
```

Session 2.
Identifying ED Patients with Alcohol Problems

Robert Woolard, MD
Many patients in the emergency department (ED) have alcohol
problems, and they can be identified.1 Research on techniques used
to identify these patients has been conducted, but several areas of
interest should be addressed by further research. We need to
further examine and refine alcohol-screening questionnaires in the
ED. We need to determine the sequence and combination of questions
and tests that constitute the best screening process. We need to
study barriers to screening, identify factors that promote
screening implementation, and demonstrate the impact of a screening
program in the ED. The final aim of screening must be improved
outcomes through referral and counseling. Identification is only
the first step in a process of care.
Alcohol problems defined
Alcohol problems designate a spectrum from risk behavior to
illness, and from problematic consumption to alcohol use disorder.
government/Alcohol_Problems/Session2-PDF.txt lines 1-23/637 3%
```

###
ex1:
The command `less -pDemocrats 911report/preface.txt` outputs:
```
Democrats chosen by elected leaders from our nation's capital at a time of great
                partisan division-have come together to present this report without dissent.
            We have come together with a unity of purpose because our nation demands it.
                September 11, 2001, was a day of unprecedented shock and suffering in the history of
                the United States. The nation was unprepared. How did this happen, and how can we
                avoid such tragedy again?
            To answer these questions, the Congress and the President created the National
                Commission on Terrorist Attacks Upon the United States (Public Law 107-306, November
                27, 2002).
            Our mandate was sweeping. The law directed us to investigate "facts and circumstances
                relating to the terrorist attacks of September 11, 2001," including those relating
                to intelligence agencies, law enforcement agencies, diplomacy, immigration issues
                and border control, the flow of assets to terrorist organization911report/preface.txt

```

ex2:
The command `` outputs:
```
          ambient conditions, hypobaric hypoxia (simulating an
          altitude of 17,000 feet), or hyberbaric normoxia
          (simulating sea level). Exposure was continuous, with
          minimal interruption for animal care. At 21 days the dam
          was removed and animals were sorted by sex. At 6 weeks
          animals of both sexes were removed for study.
        
        
          Right ventricular pressure measurements
          RVsP was measured as previously described [ 9].
          Briefly, mice were anesthetized with ketamine/xyalazine
          (100/15 mg/kg), placed supine while spontaneously
          breathing room air, and a 26-gauge needle was introduced
          percutaneously into the thorax via a subxyphloid
          approach; RVsP was recorded. Blood was drawn and animals
          were killed. The thorax was opened and the lungs were
          flushed with cold PBS. The right lung was frozen for
          protein and RNA measurement, and the left lung was fixed
          for histologic evaluation.
        
        
          Western blotting
          Frozen lung tissue was homogenized in ice cold 750 μl
:
```

### Citations
Information about uses of the less command was gathered from:
    `man less` command and the website: [Source 1](https://phoenixnap.com/kb/less-command-in-linux)

