# Trie

The Trie (pronounced "try") data structure is a type of Tree. This data structure is widely used to store characters. Some of the main benefits of a Trie is looking up a word or a part of a word. It benefits from quick lookup of a word or parts of a word.  

## Objectives

* Understand benefits of the Trie data structure.
* Be able to implement a Trie Node. 
* Be able to implemeent the Trie data structure.
* Be able to insert a new word into a Trie. 
* Be able to search for a word in a Trie. 
* Be able to search for a prefix of a word in a Trie. 

## Implementation of a Trie Node 

A Trie node has the following properties: 

* the `char` to store. 
* children nodes 
* its parent 
* a property to determine if a word is complete 

We will also be adding a method to be able to add child nodes to the Trie node called `add()`. 

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

The Trie data structure has a `root` node like a regular Tree structure. 

We will be implementing the following methods on the Trie: 

* `insert()` 
* `getNode()`
* `search()`
* `prefix()`

```swift 
class Trie {
  private var root: TrieNode
  
  init() {
    self.root = TrieNode("*")
  }
  
  private func getNode(_ word: String) -> TrieNode? {
    var currentNode = root
    for char in word {
      guard let childNode = currentNode.children[char] else { return nil } // return nil if any node does not exist for a character
      
      // traverse the path where the "word" exist
      currentNode = childNode
    }
    return currentNode // we've found the node for the "word"
  }
  
  // inserts a word into the Trie
  func insert(_ word: String) {
    var currentNode = root
    
    // traverse the "word" and perform insertion accordingly
    for char in word {
      // look up children nodes to find out if node already exist
      if let childNode = currentNode.children[char] {
        // if it exist simply move down the path
        currentNode = childNode
      } else {
        // if the node does not exist, create and add a new child
        currentNode.add(char)
        
        // then move down the Trie
        guard let childNode = currentNode.children[char] else { return }
        currentNode = childNode
      }
    }
    
    // check if word is already marked complete
    guard !currentNode.isCompleteWord else { return }
    
    // mark work complete
    currentNode.isCompleteWord = true
  }
  
  // returns true if the word is in the Trie
  func search(_ word: String) -> Bool {
    guard let node = getNode(word) else { return false }
    return node.isCompleteWord
  }
  
  // returns true if there is any word in the Trie that starts with the given prefix
  func startsWith(_ prefix: String) -> Bool {
    guard let _ = getNode(prefix) else { return false }
    return true
  }
}
```

## Testing our Trie implementation 

```swift 
/*
                         *
                        /
                       s
                      / \
                     w   a
                    / \   \
                   i   e   t
                  /     \   \
                 f       e   *
                /         \
               t           t
              /             \
             *               *
*/


let trie = Trie()
trie.insert("swift")
trie.insert("sweet")
trie.insert("sat")

trie.search("swift") // true
trie.search("objectivec") // false

trie.startsWith("swe") // true
trie.startsWith("swa") // fasle
```

## Resources 

1. [Wikipedia - Trie](https://en.wikipedia.org/wiki/Trie)
2. [GeeksforGeeks - Trie](https://www.geeksforgeeks.org/trie-insert-and-search/)
3. [Video - Trie Data Structure](https://www.youtube.com/watch?v=-urNrIAQnNo)
4. [Video - HackerRank - Tries](https://youtu.be/zIjfhVPRZCg)
5. [Ray Wenderlich - Trie Tutorial](https://www.raywenderlich.com/892-swift-algorithm-club-swift-trie-data-structure)
6. [Ray Wenderlich - Swift Algo Club - Trie]( https://github.com/raywenderlich/swift-algorithm-club/tree/master/Trie)
7. [Video - Trie Implementation](https://www.youtube.com/watch?v=giiaIofn31A)
