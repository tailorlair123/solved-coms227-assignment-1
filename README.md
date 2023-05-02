Download Link: https://assignmentchef.com/product/solved-coms227-assignment-1
<br>
<span style="font-size: 2.61792em; letter-spacing: -1px; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Overview</span>

The purpose of this assignment is to give you some practice with the process of implementing a class from a specification and testing whether your implementation conforms to the specification.




For this assignment you will implement one class, called <strong>WirelessPrinter</strong>, that models some aspects of the behavior of a simple wireless printer.  In particular, this class keeps track of the number of pages printed and the ink level in the printer, in addition to a few other things.




<h1>Specification</h1>




The specification for this assignment includes this pdf along with any “official” clarifications posted on Piazza.




<strong>There are three public constants: </strong>




<strong>public static final int PAGES_PER_CARTRIDGE = 1000; public static final int TRAY_CAPACITY = 500; public static final double NEW_CARTRIDGE_INK_LEVEL = 1.0; </strong>




<strong>There are two public constructors: </strong>




<strong>public WirelessPrinter() </strong>

Constructs a Printer that has a cartridge that is 50% full, which means the ink level is at 0.5.




<strong>public WirelessPrinter(double ink, int paper) </strong>

Constructs a Printer that has the given amount of ink and the given number of sheets of papers. The initial ink level must be between 0.0 and 1.0 and the initial paper count must be between 0 and 500, inclusive.




There are also a number of public methods, see the API.




<strong>Where’s the main() method?? </strong>

<strong> </strong>

There isn’t one!  Like most Java classes, this isn’t a complete program and you can’t “run” it by itself.  It’s just a single class, that is, the definition for a type of object that might be part of a larger system.  To try out your class, you can write a test class with a main method such the example below.

<strong> </strong>

<h1>Sample usage</h1>




A good way to think about the specification is to try to write some simple test cases and think about what behavior you expect to see. Here are a few examples:

<strong>public</strong> <strong>class</strong> WirelessPrinterTest {

<strong>public</strong> <strong>static</strong> <strong>void</strong> main(String[] args) {

WirelessPrinter printer = <strong>new</strong> WirelessPrinter(1.0, 500);




// turn it on and check its state

printer.turnOn();

System.<strong><em>out</em></strong>.println(printer.isOn()); // expected true

System.<strong><em>out</em></strong>.println(printer.isConnected()); // expected true

System.<strong><em>out</em></strong>.println(printer.getPaperLevel()); // expected 100(%)

System.<strong><em>out</em></strong>.println(printer.getInkLevel()); // expected 1.0




// try print            printer.print(50);

System.<strong><em>out</em></strong>.println(printer.getPaperLevel()); // expected 90

System.<strong><em>out</em></strong>.println(printer.getInkLevel()); // expected 0.95

System.<strong><em>out</em></strong>.println(printer.getTotalPagesPrinted()); //expected 50         System.<strong><em>out</em></strong>.println(printer.getTotalPaperUsed()); // expected 50




// try print more pages than what is left in the tray             printer.print(500); // out of paper

System.<strong><em>out</em></strong>.println(printer.getPaperLevel()); // expected 0

System.<strong><em>out</em></strong>.println(printer.getInkLevel());   // expected 0.5

System.<strong><em>out</em></strong>.println(printer.getTotalPagesPrinted());//expected 500

System.<strong><em>out</em></strong>.println(printer.getTotalPaperUsed());  // expected 500




// try loadPaper method             printer.loadPaper(1000);

System.<strong><em>out</em></strong>.println(printer.getPaperLevelExact()); // expected 500







// try replace the cartridge              printer.replaceCartridge();

System.<strong><em>out</em></strong>.println(printer.getInkLevel());   // expected 1.0




// try disconnect method            printer.disconnect(); // network goes off            printer.print(50);

System.<strong><em>out</em></strong>.println(printer.getPaperLevelExact()); // expected 500

System.<strong><em>out</em></strong>.println(printer.getInkLevel());   // expected 1.0

}

}




There is also a SpecChecker (see below) that will perform a lot of functional tests, but when you are developing and debugging your code at first you’ll always want to have some simple test cases of your own as in the <strong>main</strong> method above.

<strong> </strong>

<strong> </strong>

<h1>Suggestions for getting started</h1>

<strong> </strong>

<em>Smart developers don’t try to write all the code and then try to find dozens of errors all at once; they work <strong>incrementally</strong> and test every new feature as it’s written.   Here is a rough guide for how an experienced coder might go about creating a class such as this one: </em>




<ol>

 <li>Be sure understand the basics of defining a class as in Sections 3.1 – 3.3 of the text and as practiced in Lab 2.</li>

</ol>




<ol>

 <li>Create a new, empty project and add a package called <strong>hw1</strong>.</li>

</ol>




<ol start="2">

 <li>Create the <strong>WirelessPrinter</strong> class in the <strong>hw1</strong> package and put in stubs for all the required methods and constructors. For methods that are required to return a value, just put in a “dummy” <strong>return</strong> statement that returns zero or false.</li>

