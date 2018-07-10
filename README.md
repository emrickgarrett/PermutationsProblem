# PermutationsProblem

I originally had a solution for finding distinct permutations figured out, so now I just need to determine all possible combinations
of strings order independent... recursive solution seemed to make the most sense. Still need to fix some compile issues that I brought
over from my pseudocode implementation.

```java
import java.lang.Math; // headers MUST be above the first class
import java.util.*;
import java.lang.*;

// one class needs to have a main() method
public class HelloWorld
{
  public static void main(String[] args)
  {
    String[] values = {"a", "b", "c", "d", "e"};
    
    HashSet<String> list = generateAllStrings(values);
    
    for(int i = 0; i < list.size(); i++) {
     System.out.println(list.get(i)); 
    }
  }
  
  public static HashSet<String> generatePermutations(String input) {
    HashSet<String> returnVal = new HashSet<String>();
    if (input == "") {
    	return returnVal;
    }

    Character firstLetter = input.charAt(0);

    if(input.length() > 1) {
        input = input.substring(1);

        HashSet<String> temp = generatePerm(input);

        for (String string : temp)
        {
            for (int i = 0; i <= string.length(); i++)
            {
                returnVal.add(string.substring(0, i) + firstLetter + string.substring(i));
            }
        }
    }else {
        returnVal.add(a + "");
    }
    
    return returnVal;
  }
  
  public static HashSet<String> generateAllStrings(String[] values) {
    HashSet<String> allStrings = new HashSet<String>();
    HashSet<String> allPermutations = new HashSet<String>();
    for(int i = 0; i < values.length; i++) {
    	allStrings.addAll(generateAllStrings(values[i], values)); 
    }
    
    for(int i = 0; i < allStrings.size(); i++) {
     	allPermutations.addAll(generatePermutations(allStrings.get(i)));
    }
    
    return allPermutations;
  }
  
  public static HashSet<String> generateAllStrings(String value, String[] values) {
    if(value.length() > values.length) { return new HashSet<String>(); }
    
    HashSet<String> returnValue = new HashSet<String>();
    
    for(int i = 0; i < values.length; i++) {
      returnValue.addAll(generateAllStrings(value + values[i], values));
    }
    
    return returnValue;
  }
}
```
