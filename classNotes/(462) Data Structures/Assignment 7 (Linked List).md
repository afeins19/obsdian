# Part 1 - Singly Linked Lists
```python
"""
Use cases of singly linked lists: 

1. Music Library/Music Queue: singly linked lists may be used to construct a play order for songs in a playlist or library.

2. Function composition: a series of composed functions (like f(g(x))) may be represented with a linked list. The output of each function will point to the next one for which it is an input.

3. Undo-Operation Feature: Programs such as photo or text editors have an undo button feature which will allow the user to revet back 1 step from the current state. This may be done by storing each action in a linked list and then reversing back when needed.


"""

class node:
    def __init__(self,data):
        self.data = data
        self.next = None

class linkedlist:
    def __init__(self):
        self.head = None
        self.tail = None

    def append(self, data):
        if self.head is None:
            # If the list is empty, create a new node and set it as both head and tail
            self.head = node(data)
            self.tail = self.head
        else:
            # If the list is not empty, append a new node to the end and update  tail
            new_node = node(data)
            self.tail.next = new_node
            self.tail = new_node

    def traverse(self):
        curr = self.head
        out = ""
        while curr:
            out+=" -> " + str(curr.data)
            curr = curr.next

        print(out)
    def find_node(self, data):
        # this will find the first occurence of the node matching the argument passed in

        curr = self.head
        prev = None
        while curr.data != data:
            prev = curr
            curr= curr.next

        # returns a tuple with the previous node (for perserving linkage) and the current node
        return (prev, curr)

    def delete(self, data):
        prev, curr = self.find_node(data)

        if curr:
            if prev:
                # Node is not the head
                prev.next = curr.next
            else:
                # Node is the head
                self.head = curr.next

            if curr == self.tail:
                # Node is the tail, update the tail pointer
                self.tail = prev

            curr.next = None

    def reverse(self):
        curr = self.head
        prev = None
        next = None

        #1. save the state of the next node
        #2. set the current node to point the prev (none at first)
        #3. move prev and curr up 1 node and repeat
        while curr:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next

        self.tail = self.head  # Update the tail pointer to the new head
        self.head = prev  # Update the head pointer to the last node

    def start_insert(self, data):
        if not self.head:
            self.append(data)
        else:
            temp = self.head.next
            self.head = node(data)
            self.head.next = temp

    def middle_insert(self, insertBefore, data):
        # getting previous and current node (prev, curr)
        prev, curr = self.find_node(insertBefore)

        # create a new node with the data, and insert before the target in argument
        if prev and curr:
            new_node = node(data)
            prev.next = new_node
            new_node.next = curr

    def end_insert(self, data):
        self.append(data)


# Demonstration
"""A user has a music app open on their phone and wishes to queue the songs given in the list below"
"""
tracks = ["[Disturbia - Rhianna]",
          "[Notorious Thugs - Notorious B.I.G]",
          "[Miami - Will Smith]",
          "[Ma Cherie - DJ Antoine]"]

# we add them to a playlist for the user
playlist = linkedlist()

for track in tracks:
    playlist.append(track)

# Here is a printed representation of the users tracks
print("\nPlaylist: ")
playlist.traverse()


# The app has a function to reverse the order of the tracks
print("\nReversing Play Order: ")
playlist.reverse()
playlist.traverse()



# the user spontaneously selects a song to play from his library
# the app handels this by immediatly playing the selected song and setting
# the previous song to play after this one
print("\nUser Plays starts playing another song: ")
playlist.start_insert("[Boom Boom Pow - Black Eyed Peas]")
playlist.traverse()




# the user wants to queue a song a bit later in the playlist (after [Miami - Will Smith])
print("\nInserting a track in the middle of the playlist: ")
playlist.middle_insert("[Miami - Will Smith]", "[DNA - Kendrick Lamar]")
playlist.traverse()



# the user decides that he no longer wishes to listen to disturbia (for some reason)
# to remove it from the playlist, the app searches for the node representing that song
# and removes it
print("\n Removing the selected song: ")
playlist.delete("[Disturbia - Rhianna]")
playlist.traverse()



# the the app has a dedicated functionality to inserting a track to the end of the playlist
# the 'append()' function covered in class is sufficient to do this
print("\nInserting a track at the end of the playlist")
playlist.end_insert("[Hey Jude - Beatles]")
playlist.traverse()

```

