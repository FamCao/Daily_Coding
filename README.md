#  Daily Coding
Câu hỏi phỏng vấn được hỏi bởi Microsoft.
Số nguyên được biểu diễn bằng linked-list, trong đó mỗi node chứa giá trị của một chữ số của số nguyên đó, head node biểu diễn chữ số hàng đơn vị. Ví dụ: 1 -> 2 -> 3 -> 4 -> 5 biểu diễn 54321.
Cho 2 linked-lists biểu diễn 2 số nguyên. Trả về linked-list biểu diễn tổng của 2 số nguyên đó.
Ví dụ: cho 9 -> 8 và 5 -> 2, trả về 4 -> 1 -> 1; 89 + 25 = 114
``` python 
class Node:
   def __init__(self, dataval=None):
      self.dataval = dataval
      self.nextval = None

class SLinkedList:
   def __init__(self):
      self.headval = None

   def Number(self):
      printval = self.headval
      dem=0
      sum=0
      while printval is not None:
         sum+=printval.dataval*(10**dem)
         printval = printval.nextval
         dem+=1
      return sum
   def print(self):
      printval = self.headval
      while printval is not None:
         print (printval.dataval)
         printval = printval.nextval
def Sum (LinkedList1,LinkedList2):
  Sum_int=list1.Number()+list2.Number()
  Sum_str=str(Sum_int)
  LinkedList_Sum = SLinkedList()
  LinkedList_Sum.headval = Node(int(Sum_str[-1]))
  e2 = Node(int(Sum_str[-2]))
  LinkedList_Sum.headval.nextval = e2
  for i in reversed(Sum_str[0:-2]):
    e3 = Node(int(i))
    e2.nextval = e3
    e2=e3
  return LinkedList_Sum
  list1 = SLinkedList()
list1.headval = Node(9)
e2 = Node(8)
list1.headval.nextval = e2
e3 = Node(8)
e2.nextval=e3 

list2 = SLinkedList()
list2.headval = Node(5)
e2 = Node(2)
list2.headval.nextval = e2
Sum(list1,list2).print()
```
DC #37 [Medium] - 11.03.2022

Câu hỏi phỏng vấn được hỏi bởi Twitter.
Implement an autocomplete system. 
Bộ từ điển d là tập hợp các strings. Cho một query string s, yêu cầu trả về tất cả các string trong d mà có tiền tố = s.
Ví dụ: d = {"dog", "deer", "deal"}, s = "de" thì trả về {"deer", "deal"}.
Lưu ý: đây là hệ thống autocomplete, nên đừng bắt người dùng phải chờ hệ thống suy nghĩ quá lâu mới đưa ra được gợi ý
``` python 
class TrieNode():
    def __init__(self):
        # Initialising one node for trie
        self.children = {}
        self.last = False
class Trie():
    def __init__(self):
        # Initialising the trie structure.
        self.root = TrieNode()
    def formTrie(self, keys):
        # Forms a trie structure with the given set of strings
        # if it does not exists already else it merges the key
        # into it by extending the structure as required
        for key in keys:
            self.insert(key)  # inserting one key to the trie.
    def insert(self, key):
        # Inserts a key into trie if it does not exist already.
        # And if the key is a prefix of the trie node, just
        # marks it as leaf node.
        node = self.root
        for a in key:
            if not node.children.get(a):
                node.children[a] = TrieNode()
            node = node.children[a]
        node.last = True
    def suggestionsRec(self, node, word):
        # Method to recursively traverse the trie
        # and return a whole word.
        if node.last:
            print(word)
        for a, n in node.children.items():
            self.suggestionsRec(n, word + a)
    def printAutoSuggestions(self, key):
        # Returns all the words in the trie whose common
        # prefix is the given key thus listing out all
        # the suggestions for autocomplete.
        node = self.root
        for a in key:
            # no string in the Trie has this prefix
            if not node.children.get(a):
                return 0
            node = node.children[a]
        # If prefix is present as a word, but
        # there is no subtree below the last
        # matching node.
        if not node.children:
            return -1
        self.suggestionsRec(node, key)
        return 1
# Driver Code
keys = ["dog", "deer", "deal"]  # keys to form the trie structure.
key = "de"  # key for autocomplete suggestions.
# creating trie object
t = Trie()
# creating the trie structure with the
# given set of strings.
t.formTrie(keys)
# autocompleting the given key using
# our trie structure.
comp = t.printAutoSuggestions(key)
if comp == -1:
    print("No other strings found with this prefix\n")
elif comp == 0:
    print("No string found with this prefix\n")
 
# This code is contributed by amurdia and muhammedrijnas
```
