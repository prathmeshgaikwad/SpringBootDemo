Java Streams Interview Questions
package com.springboot.questions;
import java.util.Arrays;
import java.util.Comparator;
import java.util.HashSet;
import java.util.IntSummaryStatistics;
import java.util.LinkedHashMap;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
import java.util.stream.Stream;
public class JavaStreams
{
public static void main(String[] args)
{
String[] words = { "apple"
,
"orange"
,
"cherry"
,
"pineapple" };
JavaStreams demo = new JavaStreams();
System.out.println(demo.findNthLargestString(words, 2));
}
public List<Integer> removeDuplicate(List<Integer> nums)
{
// Java 7 Way
// Set<Integer> set = new HashSet<>();
// for (Integer no : nums)
// {
// set.add(no);
// }
// return new ArrayList<Integer>(set);
// Java 8 Way
// Set<Integer> set =
nums.stream().distinct().collect(Collectors.toSet());
// return new ArrayList<Integer>(set);
List<Integer> numsWithoutDuplicates = new
HashSet<Integer>(nums).stream().collect(Collectors.toList());
numsWithoutDuplicates.stream().forEach(System.out::println);
return numsWithoutDuplicates;
}
public List<Integer> removeDuplicatePreserveOrder(List<Integer>
nums)
{
// Java 7 Way
// Set<Integer> set = new HashSet<>();
// List<Integer> ans = new ArrayList<>();
// for (Integer no : nums)
// {
// if (set.add(no))
// {
// ans.add(no);
// }
// }
// return ans;
// Java 8 Way
List<Integer> numsWithoutDuplicates =
nums.stream().distinct().collect(Collectors.toList());
numsWithoutDuplicates.stream().forEach(System.out::println);
return numsWithoutDuplicates;
}
public List<Integer> findNumStartingWithPrefix(List<Integer>
nums, String prefix)
{
// Java 7 Way
// List<Integer> noStartingWithPrefix = new ArrayList<>();
// for (int no : nums)
// {
// if (String.valueOf(no).startsWith(prefix))
// {
// noStartingWithPrefix.add(no);
// }
// }
// return noStartingWithPrefix;
// Java 8 Way
// return nums.stream()
// .filter(no -> (no+"").startsWith(prefix))
// .collect(Collectors.toList());
List<Integer> noStartingWithPrefix = nums.stream().filter(no
-> String.valueOf(no).startsWith(prefix))
.collect(Collectors.toList());
noStartingWithPrefix.stream().forEach(System.out::println);
return noStartingWithPrefix;
}
public Stream<Integer> joinTwoStreams(List<Integer> nums1,
List<Integer> nums2)
{
Stream<Integer> combinedStream =
Stream.concat(nums1.stream(), nums2.stream());
combinedStream.forEach(System.out::println);
return combinedStream;
}
public List<Integer> mergeSortedLists(List<Integer> nums1,
List<Integer> nums2)
{
List<Integer> mergedSortedList =
Stream.concat(nums1.stream(), nums2.stream()).sorted()
.collect(Collectors.toList());
mergedSortedList.stream().forEach(System.out::println);
return mergedSortedList;
}
public boolean containsPrime(List<Integer> nums)
{
// Java 7 Way
// boolean isPrimeFound = false;
// for(Integer num : nums) {
// if(isPrime(num)) {
// isPrimeFound = true;
// break;
// }
// }
// return isPrimeFound;
// Java 8 Way
// boolean isPrimeFound =
nums.stream().anyMatch(num->isPrime(num));
boolean isPrimeFound =
nums.stream().anyMatch(this::isPrime);
System.out.println("containsPrime: " + isPrimeFound);
return isPrimeFound;
}
{
public boolean isPrime(int num)
if (num <= 1)
return false;
// Java 7 Way
// boolean isPrimeFound = false;
// for(int i=2; i<Math.sqrt(num); i++) {
// if(num % i == 0) {
// isPrimeFound = true;
// break;
// }
// }
// return isPrimeFound;
// Java 8 Way
boolean isPrimeFound = IntStream.rangeClosed(2, (int)
Math.sqrt(num)).noneMatch(i -> num % i == 0);
System.out.println("isPrime: " + isPrimeFound);
return isPrimeFound;
}
{
public void debugUsingPeek(List<String> words)
List<String> result = words.stream().peek(w ->
System.out.println("Original: " + w))
.filter(word -> word.startsWith("a")).peek(w ->
System.out.println("After filter: " + w))
.map(String::toUpperCase).peek(w ->
System.out.println("After map: " + w)).collect(Collectors.toList());
result.stream().forEach(System.out::println);
}
public List<String> stringStartingWithNumber(List<String> words)
{
List<String> result = words.stream().filter(word ->
Character.isDigit(word.charAt(0)))
.collect(Collectors.toList());
result.stream().forEach(System.out::println);
return result;
}
{
public boolean checkPalindrome(String str)
int n = str.length();
// Java 7 Way
// boolean isPalindrome = true;
// for (int i = 0; i < n/2; i++)
// {
// if (str.charAt(i) != str.charAt(n - 1 - i))
// {
// isPalindrome = false;
// break;
// }
// }
// return isPalindrome;
boolean isPalindrome = IntStream.range(0, n / 2).allMatch(i
-> str.charAt(i) == str.charAt(n - 1 - i));
System.out.println("isPalindrome: " + isPalindrome);
return isPalindrome;
public List<Double> sortDoubleReverseOrder(List<Double>
nums)
}
{
List<Double> sortedNums =
nums.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toLi
st());
sortedNums.forEach(System.out::println);
return sortedNums;
}
{
public Integer findNthSmallestNum(List<Integer> nums, int n)
// Optional<Integer> nthSmallest = nums.stream().skip(n -
1).findFirst();
// return nthSmallest.isPresent() ? nthSmallest.get() : -1;
return nums.stream().sorted().skip(n -
1).findFirst().orElse(-1);
}
public int findNthSmallestNum(int[] nums, int n)
{
// Optional<Integer> nthSmallest = nums.stream().skip(n -
1).findFirst();
// return nthSmallest.isPresent() ? nthSmallest.get() : -1;
return Arrays.stream(nums).sorted().skip(n -
1).findFirst().orElse(-1);
}
{
public Integer findNthLargestNum(List<Integer> nums, int n)
// Optional<Integer> nthLargest =
nums.stream().sorted().skip(n - 1).findFirst();
// return nthLargest.isPresent() ? nthLargest.get() : -1;
return
nums.stream().sorted(Comparator.reverseOrder()).skip(n -
1).findFirst().orElse(-1);
}
{
public int findNthLargestNum(int[] nums, int n)
// Optional<Integer> nthLargest =
nums.stream().sorted().skip(n - 1).findFirst();
// return nthLargest.isPresent() ? nthLargest.get() : -1;
return
Arrays.stream(nums).boxed().sorted(Comparator.reverseOrder()).skip(n
- 1).findFirst().orElse(-1);
}
{
public int findLastElement(int[] nums)
// return nums[nums.length-1];
return Arrays.stream(nums).skip(nums.length -
1).findFirst().orElse(-1);
}
{
public int findLastElement(List<Integer> nums)
// return nums.get(nums.size()-1);
return nums.stream().skip(nums.size() -
1).findFirst().orElse(-1);
}
{
public String joinStrings(List<String> words, String delimiter)
return words.stream().map(word -> "[" + word +
"]").collect(Collectors.joining(delimiter));
}
public String joinStrings(List<String> words, String prefix, String
suffix, String delimiter)
{
return words.stream().collect(Collectors.joining(prefix, suffix,
delimiter));
}
{
public int sumOfFirstTwoNums(List<Integer> nums)
return
nums.stream().limit(2).mapToInt(Integer::intValue).sum();
}
{
public int sumOfFirstNNums(List<Integer> nums, int n)
// return
nums.stream().limit(n).mapToInt(Integer::intValue).sum();
return nums.stream().limit(n).reduce((a, b) -> a +
b).orElse(-1);
}
{
public int sumOfFirstNNums(int[] nums, int n)
return Arrays.stream(nums).limit(n).sum();
// return
Arrays.stream(nums).limit(n).reduce((a,b)->a+b).orElse(-1);
}
public int sumOfUniqueNums(List<Integer> nums)
{
return
nums.stream().distinct().mapToInt(Integer::intValue).sum();
// return nums.stream().distinct().reduce((a,b)->a+b).orElse(-1);
}
{
public int sumOfUniqueNums(int[] nums)
// return Arrays.stream(nums).distinct().sum();
return Arrays.stream(nums).distinct().reduce((a, b) -> a +
b).orElse(-1);
}
public List<String> wordsWithKVowels(List<String> words, int k)
{
// return words.stream().filter(word ->
word.chars().mapToObj(ch -> (char) ch).filter(ch ->
"aeiouAEIOU"
.indexOf(ch) != -1).count() == k).collect(Collectors.toList());
return words.stream().filter(word -> countVowel(word) ==
k).collect(Collectors.toList());
}
{
public long countVowel(String word)
return word.chars().mapToObj(ch -> (char) ch).filter(ch ->
"aeiouAEIOU"
.indexOf(ch) != -1).count();
}
{
public List<String> wordsWithKVowels(String sentence, int k)
return Arrays.stream(sentence.split(" ")).filter(word ->
countVowel(word) == k).collect(Collectors.toList());
}
{
public char findFirstNonRepeatingChar(String word)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() == 1).map(entry ->
entry.getKey()).findFirst().orElse('0');
}
public int findFirstNonRepeatingCharIndex(String word)
{
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() == 1).map(entry ->
word.indexOf(entry.getKey())).findFirst()
.orElse(-1);
}
{
public char findFirstRepeatingChar(String word)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() > 1).map(entry ->
entry.getKey()).findFirst().orElse('0');
}
{
public int findFirstRepeatingCharIndex(String word)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() > 1).map(entry ->
word.indexOf(entry.getKey())).findFirst()
.orElse(-1);
}
{
public char findNthNonRepeatingChar(String word, int n)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() == 1).map(entry ->
entry.getKey()).skip(n).findFirst().orElse('0');
}
{
public int findNthNonRepeatingCharIndex(String word, int n)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() == 1).map(entry ->
word.indexOf(entry.getKey())).skip(n).findFirst()
.orElse(-1);
}
{
public char findNthRepeatingChar(String word, int n)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() > 1).map(entry ->
entry.getKey()).skip(n).findFirst().orElse('0');
}
{
public int findNthRepeatingCharIndex(String word, int n)
return word.chars().mapToObj(ch -> (char) ch)
.collect(Collectors.groupingBy(ch -> ch,
LinkedHashMap::new, Collectors.counting())).entrySet().stream()
.filter(entry -> entry.getValue() > 1).map(entry ->
word.indexOf(entry.getKey())).skip(n).findFirst()
.orElse(-1);
}
{
public void printSummary(List<Integer> nums)
IntSummaryStatistics stats =
nums.stream().mapToInt(Integer::intValue).summaryStatistics();
System.out.println("Count: " + stats.getCount());
System.out.println("Sum: " + stats.getSum());
System.out.println("Min: " + stats.getMin());
System.out.println("Max: " + stats.getMax());
System.out.println("Average: " + stats.getAverage());
}
{
public int findMin(List<Integer> nums)
IntSummaryStatistics stats =
nums.stream().mapToInt(Integer::intValue).summaryStatistics();
return stats.getMin();
}
{
public int findMin(int[] nums)
return Arrays.stream(nums).min().getAsInt();
}
{
public int findMax(List<Integer> nums)
IntSummaryStatistics stats =
nums.stream().mapToInt(Integer::intValue).summaryStatistics();
return stats.getMax();
}
{
public int findMax(int[] nums)
return Arrays.stream(nums).max().getAsInt();
}
{
public int findSum(int[] nums)
// return Arrays.stream(nums).sum();
return Arrays.stream(nums).reduce(0, Integer::sum);
}
{
public String findNthLargestString(List<String> words, int n)
return words.stream().sorted((w1, w2) ->
Integer.compare(w2.length(), w1.length())).skip(n).findFirst()
.orElse("");
// return
Arrays.stream(nums).sorted(Comparator.comparingInt(String::length)).sk
ip(n - 1).findFirst().orElse("");
}
public String findNthLargestString(String[] words, int n)
{
return Arrays.stream(words).sorted((w1, w2) ->
Integer.compare(w2.length(), w1.length())).skip(n).findFirst()
.orElse("");
// return
Arrays.stream(words).sorted(Comparator.comparingInt(String::length)).s
kip(n - 1).findFirst().orElse("");
}
}