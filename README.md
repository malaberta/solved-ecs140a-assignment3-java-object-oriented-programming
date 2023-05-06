Download Link: https://assignmentchef.com/product/solved-ecs140a-assignment3-java-object-oriented-programming
<br>
The purpose of this assignment is for you to gain experience with object-oriented programming in Java, and in particular the ideas of inheritance, dynamic binding (virtual methods), overriding and overloading methods. It will also give you some exposure to how some programming language features are implemented, <em>i.e.</em>, what happens “behind the scenes” when you execute a program. Although no language provides the exact features in this assignment, several languages (<em>e.g.</em>, Awk, Icon, Lisp, CLUS, SISAL) do provide similar features. Your program needs to implement several abstractions. The first abstraction is an Element, of which there are many kinds: MyInteger, MyChar and Sequence. MyInteger and MyChar respectively are class-based abstractions of int and char. Class Sequence is a dynamic array of Element objects. A Sequence object, thus stores objects of type MyInteger, MyChar and Sequence. The following is an example of a Sequence object:

[ 1 ‘a’ [1 3 ‘b’]]

In this example, the Sequence object contains three Element objects: 1, ‘a’ and another Sequence object [1 3 ‘b’]. Thus, a Sequence object may contain nested Sequence objects.

<h1>Part 1: Class Definitions</h1>

The first part of this homework requires you to define and implement the classes and their member methods. Use the names Element, MyInteger, MyChar and Sequence for your class definitions. Note that there is an <em>is-a </em>relationship between Element and MyInteger, MyChar and Sequence classes.

<ul>

 <li>Define constructor for each class. MyInteger objects are initialized to 0, MyChar objects to ’0’, and Sequence to an empty sequence, <em>e.</em>, a sequence with zero elements.</li>

 <li>Define Get and Set methods for Char and Integer:</li>

</ul>

class MyChar extends Element {

public MyChar() { … } public char Get() { … } public void Set(char val) { … } … }

class MyInteger extends Element {

public MyInteger() { … } public int Get() { … } public void Set(int val) { … } …

}

Methods Get and Set respectively are used to access and modify the value associated with an object. For instance, invocation of Get over a MyInteger object returns the integer value associated with the object.

<h1>Part 2: Additional Methods</h1>

Extend the definitions of the classes by defining the following methods:

<ol>

 <li>Define a Print member method for each class. Different objects are printed in the following manner:

  <ul>

   <li>Element: Define Print to be an abstract method.</li>

   <li>MyInteger: Print the corresponding integer value.</li>

   <li>MyChar: Print the quoted value of a MyChar object, <em>g.</em>, ’c’.</li>

   <li>Sequence: Print a sequence by surrounding the values of the elements in [, ], <em>g.</em>,</li>

  </ul></li>

</ol>

[ [ 1 ] [ 2 ] ‘3’ ‘c’ [ 1 3 [‘4’ ‘5’] ] ]

<ol start="2">

 <li>Define the following methods for the Sequence class:

  <ul>

   <li>Define method first to return the first element of the sequence: Element first();</li>

   <li>Define a method rest that returns the rest of the elements of the seqence:</li>

  </ul></li>

</ol>

Sequence rest();

Note that rest does not create a new sequence. It merely points to the rest of the elements of the original sequence.

<ul>

 <li>Define a method length to return the number of elements in a Sequence object:</li>

</ul>

int length();

<ul>

 <li>Define a method add to add an element at a specified position:</li>

</ul>

void add(Element elm, int pos);

If an element already exists at pos, elm is inserted at pos. All elements starting at location pos are pushed to the right. If pos is not between 0 and the length of the Sequence object, flag an error and exit.

<ul>

 <li>Define a delete method to remove an element at a specified position:</li>

</ul>

void delete(int pos);

After deleting the element at pos, all elements to the right of pos are pushed to the left. If there are no elements at pos, the Sequence object remains unchanged.

<h1>Part 3: Additional Methods of Sequence</h1>

Class Sequence defines the following additional methods:

<ol>

 <li>index to access the element at a particular position:</li>

</ol>

public Element index(int pos);

The method index is used to access a particular element of a Sequence object. For instance, S.index(0) returns the first element of S. If pos is not between 0 and the length of the Sequence object, flag an error and exit.

<ol start="2">

 <li>flatten to flatten a sequence: public Sequence flatten();</li>

</ol>

An example usage of flatten is shown below:

flatten ([1 2 [1 3 4] [‘s’ a b] ]) = [1 2 1 3 4 ‘s’ a b]

Note that flatten returns a new Sequence object.

<ol start="3">

 <li>copy to perform a <em>deep copy </em>of a Sequence object: public Sequence copy();</li>

</ol>

<h1>Part 4: Iterator over Sequence</h1>

Define a SequenceIterator class to serve as an iterator over Sequence objects. An iterator object is used to iterate over a data structure. Note also that there can be multiple SequenceIterator objects for a

Sequence object.

The Sequence class must be extended to implement the following member methods:

