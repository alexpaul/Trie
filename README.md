# Trie

The Trie (pronounced "try") data structure is a type of Tree. This data structure is widely used to store characters. Some of the main benefits of a Trie is looking up a word or a part of a word. It benefits from quick lookup of a word or parts of a word.  

## Objectives

* Understand benefits of the Trie data structure.
* Be able to implemeent the Trie data structure.

## Implementation of a Trie Node 

```swift 
class TrieNode {
  var char: Character // the character of the node
  var isCompleteWord: Bool // bool to indicate if the path is a complete word
  var children: [Character: TrieNode] // the children of the parent node
  var parent: TrieNode? // parent useful in thhe case of deleting nodes
  
  init(_ char: Character, parent: TrieNode? = nil) {
    self.char = char
    self.parent = parent
    self.isCompleteWord = false
    self.children = [:]
  }
  
  // add a new child to the node's children
  public func add(_ child: Character) {
    // check to see if the node already exist
    guard children[child] == nil else { return }
    
    // if not, create a new child
    children[child] = TrieNode(child, parent: self)
  }
}
```

## Trie Implementation 

```swift 
class Trie {
  private var root: TrieNode
  
  init() {
    self.root = TrieNode("*")
  }
  
  // inserts a word into the Trie
  func insert() {
    
  }
  
  // returns true if the word is in the Trie
  func search() {
    
  }
  
  // returns true if there is any word in the Trie that starts with the given prefix
  func startsWith() {
    
  }
}
```

## Resources 

1. [Wikipedia - Trie](https://en.wikipedia.org/wiki/Trie)
2. [GeeksforGeeks - Trie](https://www.geeksforgeeks.org/trie-insert-and-search/)
3. [Video - Trie Data Structure](https://www.youtube.com/watch?v=-urNrIAQnNo)
4. [Video - HackerRank - Tries](https://youtu.be/zIjfhVPRZCg)
5. [Ray Wenderlich - Trie Tutorial](https://www.raywenderlich.com/892-swift-algorithm-club-swift-trie-data-structure)
6. [Ray Wenderlich - Swift Algo Club - Trie]( https://github.com/raywenderlich/swift-algorithm-club/tree/master/Trie)
7. [Video - Trie Implementation](https://www.youtube.com/watch?v=giiaIofn31A)
