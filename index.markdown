---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Parson's Problems for practice
---
## Problem 1: Right-angled triangle
Re-arrange the blocks below so that the program reads an integer `n` and prints a right-angled triangle of height `n`.

*Example*: If `n = 4`, the program should print:
```
*
**
***
****
```
<script>
function mygetFeedback(parsonsPuzzle, feedback_id) {
    if (parsonsPuzzle) {
      var feedback = parsonsPuzzle.getFeedback();

      var message = feedback.html || feedback.feedback;
      if (!message && feedback.length) {
        message = feedback.join('\n')
      }
      message = message && !feedback.success ? message : 'Congratulations on solving your Parsons Problem!';

      var feedbackContainer = document.getElementById(feedback_id);
      feedbackContainer.innerHTML = message;
    }
  }
</script>

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
      mygetFeedback(parsonsPuzzle, 'p01-feedback'); 
  }); 
})();
</script>

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
    "    answer = 0\n" +
    "    min_so_far = None\n" +
    "    for num in nums:\n" +
    "        if min_so_far == None or num &lt; min_so_far:\n" +
    "            answer = 1\n" +
    "            min_so_far = num\n" +
    "        elif num == min_so_far:\n" +
    "            answer += 1\n" +
    "    return answer\n" +
    "min_so_far = 0 #distractor\n" +
    "min_so_far = -1 #distractor\n" +
    "answer = 0 #distractor\n" +
    "if num &lt; min_so_far: #distractor\n" +
    "if num &lt; min_so_far or min_so_far == None: #distractor\n" +
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
      mygetFeedback(parsonsPuzzle, 'p02-feedback');
  }); 
})(); 
</script>
