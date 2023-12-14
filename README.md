Sorting element in array by frequency in Java
Here in this program, we will learn about Java program for Sorting element in array by frequency in java and discuss it. You need to print the elements of an array in the descending order of their frequency and if 2 numbers have same frequency then print the one which came first.

Sorting element in array by frequency in C++
Example

Input :arr[6]=[30, 20, 30, 10, 20, 20]
Output: 20 20 20 30 30 10
Method Discussed :
Method 1 : Using Naive Approach.
Method 2 : Using Hash map
Method 1:
Declare two 2d array arr[MAX][2] and brr[MAX][2].
Store 1d array in 0th index of arr array.
Set arr[][1] = 0, for all indexes up to n.
Now, count the frequency of elements of the array.
If element is unique the push it at brr[][0] array, and its frequency will represent by brr[][1].
Now, sort the brr on the basis of frequency.
Print the brr array on basis of their frequency.
Related Pages
Sort the elements of an array

Finding the frequency of elements in an array

Finding the Longest Palindrome in an Array

Counting Distinct Elements in an Array

Finding  Repeating elements in an Array

Method 1 : Code in Java
Run
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.List;
class Main {

    // Driver Code
    private static final int MAX = 254;
    public static void main(String[] args)
    {

         int [] a = {10, 20, 10, 10, 20, 30, 30, 30, 30, 0};
         int n = a.length;
         int[][] arr = new int[MAX][2];
         int[][] brr = new int[MAX][2];

         int k = 0, temp, count;

         for (int i = 0; i < n; i++){
             arr[i][0] = a[i];
             arr[i][1] = 0;
         }

         // Unique elements and its frequency are stored in another array
         for (int i = 0; i < n; i++){
              if (arr[i][1]==1)
                continue;
              count = 1;
              for (int j = i + 1; j < n; j++){
                   if (arr[i][0] == arr[j][0]){
                      arr[j][1] = 1;
                      count++;
                   }
              }
              brr[k][0] = arr[i][0];
              brr[k][1] = count;
              k++;
         }
         n = k;

         //Store the array and its frequency in sorted form
         for (int i = 0; i < n - 1; i++)
         {
             temp = brr[i][1];
             for (int j = i + 1; j < n; j++)
             {
                 if (temp < brr[j][1])
                 {
                      temp = brr[j][1];
                      brr[j][1] = brr[i][1];
                      brr[i][1] = temp;

                      temp = brr[j][0];
                      brr[j][0] = brr[i][0];
                      brr[i][0] = temp;
                  }
              }
          }
          for (int i = 0; i < n; i++)
          {
              while (brr[i][1] != 0){
                    System.out.print(brr[i][0]+" ");
                      brr[i][1]--;
              }
          }
   }

}
Output
30 30 30 30 10 10 10 20 20 0
Method 2 :
In this method we use hash map in java and then sort the values of the hash map.

Hash Map in Java
Java HashMap is a hash table based implementation of Java's Map interface.
A Map, as you might know, is a collection of key-value pairs.
It maps keys to values. HashMap is an unordered collection. It does not guarantee any specific order of the elements.
Method 2 : Code in Java
Run
import java.util.*;
public class Main {
	 static Integer[] arr = {10, 20, 10, 10, 20, 30, 30, 30, 30, 0};

	 public static void sortBasedOnFrequencyAndValue(List<Integer> list)
	   {
	       int n = arr.length;
	       final HashMap<Integer, Integer> mapCount = new HashMap<Integer, Integer>();
	       final HashMap<Integer, Integer> mapIndex = new HashMap<Integer, Integer>();
	       
	       for (int i = 0; i < n; i++) {
	           if (mapCount.containsKey(arr[i])) {
	              mapCount.put(arr[i],mapCount.get(arr[i]) + 1);
	           }
	           else {
	              mapCount.put(arr[i],1); // Map to capture Count of elements
	              mapIndex.put(arr[i],i); // Map to capture 1st occurrence of elements
	           }
	       }
	       Collections.sort(list, new Comparator<Integer>(){
	           public int compare(Integer n1, Integer n2)
	             {
	                  int freq1 = mapCount.get(n1);
	                  int freq2 = mapCount.get(n2);
	                  if (freq1 != freq2) {
	                      return freq2 - freq1;
	                  }
	                  else {
	                      return mapIndex.get(n1) - mapIndex.get(n2); 
	                  }
	             }
	       });
	       System.out.println(list);
	    }
	
	public static void main(String[] args) {
		List<Integer> list = Arrays.asList(arr);
	       sortBasedOnFrequencyAndValue(list);
	}
}
Output
[30, 30, 30, 30, 10, 10, 10, 20, 20, 0]
