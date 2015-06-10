This file is for some examples of the writing format for cyoa.

It is also a short tutorial in how to add things to this file...
  1. click the edit button
  2. make your changes
  3. discribe your changes below
  4. I will review them and we will disscuss them
  5. Glory
  
Here are features that I can think of (not all of these will make the cut, just brainstorming)

As a writer
----------
I can annotate chunks of writing with
* Charactors invovled
* Place's invovled
* Options the user can choose
* Conditions about which place to go to next
* Use annotations like`#charactor/name[id]`as place holders in my writing.
 
From the writer
----------
Looking at the story top down, I'd like to.....
* Assign tags to paragraphs, to make searching through project quick, and ease moving information around
* Moving paragraphs around needs to be easy.
* Allow blank "filler" spaces when there is a gap in the story (!null)
* Have cyoa action options separate from the preceding paragraph/text (unlike w/inkle) - so choices can move around
* Allow for "junk" of unused paragraphs, segments, or chains that can be cut/paste in as/if needed


As an engineer
------------
* I can create a graph out of the writers text (like below) (note that edges and nodes are independent objects)
![example story graph](http://www.gamesbyangelina.org/wp-content/uploads/2013/09/Screen-Shot-2013-09-12-at-13.05.26-1024x512.png)
* The text is parseable to datoms like this
``` [ entity-id entity-attirbute attribute-value order]```
* The format is plain text
 
Feedback for that tech and that v
------------
* What kind of graph? Word usage? Length?
* Would the writer be creating the story like  that v ? Or is that just the plain text at the back end?

Examples
---------
```clojure
[
{
 :chunk/name :random-scene
 :chunk/text
"""
Lots of story going on here telling the reader about all of the things, helping them get off just one more time when suddnely #char/name[:sexy-man] enters the room and  #phrases/synonym["fucks"] #char/name[:sexy-lady]. They then leave. Suddenly you have a choise!
"""
  :chunk/tags ["awesome tag 1", "awsome tag 2", :tags-can-be-symbols-too]
}
{
  :chunk/name :not-yet-written
  :chunk/text ""
  :chunk/tags ["charactors have steamy sex, but sex scene generator is not ready"
}
{
 :chunk/name :another-better-scene
 :chunk/text
"""
A chicken is punched, leaving the religious people quite startled.
"""
  :chunk/tags ["awesome outher tag", :kelp]
  :chunk/notes
  """
    Free form flield for the writer to put notes about things? Useful I don't know.
  """
}

;; Write some choices for the user  (;; is comment in clojure)
{ :choice/from :another-better-scene
  :choice/to :random-scene
  :choice/text "punch chicken"}


{ :choice/from :another-better-scene
  :choice/to :random-scene
  :choice/text "don't punch chicken"
  :choice/comment "not that it really matters"}
  
;; You can write them in anywhere, 
;; when the story is rendered it quries the data base from all choices going from that chuck 
;; that query looks something like this 
[:find ?c
 :with ?origin_chunk
 :where [?c :choice/from ?origin_chunk]]
;; Find all ?c, with the paramater ?origin_chunk where ?c has the attribute :choice/from set to ?origin_chunk

                  


```


ChangeLog
---------
Reworked the structure of the story to be slightly flatter and allow more flexiblity around where choices are and how deeply nested they are. 

Tidbits

* `#thing[Identitfier]` is the notation I am using for getting objects. as you can see you can grab just a value from a with `#thing/attribute[Identifier]` (like the name of a charactor). Using this will allow us to trade out things.
* All of the squigly brackets `{}` mean dictionary/hash (a bunch of properties of a thing.
* All of the `[]` mean vector (fixed length list of things)
* The `:namespace/id` are called keywords, they are garenteed to be unique and equal. The namespace is a... well namespace for the identifier,
*  The `chunk` `phrase` `charactor` namespaces were arbitrary if you have better thoughts for them please pull request them.