</ol>




<ol start="3">

 <li>Download the specchecker, import it into your project as you did in labs 1 and 2, and run it. There will be lots of error messages appearing in the console output, since you haven’t actually implemented the methods yet.  <em>Always start reading from the top.</em>  All you really want to check at this point is whether you have a missing or extra public method, if the method declarations are incorrect, or if something is really wrong like the class having the incorrect name or package.  <strong>Any such errors will appear <em>first</em> in the output and will usually say “Class does not conform to specification.”</strong></li>

</ol>




<ol start="4">

 <li>Look at each method. Mentally classify it as either an <em>accessor</em> (returns some information without modifying the object) or a <em>mutator</em> (modifies the object, usually returning <strong>void</strong>).  The accessors will give you a lot of hints about what instance variables you need.</li>

</ol>




<ol start="5">

 <li>Before you write code for a method, always write a simple usage example or test case, similar to the <strong>main</strong> method shown above. This will make sure you understand what the code is really supposed to do, and it will give later you a way to check whether you did it correctly.  Of course, if you are really <em>not</em> sure what a method is supposed to do, bring up your question for discussion on Piazza!</li>

</ol>




<ol start="6">

 <li><sup>You might start with loading and getting the paper level. Look at </sup><strong>getPaperLevelExact()</strong>.  It’s an accessor that returns the exact count of the sheets of paper in the tray.  That information has to be stored somehow within the <strong>WirelessPrinter</strong> object, which tells you that you probably need an instance variable to represent the sheet count.  Then <strong>loadPaper()</strong> is also simple to write.   Note there is a requirement that the number of papers in the tray cannot surpass its capacity.  You can do this easily using <strong>min</strong> to select the smaller of two values, for example</li>

</ol>

<strong>int paperLeft = Math.min(paperLeft + pages, TRAY_CAPACITY); </strong>




<ol start="7">

 <li>For the print() method, it should do nothing if the printer is not connected to the network. You can achieve it by placing the following statement at the top of your print() method.</li>

</ol>

