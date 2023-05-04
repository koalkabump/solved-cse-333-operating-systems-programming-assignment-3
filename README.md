Download Link: https://assignmentchef.com/product/solved-cse-333-operating-systems-programming-assignment-3
<br>
<h1></h1>

In this assignment, you will  write a program that will package books published by different publishers. You will have publisher and packager threads. After publishers publish books, packagers package the books published.

<ul>

 <li>The number of publisher types, publisher and packager threads will be given as command line argument. (i.e. You will have n number of publisher types. Each publisher type will have m publisher threads (at total, there will be m*n publisher threads). There will be k number of packager threads. All these numbers (n, m, and k) will be given as command line arguments.)</li>

 <li>Each publisher type threads will publish one type of book. The number of books that will be published by each publisher type will be given as command line argument.</li>

 <li>The books will be named according to its publisher type, i.e., the l<sup>th </sup>book published by the i<sup>th </sup>type of publisher will be named Booki_l.</li>

 <li>After publishing a new book, each publisher thread will put it in a buffer that is shared among the same type of publisher. (Each publisher type will have its own buffer.) The buffers’ initial size will be given as command line argument.</li>

 <li>When its buffer is full, the publisher thread that wants to put a book will double the size of the buffer.</li>

 <li>When each publisher thread publishes required number of books, they will exit the system.</li>

 <li>Packagers package the books published. They will take books from the buffers (each packager thread can take books from all buffers).</li>

 <li>Each packager thread will put some number of books in a package. This number will be given as command line argument.</li>

 <li>After one package is prepared, packager thread will prepare another package.</li>

 <li>Packagers will select the book type to put into package randomly. Then, it will take the book from the related buffer and put it into its own package.</li>

 <li>If a buffer of the publisher type randomly chosen by the packager thread is empty, the packager thread will check whether there are threads left in the system that belongs to chosen type. If so, it will wait for the publisher thread to publish a book and put it into the buffer. Otherwise, it will select another buffer.</li>

 <li>If a packager thread finds all buffers empty after all publisher threads exit the system, it will print the message: “Only i of j number of books could be packaged.” and leave the system. So, you need to keep track of how many publisher threads are left for each type. <strong><u>Program Details</u></strong></li>

 <li>The user will execute the program specifying the number of threads to be created of each kind.</li>

</ul>

You will then create the specified number of threads of each type.

<ul>

 <li>The same type of publisher threads will share the same buffer. Make sure that no multiple publisher thread will attempt to put their books on the same place of the buffer.</li>

 <li>Note that packager threads can access to all buffers. Make sure that no multiple package thread will attempt to get the same book from the buffer.</li>

 <li>Make sure that publisher and packager threads work concurrently. This means that when a publisher thread puts and item to the buffer, no packager can take an item from the buffer.</li>

 <li>The main thread is responsible for creating all of the threads and waiting for them. Note that, all of the threads has to exist in the system at the same time, and you have to work on synchronizing them.</li>

 <li>All the threads have to print information about their job on the screen (see the example execution below).</li>

 <li>Note that there are global buffers requested and the buffers can be accessed by many threads of different types so a synchronization and mutual exclusion are necessary for the buffer. This can be achieved by using the semophores and mutexes.</li>

 <li>The global buffers have to be created at the very first time a thread needs to use it by that thread.</li>

 <li>Preserving consistency and preventing deadlocks are major issues to be considered.</li>

 <li>Your program will be executed as follows: o Example:</li>

</ul>

./project3.out -n 2 3 4 -b 5 -s 6 7 o The -n option represents the type and number of threads. Here 2 3 4 corresponds to publisher type, publisher thread count for each type and packager thread count respectively (there will be 2 types of publisher threads, each type will have 3 publisher threads (so, there will be 6 publisher threads at total), and 4 packager threads).

<ul>

 <li>The -b option represents to number of books that should be published by each publisher. 5 indicates that each publisher thread will publish 5 books (at total, there will be 30 books published, 15 belonging to first type, 15 belonging to second type).</li>

 <li>The -s option represents the package and initial buffer size, respectively (each packager thread will put 6 books at each package and the initial buffer size will be 7 for each type of publisher threads (remember that each publisher type has its own buffer)).</li>

</ul>

<ul>

 <li>Your program should produce output. o Example:</li>

</ul>

&lt;Thread-type and ID&gt;                       &lt;Output&gt;

Publisher 1 of type 1             Book1_1 is published and put into the buffer 1.

Publisher 2 of type 2             Book2_1 is published and put into the buffer 2.

Publisher 2 of type 2              Book2_2 is published and put into the buffer 2.

<table width="386">

 <tbody>

  <tr>

   <td width="189">Packager 1</td>

   <td width="197">Put Book2_1 into the package.</td>

  </tr>

  <tr>

   <td width="189">Packager 2</td>

   <td width="197">Put Book2_2 into the package.</td>

  </tr>

  <tr>

   <td width="189">Packager 1</td>

   <td width="197">Put Book1_1 into the package.</td>

  </tr>

 </tbody>

</table>

…………………………………………………………………………………………………………….

Publisher 2 of type 1              Finished publishing 5 books. Exiting the system.

…………………………………………………………………………………………………………….

Packeger 4                             Finished preparing one package. The package contains:

Book2_3, Book2_7 …. Book1_13.

Publisher 3 of type 1               Buffer is full. Resizing the buffer.

……………………………………………………………………………………………………………..


