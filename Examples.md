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
* I can use annotations like`#charactor/name[id]`as place holders in my writing.
 
From the writer
----------
Looking at the story top down, I'd like to.....
*Assign tags to paragraphs, to make searching through project quick, and ease moving information around
*Moving paragraphs around needs to be easy.
*Allow blank "filler" spaces when there is a gap in the story (!null)
*Have cyoa action options separate from the preceding paragraph/text (unlike w/inkle) - so choices can move around
*Allow for "junk" of unused paragraphs, segments, or chains that can be cut/paste in as/if needed


As an engineer
------------
* I can create a graph out of the writers text
* The text is parseable to datoms like this
``` [ entity-id entity-attirbute attribute-value order]```
* The format is plain text
 
Feedback for that ^ and that v
------------
*What kind of graph? Word usage? Length?
*Would the writer be creating the story like  that v ? Or is that just the plain text at the back end?

Examples
---------
```clojure
{:chunk/name :random-scene
 :chunk/text
"""
Lots of story going on here telling the reader about all of the things, helping them get off just one more time when suddnely #char/name[:sexy-man] enters the room and  #phrases/synonym["fucks"] #char/name[:sexy-lady]. They then leave. Suddenly you have a choise!
"""
 :chunk/choices [
 {
   :choice/text "Punch #char/name[:sexy-man] in the face next time you see him and proceed to his room"
   :choice/go-to #chunk[:another-random-scene]
 }
  {
   :choice/text "make out with #char/name[:sexy-lady] in the face next time you see her while beating her with a dildo"
   :choice/go-to #chunk[:death]
 }
]
```


Tidbits

* `#thing[Identitfier]` is the notation I am using for getting objects. as you can see you can grab just a value from a with `#thing/attribute[Identifier]` (like the name of a charactor). Using this will allow us to trade out things.
* All of the squigly brackets `{}` mean dictionary/hash (a bunch of properties of a thing.
* All of the `[]` mean vector (fixed length list of things)
* The `:namespace/id` are called keywords, they are garenteed to be unique and equal. The namespace is a... well namespace for the identifier,
*  The `chunk` `phrase` `charactor` namespaces were arbitrary if you have better thoughts for them please pull request them.