## Testing & Output
``` 
Playlist: 
 -> [Disturbia - Rhianna] -> [Notorious Thugs - Notorious B.I.G] -> [Miami - Will Smith] -> [Ma Cherie - DJ Antoine]

Reversing Play Order: 
 -> [Ma Cherie - DJ Antoine] -> [Miami - Will Smith] -> [Notorious Thugs - Notorious B.I.G] -> [Disturbia - Rhianna]

User Plays starts playing another song: 
 -> [Boom Boom Pow - Black Eyed Peas] -> [Miami - Will Smith] -> [Notorious Thugs - Notorious B.I.G] -> [Disturbia - Rhianna]

Inserting a track in the middle of the playlist: 
 -> [Boom Boom Pow - Black Eyed Peas] -> [DNA - Kendrick Lamar] -> [Miami - Will Smith] -> [Notorious Thugs - Notorious B.I.G] -> [Disturbia - Rhianna]

 Removing the selected song: 
 -> [Boom Boom Pow - Black Eyed Peas] -> [DNA - Kendrick Lamar] -> [Miami - Will Smith] -> [Notorious Thugs - Notorious B.I.G]

Inserting a track at the end of the playlist
 -> [Boom Boom Pow - Black Eyed Peas] -> [DNA - Kendrick Lamar] -> [Miami - Will Smith] -> [Notorious Thugs - Notorious B.I.G] -> [Hey Jude - Beatles]

Process finished with exit code 0

```


# Part 2: Doubly Linked Lists
```python 
"""Uses of Doubly Linked Lists:

    these differ from singly linked lists because each node now stores a pointer to the previous node in the chain.
    This makes traversal more efficient since we only need to keep track of the current node as the current node has a
    reference to the previous one.

    Uses for doubly linked lists:

    1. Text Editor: a doubly linked list can be used to create a text editing program. Each node is a charecter
    in am instance of the text editor. The cursor position may be next to any given charecter and may move forward or backwards.
    The cursor will know where to move from any given charecter as each one will always point back or forward to its neighbor

    2. Dynamic memory: we can efficiently implement a memory management system with the use of doubly linked-lists. Memory
    Blocks can change as required by some operating system or allocator and nodes will be the programs uing those memory blocks.
    when a program frees up some memory, it may be allocated to another program efficiently.

    3. Polynomial Representation Program: we can efficiently represent polynomial expressions with doubly linked lists.
    Each term in the polynomial expression is a node and it will keep track of its position relative to its right and left
    neighbor.
"""
class node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

class DoubleyLinkedList:

    def __init__(self):
        self.head = None
        self.tail = None

    def append(self, data):
        if not self.head:
            self.head = node(data)
            self.tail = self.head

        else:
            new_node = node(data)
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node


    def traverse(self):
        curr = self.head
        while curr:
            print(curr.data)
            curr = curr.next

    def find_node(self, data):
        curr = self.head

        while curr and not curr.data == data:
            curr = curr.next

        return curr

    def delete(self, data):
        temp = self.find_node(data)

        if temp:
            if temp.prev:
                temp.prev.next = temp.next
            else:
                self.head = temp.next  # Update head if deleting the head

            if temp.next:
                temp.next.prev = temp.prev
            else:
                self.tail = temp.prev  # Update tail if deleting the

    def reverse(self):
        temp = None # swap place holder
        current = self.head


        while current:
            temp = current.prev # hold position of previous node
            current.prev, current.next = current.next, temp # swap prev and next of current node

            current = current.prev # move to next node in the chain but by using the prev (since we swapped)

        # make the head the previous tail
        if temp:
            self.head = temp.prev

    def start_insert(self, data):
        if self.head:
            temp_head = self.head

            # creating a new node with the data passed in
            head = node(data)

            temp_head.prev = head # pointing back to the new head

            self.head = head # setting this new node as the head
            self.head.next = temp_head # pointing it to the previous head
            self.head.prev = None
        else:
            return

    def middle_insert(self, data, insert_before): # specify what node to insert this one before
        insert_location = self.find_node(insert_before) # traversing the linked list until we find the right node

        if insert_location:  # making sure that node exists
            insertion = node(data)  # creating the new node

            temp_prev = insert_location.prev
            temp_prev.next = insertion
            insertion.prev = temp_prev  # point back from the new node to the one we are replacing in its position
            insertion.next = insert_location  # set our new node to point to the one we are inserting before

            insert_location.prev = insertion  # point back from the node we are inserting before

        else:
            return

    def end_insert(self, data):
        # finding the end of our linked list
        curr = self.head

        while curr:
            curr = curr.next

        if curr:
            # found the tail, now we point it to a new node
            insertion = node(data)
            curr.next = insertion # point the previous tail to our node
            insertion.prev = curr # point the new node back to the old tail
        else:
            return


test = DoubleyLinkedList()
for i in range(1,5):
    test.append(i)

print("Original Linked List (doubly):")
test.traverse()

test.start_insert(0)
print("Inserting at the start")
test.traverse()

print("\nInserting in the middle (between 2 and 3)")
test.middle_insert(2.5, insert_before=3)
test.traverse()

print("\nInserting at the end (value of 11)")
test.end_insert(6)
test.traverse()

print("\nReversal: ")
test.reverse()
test.traverse()
```

## Testing & Output
```
Original Linked List (doubly):
1
2
3
4
Inserting at the start
0
1
2
3
4

Inserting in the middle (between 2 and 3)
0
1
2
2.5
3
4

Inserting at the end (value of 11)
0
1
2
2.5
3
4

Reversal: 
4
3
2.5
2
1
0

Process finished with exit code 0

```