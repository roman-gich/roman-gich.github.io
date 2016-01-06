---
layout: post
title:  "How to generate a random password in PHP?"
excerpt: "Generating a random password in php. Types of characters alternate with each other - maybe it'll be helpful for someone..."
date:   2016-01-02 22:00:00 +0200
---
Here is one more function for generating a random  password in php. It allows to specify which characters are allowed and also the length of the password. Types of characters can alternate with each other - maybe it'll be helpful for someone.

{% highlight php %}<?php

/**
 * Password generator
 * @param   boolean    $digits      use digits
 * @param   boolean    $upper       use uppercase letters
 * @param   boolean    $lower       use lowercase letters
 * @param   boolean    $special     use special characters
 * @param   boolean    $random      specifies whether types of characters alternate with each other or not
 * @param   integer    $length      password length
 * @return  string
 */
function generatePassword($digits, $upper, $lower, $special, $random, $length) {
    $password = '';
    $characters = [];
    if ($digits) {
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
        $n = $random ? rand(0, count($characters) -1) : $i%$j;
        $password .= $characters[$n][rand(1, count($characters[$n]) - 1)];
    }
    return $password;
}

echo generatePassword(true, true, false, false, true, 8) . "\n";
echo generatePassword(true, true, true, false, true, 8) . "\n";
echo generatePassword(true, true, true, true, true, 10);
echo generatePassword(true, true, true, true, false, 10);

?>{% endhighlight %}

The above example will output something similar to:
<pre>
27V52E8F
RgEjHjeX
Yz*EJQ9#t?
8Vq?1Lq~5F
</pre>