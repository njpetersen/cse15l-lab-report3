## eryfer ##
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
} ```
