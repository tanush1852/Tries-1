# Tries-1

## Problem1 
Implement Trie (Prefix Tree)(https://leetcode.com/problems/implement-trie-prefix-tree/)

## Time Complexity:O(N*L) Space Complexity:O(N*L)
class Trie {
    TrieNode root;
    class TrieNode{
    TrieNode[] children;
    boolean isEnd;

    public TrieNode(){
        this.children=new TrieNode[26];
    }
    }
    public Trie() {
       this.root=new TrieNode();
    }
    
    public void insert(String word) {
      TrieNode curr=root;
      for(char c:word.toCharArray()){
      if(curr.children[c-'a']==null)
      {
        curr.children[c-'a']=new TrieNode(); 
      } 
      curr=curr.children[c-'a'];
      } 

      curr.isEnd=true;
    }
    
    public boolean search(String word) {
        TrieNode curr=root;
        for(char c:word.toCharArray())
        {
            if(curr.children[c-'a']==null)
            return false;

            curr=curr.children[c-'a'];
        }
        return curr.isEnd;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode curr=root;
        for(char c:prefix.toCharArray())
        {
            if(curr.children[c-'a']==null)
            return false;
            curr=curr.children[c-'a'];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */



## Problem2
Longest Word in Dictionary(https://leetcode.com/problems/longest-word-in-dictionary/)
## Time Complexity:O(N*L) Space Complexity:O(N*L)
class Solution {
    
    class TrieNode {
        TrieNode[] children;
        boolean isEnd;
        String word;
        
        public TrieNode() {
            children = new TrieNode[26];
            isEnd = false;
            word = null;
        }
    }

    TrieNode root;  
    
    

    public void insert(String word) {
        TrieNode curr = root;
        for(char c : word.toCharArray()) {
            if(curr.children[c-'a'] == null) {
                curr.children[c-'a'] = new TrieNode(); 
            } 
            curr = curr.children[c-'a'];
        } 
        curr.isEnd = true;
        curr.word = word;
    }
    
    public boolean search(String word) {
        TrieNode curr = root;
       
        for(char c : word.toCharArray()) {
            if(curr.children[c-'a'] == null || !curr.children[c-'a'].isEnd) {
                return false;
            }
            curr = curr.children[c-'a'];
        }
        return curr.isEnd;
    }

    public String longestWord(String[] words) {
        root = new TrieNode();  // Initialize root
        for(String word : words) {
            insert(word);
        }

        String longest = "";  
        for(String word : words) {
            if(search(word)) {  
                if(word.length() > longest.length() || 
                   (word.length() == longest.length() && word.compareTo(longest) < 0)) {
                    longest = word;
                }
            }
        }
        return longest;
    }
}



## Problem3
Replace Words (https://leetcode.com/problems/replace-words/)
## Time Complexity:O(D*L +W*M) Space Complexity:O(D*L +W*M)

class Solution {

    TrieNode root;

    class TrieNode{
        TrieNode[] children;
        boolean isEnd;

        public TrieNode(){
            this.children=new TrieNode[26];
        }
    }  

    private void insert(String word){
        TrieNode curr=root;
        for(char c:word.toCharArray())
        {
            if(curr.children[c-'a']==null)
            {
                curr.children[c-'a']=new TrieNode();
            }
            curr=curr.children[c-'a'];
        }
        curr.isEnd=true;
    }
    public String replaceWords(List<String> dictionary, String sentence) {
        StringBuilder result=new StringBuilder();
        root=new TrieNode();

        for(String word:dictionary)
        {
            insert(word);
        }

        String[] splitArr=sentence.split(" ");
        for(int i=0;i<splitArr.length;i++){
            if(i>0)
            result.append(" ");
            result.append(getShortestVersion(splitArr[i]));
        }

        return result.toString();
    }

    private String getShortestVersion(String word)
    {
        StringBuilder result=new StringBuilder();
        TrieNode curr=root;

        for(char c:word.toCharArray()){
            if(curr.children[c-'a']==null || curr.isEnd)
            break;
           
            curr=curr.children[c-'a'];
            result.append(c);

        }
        if(curr.isEnd)
        return result.toString();

        return word;
    }
}