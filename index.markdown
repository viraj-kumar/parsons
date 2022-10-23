---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Parson's Problems for practice
---
<script type="text/javascript">
const TAB_SPACES = 4;
const SUBGOAL_MARKER = "##";
function success_message(parsonsPuzzle) {
    var code_list = parsonsPuzzle.getModifiedCode("#ul-" + parsonsPuzzle.options.sortableId);
    var html_str = "Your solution to this Parsons Problem is correct!<br><code>";
    for (i = 0; i < code_list.length; i++) {
        var html_pre = "<br>";
        var code_pre = "\n";
        if (code_list[i].indent > 0) {
            html_pre += "\xa0".repeat(code_list[i].indent * TAB_SPACES);
        }
        html_str += (html_pre + code_list[i].code);
    }
    html_str += "<br></code>";
    return html_str;
}

function giveFeedback(parsonsPuzzle, feedback_id) {
    if (parsonsPuzzle) {
      var feedback = parsonsPuzzle.getFeedback();

      var message = feedback.html || feedback.feedback;
      if (!message && feedback.length) {
        message = feedback.join('\n')
      }
      message = message && !feedback.success ? message : success_message(parsonsPuzzle);

      var feedbackContainer = document.getElementById(feedback_id);
      feedbackContainer.innerHTML = message;
    }
  }

function commentsFirst(code) {
    var n = code.length;
    var commentIDs = [];
    var codeIDs = [];
    for (i = 0; i < n; i++) {
        var tr = code[i].trim();
        if (tr.startsWith(SUBGOAL_MARKER)) {
            commentIDs.push(i);
        } else {
            codeIDs.push(i);
        }
    }
    n = codeIDs.length;
    var swap1, swap2, tmp;
    for (i = 0; i < n; i++) {
       swap1 = Math.floor(Math.random() * n);
       swap2 = Math.floor(Math.random() * n);
       tmp = codeIDs[swap1];
       codeIDs[swap1] = codeIDs[swap2];
       codeIDs[swap2] = tmp;
    }
    for (i = 0; i < n; i++) {
        commentIDs.push(codeIDs[i]);
    }
    return commentIDs;
}
</script>

## Problem 1: Modify this function
The following function has one argument: a list `xs`. The function is *supposed* to sum up all the integers in `xs`, but it presently sums up *all* items in `xs`. Re-arrange the blocks below so that the function calculates the sum correctly.

```
def sum_ints(xs):
    result = 0
    for x in xs:
        result += x
    return result
```
<div id="p01-sortableTrash" class="sortable-code"></div> 
<div id="p01-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p01-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p01-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p01-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def sum_ints(xs):\n" +
    "    result = 0\n" +
    "    for x in xs:\n" +
    "        if type(x) == int:\n" +
    "            result += x\n" +
    "    return result\n" +
    "if isinstance(x, int): #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p01-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p01-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p01-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p01-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p01-feedback"); 
  }); 
})(); 
</script>

## Problem 2: Further modify the above function
Further modify the above function so that it returns the sum of all *positive* integers in the list `xs`.

<div id="p02-sortableTrash" class="sortable-code"></div> 
<div id="p02-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p02-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p02-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p02-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def sum_positive_ints(xs):\n" +
    "    result = 0\n" +
    "    for x in xs:\n" +
    "        if type(x) == int and x &gt; 0:\n" +
    "            result += x\n" +
    "    return result\n" +
    "if x &gt; 0 and type(x) == int: #distractor\n" +
    "if type(x) == int or x &gt; 0: #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p02-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p02-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p02-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p02-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p02-feedback"); 
  }); 
})(); 
</script>

## Problem 3: Mostly positive
The following function has one argument: a list `xs` of integers (positive, negative, or zero). The function should return `True` if the most freuqent type of integers in the list are *positive*. Otherwise, it should return `False`. Re-arrange the blocks of code to create such a function.

<div id="p03-sortableTrash" class="sortable-code"></div> 
<div id="p03-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p03-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p03-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p03-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def mostly_positive(xs):\n" +
    "    p_count = 0; n_count = 0; z_count = 0\n" +
    "    for x in xs:\n" +
    "        if x &gt; 0:\n" +
    "            p_count += 1\n" +
    "        elif x &lt; 0:\n" +
    "            n_count += 1\n" +
    "        else:\n" +
    "            z_count += 1\n" +
    "    return p_count &gt; max(n_count, z_count)\n" +
    "return True #distractor\n" +
    "return False #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p03-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p03-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p03-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p03-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p03-feedback"); 
  }); 
})(); 
</script>
    
## Problem 4: Counting substrings
The following function has two arguments: a list of strings `xs` and a string `s`. Re-arrange these blocks so that the function returns the number of strings in `xs` that contain `s` as a substring.

<div id="p04-sortableTrash" class="sortable-code"></div> 
<div id="p04-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p04-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p04-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p04-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def count_substrings(xs, s):\n" +
    "    result = 0\n" +
    "    for x in xs:\n" +
    "        if s in x:\n" +
    "            result += 1\n" +
    "    return result\n" +
    "for x in s: #distractor\n" +
    "if x in s: #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p04-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p04-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p04-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p04-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p04-feedback"); 
  }); 
})(); 
</script>


