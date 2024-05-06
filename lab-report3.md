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
### - 
ex1:
The command `less -N chapter-1.txt` produces the output:
`     
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
`


ex2:

###
ex1:

ex2:

###
ex1:

ex2:

###
ex1:

ex2:
### Citations
