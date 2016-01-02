---
layout: post
title:  "How to generate a random password in PHP?"
excerpt: "Generating a random password in php. Types of characters alternate with each other - maybe it'll be helpful for someone..."
date:   2016-01-02 22:00:00 +0200
---
Here is one more function for generating a random  password in php. It allows to specify which characters are allowed and also the length of the password. Types of characters alternate with each other - maybe it'll be helpful for someone.

{% highlight php %}<?php

function generatePassword($digital, $upper, $lower, $special, $length) {
    $password = '';
    $characters = [];
    if ($digital) {
        $characters[] = range(0, 9);
    }
    if ($upper) {
        $characters[] = range('A', 'Z');
    }
    if ($lower) {
        $characters[] = range('a', 'z');
    }
    if ($special) {
        $characters[] = ['%', '*', '?', '@', '#', '$', '~'];
    }
    $j = count($characters);
    for ($i = 0; $i < $length; $i++) {
        $n = $i%$j;
        $password .= $characters[$n][rand(1, count($characters[$n]) - 1)];
    }
    return $password;
}

echo generatePassword(true, true, false, false, 6) . "\n";
echo generatePassword(true, true, true, false, 8) . "\n";
echo generatePassword(true, true, true, true, 10);

?>{% endhighlight %}

The above example will output something similar to:
<pre>
4Y9T9V
8Cf2Vf8R
5Lz~6Xt*5Q
</pre>