<!---
## Simple Parsons Problem: A typical day for a student/teacher
Re-arrange the blocks below to construct a typical day in the life of a student/teacher.
    
<div id="p01-sortableTrash" class="sortable-code"></div> 
<div id="p01-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p01-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p01-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p01-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "Wake up\n" +
    "Get ready\n" +
    "Go to campus\n" +
    "Come home\n" +
    "Go to sleep";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p01-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p01-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p01-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p01-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p01-feedback"); 
  }); 
})(); 
</script>

## Parsons Problem with distractors:
Re-arrange the blocks below to describe how a faculty member might interact with students after evaluating their Midterm Exams.

<div id="p02-sortableTrash" class="sortable-code"></div> 
<div id="p02-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p02-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p02-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p02-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "If score is less than 40:\n" +
    "    Email student: &quot;Let us meet for a personal discussion&quot;\n" +
    "Otherwise, if score is less than 60:\n" +
    "    Email student: &quot;I urge you to join the help session&quot;\n" +
    "Otherwise, if score is less than 80:\n" +
    "    Email student: &quot;You are welcome to join the help session&quot;\n" +
    "Otherwise:\n" +
    "    Email student: &quot;Keep up the good work&quot;\n" +
    "Email student to say &quot;You failed&quot; #distractor\n" +
    "Skip this student #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p02-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p02-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p02-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p02-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p02-feedback"); 
  }); 
})(); 
</script>

## Problem 1: Right-angled triangle
Re-arrange the blocks below so that the program reads an integer `n` and prints a right-angled triangle of height `n`.

*Example*: If `n = 4`, the program should print:
```
*
**
***
****
```
<div id="p01-sortableTrash" class="sortable-code"></div> 
<div id="p01-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p01-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p01-newInstanceLink" value="Reset Problem" type="button" /> 
</p>
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p01-feedback"/></fieldset>
<script type="text/javascript">
(function(){
  var initial = "n = int(input())\n" +
    "for i in range(n):\n" +
    "	print(&#039;*&#039; * (i+1))\n" +
    "n = input() #distractor\n" +
    "for i in range(1, n): #distractor\n" +
    "	print(&#039;*&#039; * i) #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p01-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p01-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p01-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p01-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, 'p01-feedback'); 
  }); 
})();
</script>

## Problem 2: Number of times minimum appears
Define a function `num_min` with one argument `nums` (a sequence of numbers) which returns the *frequency* of the minimum value in `nums`.

*Examples*:
```
>>> num_min([1, 3, 1])
2
>>> num_min((1, 2))
1
>>> num_min([])
0
```
<div id="p02-sortableTrash" class="sortable-code"></div> 
<div id="p02-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p02-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p02-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p02-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def num_min(nums):\n" +
    "    answer = 0; min_so_far = None\n" +
    "    for num in nums:\n" +
    "        if min_so_far == None or num &lt; min_so_far:\n" +
    "            answer = 1\n" +
    "            min_so_far = num\n" +
    "        elif num == min_so_far:\n" +
    "            answer += 1\n" +
    "    return answer\n" +
    "min_so_far = 0 #distractor\n" +
    "min_so_far = -1 #distractor\n" +
    "if num &lt; min_so_far: #distractor\n" +
    "else: #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p02-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p02-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.shuffleLines();
  $("#p02-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#p02-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "p02-feedback"); 
  }); 
})(); 
</script>

## Problem 3: Alternating odd-even numbers
Define a function `odd_even` that returns `True` if the integers in the sequence `nums` alternate in the pattern: odd, even, odd, even, etc.

*Examples*:
```
>>> odd_even([1, 3, 1])
False
>>> odd_even((1, 2, 3))
True
>>> odd_even([])
True
```

<div id="p03-sortableTrash" class="sortable-code"></div> 
<div id="p03-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="p03-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="p03-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="p03-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "## Function header\n" +
    "def odd_even(nums):\n" +
    "    ## Initially expecting odd\n" +
    "    expecting_odd = True\n" +
    "    ## For each number in nums...\n" +
    "    for num in nums:\n" +
    "        ## ...if it is not as expected, fail\n" +
    "        if expecting_odd != (num % 2 == 1):\n" +
    "            return False\n" +
    "        ## Update expectation\n" +
    "        expecting_odd = not expecting_odd\n" +
    "    ## Succeed if all numbers are as expected\n" +
    "    return True\n" +
    "if expecting_odd and (num % 2 == 0): #distractor\n" +
    "if not expecting_odd and (num % 2 == 1): #distractor\n" +
    "return False #distractor\n" +
    "return True #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p03-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.UnitTestGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p03-sortableTrash",
    "unittests": "import unittestparson\nclass myTests(unittestparson.unittest):\n  def test_0(self):\n    self.assertEqual(odd_even([1, 3, 1]),False,'Testing: [1, 3, 1]')\n  def test_1(self):\n    self.assertEqual(odd_even((1, 2, 3)),True,'Testing: (1, 2, 3)')\n  def test_2(self):\n    self.assertEqual(odd_even([]),True,'Testing: []')\n_test_result = myTests().main()"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#p03-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  });
  $("#p03-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, 'p03-feedback'); 
  }); 
})(); 
</script>

