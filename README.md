# Sentence Similarity
## https://leetcode.com/problems/sentence-similarity

We can represent a sentence as an array of words, for example, the sentence "I am happy with leetcode" can be represented as arr = ["I","am",happy","with","leetcode"].

Given two sentences sentence1 and sentence2 each represented as a string array and given an array of string pairs similarPairs where similarPairs[i] = [xi, yi] indicates that the two words xi and yi are similar.

Return true if sentence1 and sentence2 are similar, or false if they are not similar.

Two sentences are similar if:

1. They have the same length (i.e., the same number of words)
2. sentence1[i] and sentence2[i] are similar.

Notice that a word is always similar to itself, also notice that the similarity relation is not transitive. For example, if the words a and b are similar, and the words b and c are similar, a and c are not necessarily similar.
```java
Example 1:

Input: sentence1 = ["great","acting","skills"], sentence2 = ["fine","drama","talent"], similarPairs = [["great","fine"],["drama","acting"],["skills","talent"]]
Output: true
Explanation: The two sentences have the same length and each word i of sentence1 is also similar to the corresponding word in sentence2.

Example 2:

Input: sentence1 = ["great"], sentence2 = ["great"], similarPairs = []
Output: true
Explanation: A word is similar to itself.

Example 3:

Input: sentence1 = ["great"], sentence2 = ["doubleplus","good"], similarPairs = [["great","doubleplus"]]
Output: false
Explanation: As they don't have the same length, we return false.
``` 

### Constraints:

1. 1 <= sentence1.length, sentence2.length <= 1000
2. 1 <= sentence1[i].length, sentence2[i].length <= 20
3. sentence1[i] and sentence2[i] consist of English letters.
4. 0 <= similarPairs.length <= 1000
5. similarPairs[i].length == 2
6. 1 <= xi.length, yi.length <= 20
7. xi and yi consist of lower-case and upper-case English letters.
8. All the pairs (xi, yi) are distinct.

## Implementation :
```java
class Solution {
    public boolean areSentencesSimilar(String[] sentence1, String[] sentence2, List<List<String>> similarPairs) {
        if(sentence1.length != sentence2.length)
          return false;
        Map<String,Set<String>> map = new HashMap<>();
        for(List<String> pair : similarPairs) {
            String word1 = pair.get(0);
            String word2 = pair.get(1);
            map.putIfAbsent(word1, new HashSet<String>());
            map.get(word1).add(word2);
            map.putIfAbsent(word2, new HashSet<String>());
            map.get(word2).add(word1);
        }
        for(int i = 0; i < sentence1.length; i++) {
            String word1 = sentence1[i], word2 = sentence2[i];
            if(word1.equals(word2))
              continue;
            if(!map.containsKey(word1))
              return false;
            if(!map.get(word1).contains(word2))
              return false;    
        }
        return true;
    }
}
```
