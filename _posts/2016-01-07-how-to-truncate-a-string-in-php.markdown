---
layout: post
title:  "Truncation of a string to first N words or to a specified length in PHP?"
excerpt: "A simple function that truncates a string to first N words or to a specified length and adds an ellipsis using PHP"
date:   2016-01-07 18:00:00 +0200
---
Below is a simple example how to truncate a string to first N words or to a specified length using PHP.
The function allows to specify the maximum length of the text and also the maximum number of words.

Don't forget that strlen() returns the number of bytes rather than the number of characters in a string. 
So be careful if you use an encoding other than UTF-8 or a different alphabet.

{% highlight php %}<?php

/**
 * The function truncates a string and adds an ellipsis
 * @param   string      $str
 * @param   integer     $maxlength  
 * @param   integer     $maxwords   
 * @return  string
 */
function truncateText($str, $maxlength = 150, $maxwords = 25)  {
    $ellipsis = false;
    if (str_word_count($str, 0) > $maxwords) { 
        $words = str_word_count($str, 2);
        $pos = array_keys($words);
        $str = substr($str, 0, $pos[$maxwords]);
        $ellipsis = true;
    }
    if (strlen($str) > $maxlength) {
        $str = substr($str, 0, $maxlength);
        $str = substr($str, 0, strrpos($str, ' '));
        $ellipsis = true;
    }
    if ($ellipsis) {
        $str = trim($str, ';,. ') . '...';
    }
    return $str;
}

$str = 'Lorem ipsum dolor sit amet, consectetuer adipiscing elit.';
echo truncateText($str, 30, 5);
?>{% endhighlight %}


The above example will output:
<pre>
Lorem ipsum dolor sit amet...
</pre>