### Examples created by Faculty (BITES FDP, 18 June 2022)
Define a function sum_natural that returns the sum of all natural numbers (non-negative integers) in a sequence items. Note that items may contain integers as well as non-integers.

<div id="tej123-sortableTrash" class="sortable-code"></div> 
<div id="tej123-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="tej123-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="tej123-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="tej123-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def sum_natural(items):\n" +
    "    answer = 0\n" +
    "    for item in items:\n" +
    "        if isinstance(item, int) and item &gt; 0:\n" +
    "            answer += item\n" +
    "    return answer";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "tej123-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "tej123-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#tej123-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#tej123-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "tej123-feedback"); 
  }); 
})(); 
</script>

Write a program to add 2 numbers
<div id="gl-sortableTrash" class="sortable-code"></div> 
<div id="gl-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="gl-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="gl-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="gl-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "#sum of 2 nos\n" +
    "	num1 = 1.5\n" +
    "	num2 = 6.3\n" +
    "	sum = num1 + num2\n" +
    "		print(&#039;The sum of {0} and {1} is {2}&#039;.format(num1, num2, sum))\n" +
    "else #distractor\n" +
    "sum = num1 - num2 #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "gl-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "gl-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#gl-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#gl-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "gl-feedback"); 
  }); 
})(); 
</script>
    
To add N natural number
<div id="KJ123-sortableTrash" class="sortable-code"></div> 
<div id="KJ123-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="KJ123-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="KJ123-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="KJ123-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def nat_num(num):\n" +
    "	answer=0\n" +
    "    for num in nums:\n" +
    "    	answer += num\n" +
    "    return answer\n" +
    "if num&lt;=2 #distractor\n" +
    "else: #distractor\n" +
    "answer = num #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "KJ123-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "KJ123-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#KJ123-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#KJ123-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "KJ123-feedback"); 
  }); 
})(); 
</script>
    
write a function to find the gcd of two numbers
<div id="nsk123-sortableTrash" class="sortable-code"></div> 
<div id="nsk123-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="nsk123-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="nsk123-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="nsk123-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def gcd(m, n) :\n" +
    "   while m != n :\n" +
    "       if m &gt; n :\n" +
    "          m -= n\n" +
    "       else: \n" +
    "          n -=m \n" +
    "   return m       ";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "nsk123-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "nsk123-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#nsk123-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#nsk123-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "nsk123-feedback"); 
  }); 
})(); 
</script>

Write a function to return the count of odd and even numbers in a list.
<div id="mr128-sortableTrash" class="sortable-code"></div> 
<div id="mr128-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="mr128-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="mr128-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="mr128-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def even_count(nums):\n" +
    "	even = 0\n" +
    "	odd = 0\n" +
    "	for num in nums:\n" +
    "		if num%2==0:\n" +
    "			even+=1\n" +
    "		else:\n" +
    "			odd+=1\n" +
    "	return even,odd";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "mr128-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.LineBasedGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "mr128-sortableTrash"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#mr128-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#mr128-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "mr128-feedback"); 
  }); 
})(); 
</script>
    
Calculate factorial of n
<div id="fact-sortableTrash" class="sortable-code"></div> 
<div id="fact-sortable" class="sortable-code"></div> 
<div style="clear:both;"></div> 
<p> 
    <input id="fact-feedbackLink" value="Get Feedback" type="button" /> 
    <input id="fact-newInstanceLink" value="Reset Problem" type="button" /> 
</p> 
<fieldset class="feedbackFieldset"><legend>Feedback:</legend><div id="fact-feedback"/></fieldset> 
<script type="text/javascript"> 
(function(){
  var initial = "def factorial(n):\n" +
    "    if n &lt; 0:\n" +
    "        return None\n" +
    "    elif n == 0:\n" +
    "        return 1\n" +
    "    return n * factorial(n-1)\n" +
    "ans = 1 #distractor\n" +
    "ans *= i #distractor\n" +
    "for i in range(1, n+1): #distractor\n" +
    "return ans #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "fact-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.UnitTestGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "fact-sortableTrash",
    "unittests": "import unittestparson\nclass myTests(unittestparson.unittest):\n  def test_0(self):\n    self.assertEqual(factorial(3),6,)\n  def test_1(self):\n    self.assertEqual(factorial(-3),None,)\n  def test_2(self):\n    self.assertEqual(factorial(0),1,)\n_test_result = myTests().main()"
  });
  parsonsPuzzle.init(initial);
  parsonsPuzzle.options.permutation = function(n) {
    return commentsFirst(initial.split("\n"));
  };
  parsonsPuzzle.shuffleLines();
  $("#fact-newInstanceLink").click(function(event){ 
      event.preventDefault(); 
      parsonsPuzzle.shuffleLines(); 
  }); 
  $("#fact-feedbackLink").click(function(event){ 
      event.preventDefault(); 
      giveFeedback(parsonsPuzzle, "fact-feedback"); 
  }); 
})(); 
</script>
-->
