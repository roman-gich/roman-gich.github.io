---
layout: post
title:  "How to enable SEO friendly URLs in Yii2"
date:   2016-01-02 00:10:00 +0200
---
For doing this create a .htacess file within frontend/web/ of the application.

{% highlight apache %}
Options Includes FollowSymLinks
#hide index.php
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php
{% endhighlight %}

After that configure urlManager by adding this code into your config/main.php file.
{% highlight php %}<?php
    // 'components' => [
        'urlManager' => [
            'enablePrettyUrl' => true,
            'showScriptName' => false,
            'suffix' => '.html',
            'rules' => [
            // your rules go here
            ],
        // ...
        ],
    // ...
    
?>{% endhighlight %}