<strong>public</strong> <strong>void</strong> print(<strong>int</strong> pages) {

<strong>if</strong> (!isConnected())

<strong>return</strong>; // do nothing

// the rest of the code goes here




<strong> </strong>

<h1>Additional notes</h1>

<ol>

 <li>You do NOT need conditional statements (“<strong>if</strong>” statements) or loops for this assignment (except for the print() method, for which how “if” should be used has been given above). We will start covering conditional statements later next week or in week 5, and you won’t be penalized if you use them, but you would just be making things more complicated. (If you have done some programming before and are tempted to use a bunch of if-statements, make it a challenge for yourself write simpler code without them.)</li>

</ol>




<ol>

 <li>If you need to find the smaller or larger of two, just use the methods <strong>min()</strong> or <strong>Math.max().</strong> As an example,</li>

</ol>

<strong>int x = Math.min(3, 4); // now x is 3 </strong>




<ol>

 <li>To round to the nearest integer, use <strong>round()</strong> <em>Note:</em> one little “gotcha” with <strong>Math.round</strong> is that it returns a type of integer value called a <strong>long</strong>, so you generally have to “cast” it to convert to the <strong>int</strong> type to use it in your code. It would look like this:</li>

</ol>




<strong>int x = (int) Math.round(y); </strong>

<ol>

 <li>You may want to use also <strong>floor()</strong>to get the largest int that is less than or equal to a given double value. It would look like this:</li>

</ol>




<strong>int x = (int) Math.floor(y);  </strong>




<ol start="2">

 <li>Do not add any additional public methods. (You can add your own methods if you feel compelled to do so, but they must be declared <strong>private</strong>.)  Do not create any additional Java classes.</li>

</ol>




<h1>The SpecChecker</h1>

You can find the SpecChecker online; see the Piazza Homework post for the link.  Import and run the SpecChecker just as you practiced in Labs 1 and 2.  It will run a number of functional tests and then bring up a dialog offering to create a zip file to submit.  Remember that error messages will appear in the console output.  There are many test cases so there may be an overwhelming number of error messages.  <strong><em>Always start reading the errors at the top and make incremental corrections in the code to fix them.</em></strong>  When you are happy with your results, click “Yes” at the dialog to create the zip file.  See the document “SpecChecker HOWTO”, which can be found in the Piazza pinned messages.




<h1>More about grading</h1>




This is a “regular” assignment so we are going to read your code.  Your score will be based partly (about a third) on the specchecker’s functional tests and partly on the grader’s assessment of the quality of your code.  This means you can get partial credit even if you have errors, and it also means that even if you pass all the specchecker tests you can still lose points.  Are you doing things in a simple and direct way that makes sense?  Are you defining redundant instance variables?  Some specific criteria that are important for this assignment are:




<ul>

 <li>Use instance variables only for the “permanent” state of the object, use local variables for temporary calculations within methods.</li>

</ul>

o You will lose points for having lots of unnecessary instance variables o All instance variables should be <strong>private</strong>.

<ul>

 <li><strong>Accessor methods should not modify instance variables</strong>.</li>

</ul>




See the “Style and documentation” section below for additional guidelines.




<h1>Style and documentation</h1>




Roughly 15% of the points will be for documentation and code style.  Here are some general requirements and guidelines:

<ul>

 <li>Each class, method, constructor and instance variable, whether public or private, must have a meaningful and complete Javadoc comment. Class javadoc must include the</li>

</ul>

<strong>@author</strong> tag, and method javadoc must include <strong>@param</strong> and <strong>@return</strong> tags as appropriate.   o Try to state what each method does in your own words, but there is no rule against copying and pasting the descriptions from this document or from the posted javadoc.

<ul>

 <li>Run the javadoc tool and see what your documentation looks like! You do not have to turn in the generated html, but at least it provides some satisfaction &#x1f642;</li>

</ul>




<ul>

 <li>All variable names must be meaningful (i.e., named for the value they store). Your code should not be producing console output. You may add <strong>println</strong> statements when debugging, but you need to remove them before submitting the code. • Use the defined constants <strong>PAGES_PER_CARTRIDGE, TRAY_CAPACITY, NEW_CARTRIDGE_INK_LEVEL.</strong></li>

</ul>




<ul>

 <li>Internal (//-style) comments are normally used inside of method bodies to explain <em>how</em> something works, while the Javadoc comments explain <em>what</em> a method does. (A good rule of thumb is: if you had to think for a few minutes to figure out how something works, you should probably include a comment explaining how it works.)   o Internal comments always <em>precede</em> the code they describe and are indented to the same level.  In a simple homework like this one, as long as your code is straightforward and you use meaningful variable names, your code will probably not need many internal comments.</li>

</ul>




<ul>

 <li>Use a consistent style for indentation and formatting.

  <ul>

   <li>Note that you can set up Eclipse with the formatting style you prefer and then use Ctrl-Shift-F to format your code. To play with the formatting preferences, go to Window-&gt;Preferences-&gt;Java&gt;Code Style-&gt;Formatter and click the New button to create your own “profile” for formatting.</li>

  </ul></li>

</ul>

<strong> </strong>

<h1>If you have questions</h1>

For questions, please see the Piazza Q &amp; A pages and click on the folder <strong>assignment1</strong>. If you don’t find your question answered, then create a new post with your question.  Try to state the question or topic clearly in the title of your post, and attach the tag <strong>assignment1</strong>.  <em>But remember, do not post any source code for the classes that are to be turned in.</em> It is fine to post source code for general Java examples that are not being turned in.  (In the Piazza editor, use the button labeled “pre” to have Java code formatted the way you typed it.)

<strong> </strong>

If you have a question that absolutely cannot be asked without showing part of your source code, make the post “private” so that only the instructors and TAs can see it.  Be sure you have stated a specific question; vague requests of the form “read all my code and tell me what’s wrong with it” will generally be ignored.




Of course, the instructors and TAs are always available to help you.  See the Office Hours section of the syllabus to find a time that is convenient for you.  We do our best to answer every question carefully, short of actually writing your code for you, but it would be unfair for the staff to fully review your assignment in detail before it is turned in.




Any posts from the instructors on Piazza that are labeled “Official Clarification” are considered to be part of the spec, and you may lose points if you ignore them.  Such posts will always be placed in the Announcements section of the course page in addition to the Q&amp;A page.  (We promise that no official clarifications will be posted within 24 hours of the due date.)




<h1>What to turn in</h1>




<strong>Note: You will need to complete the “Academic Dishonesty policy questionnaire,” found on the Homework page on Canvas, before the submission link will be visible to you. </strong>




Please submit, on Canvas, the zip file that is created by the SpecChecker. The file will be named

<strong>SUBMIT_THIS_hw1.zip</strong>. and it will be located in the directory you selected when you ran the

SpecChecker.  It should contain one directory, <strong>hw1</strong>, which in turn contains one file,

<strong>WirelessPrinter.java</strong>.  Please LOOK at the file you upload and make sure it is the right one!




Submit the zip file to Canvas using the Assignment 1 submission link and verify that your submission was successful.  If you are not sure how to do this, see the document “Assignment Submission HOWTO” which can be found in the Piazza pinned messages.




We recommend that you submit the zip file as created by the specchecker.  If necessary for some reason, you can create a zip file yourself.  The zip file must contain the directory <strong>hw1</strong>, which in turn should contain the file <strong>WirelessPrinter.java</strong>.  You can accomplish this by zipping up the <strong>src</strong> directory of your project.  The file must be a zip file, so be sure you are using the Windows or Mac zip utility, and NOT a third-party installation of WinRAR, 7-zip, or Winzip.<img decoding="async" data-recalc-dims="1" data-src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/02/116.png?w=980&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/www.ankitcodinghub.com/wp-content/uploads/2020/02/116.png?w=980&amp;ssl=1" data-recalc-dims="1">

 </noscript>