class Sequence extends Element {

SequenceIterator begin();

SequenceIterator end(); …

}

Method begin returns a SequenceIterator object that points to the first element of the sequence. Method end, on the other hand, returns a SequenceIterator object that points to a special value after the last element of a Sequence object. This special value is used merely to indicate that an iterator has gone beyond the last element of a Sequence object. It can be implemented by adding an extra dummy element to a Sequence object.

Define the following methods for SequenceIterator:

<ol>

 <li>advance to advance a SequenceIterator to the next element in a Sequence object.</li>

 <li>get to return the object to which the SequenceIterator object points.</li>

 <li>equal to determine if two SequenceIterator objects point to the same element.</li>

</ol>

The interface of the SequenceIterator class may look like the following:

class SequenceIterator { …

public bool equal (SequenceIterator other) { … }

SequenceIterator advance();

Element get(); …

}

The following code fragment shows a possible usage of the iterator:

Sequence seq;

SequenceIterator it;

for (it = seq.begin(); it != seq.end(); it.advance()) { (it.get()).f();

}

The above applies method f over all elements of seq.

<h1>Part 5: Two Dimensional Sequences</h1>

Define a class Matrix by extending Sequence. Matrix represents a two dimensional array of integers, and defines the following methods:

class Matrix extends Sequence {

// constructor for creating a matrix of specific number of rows and columns Matrix(int rowsize, int colsize);

void Set(int rowsize, int colsize, int value); // set the value of an element int Get(int rowsize, int colsize); // get the value of an element

Matrix Sum(Matrix mat); // return the sum of two matrices: mat &amp; this Matrix Product(Matrix mat); // return the product of two matrices: mat &amp; this void Print(); // print the elements of matrix }

<h1>Part 6: Map</h1>

This part of the homework involves modifying the Sequence class so that the elements of a Sequence object can be stored and retrieved using a key. We will call this class Map. A Map object therefore stores a set of Pair objects. Each Pair object contains a key object and a value object. A key object refers to a MyChar object whereas a value object can refer to any type of <em>Element</em>. An example of a Map object is shown below:

[ (‘1’ ‘a’) (‘3’ ‘h’) (‘8’ 4) ]

This Map object contains three Pair objects: (‘1’ ‘a’), (‘3’ ‘h’), and (‘8’ 4). The first component in each Pair object is the key object whereas the second is the value object. Note that the elements of the Map object are ordered according to the key object. Define the following for the Map class:

<ol>

 <li>Define an iterator class MapIterator for the Map class. The behavior of a MapIterator object is similar to that of a SequenceIterator object. MapIterator implements all methods that SequenceIterator supports.</li>

 <li>Methods begin, end, and Print. Methods begin and end are similar to those of the Sequence class (see Part 4). Method Print prints a map object in the following manner:</li>

</ol>

[ (‘1’ 1) (‘2’ 2) (‘3’ 8) ]

The first is the key object, and the second is the value object.

<ol start="3">

 <li>add method for adding a Pair object: public void add(Pair inval);</li>

</ol>

The method add adds a Pair object, say p, in a Map object, say mp, by comparing the key value of p with the key values of the Pair objects of mp, and inserts p such that the key values of the Pair objects are in ascending order. Note that a Map object may contain Pair objects with identical keys. In the case when there are multiple Pair objects with the same key, p is added after these Pair objects.

<ol start="4">

 <li>find method for finding a Pair object given the key component:</li>

</ol>

public MapIterator find(MyChar key);

The argument to the find method is the key component of a Pair object. It is used to search a Map object for a Pair object. If the object exists, return a MapIterator object that points to the element. If the object does not exist, return a MapIterator object that points to the end element. If multiple Pair objects with the same key exist, return a MapIterator object that points to the first such Pair object.

<h1>Notes</h1>

<ul>

 <li>Note that Java provides several of these classes. For this assignment, you can only use pre-existing</li>

</ul>

Integer, Char and String classes for defining MyInteger, MyChar, and MyString respectively. You cannot use any other libraries or pre-existing classes for implementing other classes such as Sequence and Map. In other words, implement them from scratch.

<ul>

 <li>Do not be overly concerned with efficiency. On the other hand, do not write a grossly inefficient program.</li>

 <li>Express your program neatly. Part of your grade will be based on presentation. Indentation and comments are important. Be sure to define each variable used with a concise comment describing its purpose. In general, each procedure should have a comment at its beginning describing its purpose.</li>

 <li>Create several of your own test programs. Your will probably want different test data for the different parts. Be sure that your program works for boundary conditions.</li>

 <li>This program has no input data. Instead, you will be given test programs that will employ and exercise your classes. You may modify the tests during debugging, but you must use the unmodified tests for what you turn in.</li>

 <li>“Correct” output will also be given. Your output can differ in minor ways yet still be correct. It is up to you to verify your code’s correctness. In general, the easiest thing to do is to make your output conform to the given correct output and then use “make run”, which employs diff to test for and display differences.</li>

</ul>