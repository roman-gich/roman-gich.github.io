---
layout: post
title:  "How to find the number of days between two dates using PHP?"
date:   2016-01-01 23:15:00 +0200
---

Here is a simple way to find the number of days between two dates.

For doing this you should convert two dates into unix time format. Then calculate the difference to get the number of seconds.
And finally divide the received seconds by 86400 (seconds per day) to get the number of days.
{% highlight php %}<?php

$date1 = '2015-12-30';
$date2 = '2015-12-25';

$date1_unix = strtotime($date1);
$date2_unix = strtotime($date2);

$diff = abs($date2_unix - $date1_unix);
$number_of_days = $diff / 60 / 60 / 24;

printf('The number of days between two dates is %d', $number_of_days);

?>{% endhighlight %}
The above example will output:
<pre>The number of days is 5</pre>

Here is a short function:
{% highlight php %}<?php

function getNumberDays($date1, $date2) {
    return abs(strtotime($date2) - strtotime($date1)) / 86400;
}

?>{% endhighlight %}