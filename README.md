# PermutationsProblem

I originally had a solution for finding distinct permutations figured out, so now I just need to determine all possible combinations
of strings order independent... recursive solution seemed to make the most sense.

I believe this will do it... but I will need to do some testing to verify.

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
    
    for(Iterator<String> it = list.iterator(); it.hasNext();) {
     System.out.println(it.next()); 
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

        HashSet<String> temp = generatePermutations(input);

        for (String string : temp)
        {
            for (int i = 0; i <= string.length(); i++)
            {
                returnVal.add(string.substring(0, i) + firstLetter + string.substring(i));
            }
        }
    }else {
        returnVal.add(firstLetter + "");
    }
    
    return returnVal;
  }
  
  public static HashSet<String> generateAllStrings(String[] values) {
    HashSet<String> allStrings = new HashSet<String>();
    HashSet<String> allPermutations = new HashSet<String>();
    for(int i = 0; i < values.length; i++) {
    	allStrings.addAll(generateAllStrings(values[i], values)); 
    }
    
    for(Iterator<String> it = allStrings.iterator(); it.hasNext(); ) {
     	allPermutations.addAll(generatePermutations(it.next()));
    }
    return allPermutations;
  }
  
  public static HashSet<String> generateAllStrings(String value, String[] values) {    
    HashSet<String> returnValue = new HashSet<String>();
    
    if(value.length() == values.length) {
    	returnValue.add(value);
      	return returnValue;
    }

    for(int i = 0; i < values.length; i++) {
      returnValue.addAll(generateAllStrings(value + values[i], values));
    }
    
    return returnValue;
  }
}
```
