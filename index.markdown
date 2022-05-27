---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Parson's Problems for practice
---
<script>
function student_code(parsonsPuzzle) {
    var code_list = parsonsPuzzle.normalizeIndents(parsonsPuzzle.getModifiedCode("#ul-" + parsonsPuzzle.options.sortableId));
    var code_str = '';
    for (i = 0; i < code_list.length; i++) {
        code_str += ("\n" + code_list[i].code);
    }
    return code_str;
}

function giveFeedback(parsonsPuzzle, feedback_id) {
    if (parsonsPuzzle) {
      var feedback = parsonsPuzzle.getFeedback();

      var message = feedback.html || feedback.feedback;
      if (!message && feedback.length) {
        message = feedback.join('\n')
      }
      message = message && !feedback.success ? message : "Congratulations on solving your Parsons Problem!" + student_code(parsonsPuzzle);

      var feedbackContainer = document.getElementById(feedback_id);
      feedbackContainer.innerHTML = message;
    }
  }
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
    "    answer = 0\\nmin_so_far = None\n" +
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
  var initial = "def odd_even(nums):\n" +
    "    expecting_odd = True\n" +
    "    for num in nums:\n" +
    "        if expecting_odd != (num % 2 == 1):\n" +
    "            return False\n" +
    "        expecting_odd = not expecting_odd\n" +
    "    return True\n" +
    "if expecting_odd and (num % 2 == 0): #distractor\n" +
    "if not expecting_odd and (num % 2 == 1): #distractor\n" +
    "return True #distractor\n" +
    "return False #distractor";
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

## Problem 4: Sum of natural numbers
Define a function `sum_natural` that returns the sum of all natural numbers (non-negative integers) in a sequence `items`. Note that `items` may contain integers as well as non-integers.

*Examples*:
```
>>> sum_natural([1, 3, 1])
5
>>> sum_natural((1, 2.5))
1
>>> sum_natural([None])
0
```

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
  var initial = "def sum_natural(items):\n" +
    "    answer = 0\n" +
    "    for item in items:\n" +
    "        if isinstance(item, int) and item &gt; 0:\n" +
    "            answer += item\n" +
    "    return answer\n" +
    "if item &gt; 0: #distractor\n" +
    "if isinstance(item, int): #distractor";
  var parsonsPuzzle = new ParsonsWidget({
    "sortableId": "p04-sortable",
    "max_wrong_lines": 10,
    "grader": ParsonsWidget._graders.UnitTestGrader,
    "exec_limit": 2500,
    "can_indent": true,
    "x_indent": 50,
    "lang": "en",
    "show_feedback": true,
    "trashId": "p04-sortableTrash",
    "unittests": "import unittestparson\nclass myTests(unittestparson.unittest):\n  def test_0(self):\n    self.assertEqual(sum_natural(['a', 1.2, -1]),0,\"Testing: ['a', 1.2, -1]\")\n  def test_1(self):\n    self.assertEqual(sum_natural(['a', 1.2, 1]),1,\"Testing: ['a', 1.2, 1]\")\n  def test_2(self):\n    self.assertEqual(sum_natural(['a', 12, -1]),12,\"Testing: ['a', 12, -1]\")\n  def test_3(self):\n    self.assertEqual(sum_natural([0, 1.2, -1]),0,\"Testing: [0, 1.2, -1]\")\n_test_result = myTests().main()"
  });
  parsonsPuzzle.init(initial);
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
