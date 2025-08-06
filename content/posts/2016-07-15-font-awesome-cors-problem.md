+++
author = "yulistic"
date = "2016-07-15T12:11:14+09:00"
description = "Font-awesome icons are not shown correctly when the page is hosted by the GitLab page."
draft = false
tags = ["font-awesome", "CORS", "cross-origin resource sharing", "GitLab page"]
title = "Font-awesome CORS problem"
topics = ["issues"]
type = "post"
+++

# Problem
Font-awesome icons were not displayed correctly when the website was hosted on GitLab page.

[![Abnormal font-awesome icons](/img/fa_cors_problem.png "Abnormal font-awesome icons")](/img/fa_cors_problem.png)
*Abnormal font-awesome icons*

You can figure out the reason of the problem with the console of your browser. The above figure is an example screenshot of my Chrome browser.

The symptom was that the fa(font-awesome) icons were successfully loaded under the `https` connection, but it were not in the `http` connection.

If you are hosting your web site with your machine, the problem can be resolved easily by configuring your web server application such as Nginx or Apache.
But, in my case, the site was hosted on the GitLab page server.
To change the configuration options of the web service application hosted by GitLab page, it is required to set a new custom GitLab runner which is quite tiresome.

Continuously using `Shared Runner` of GitLab (no custom runner), I decided to **redirect all the `http` addresses to `https`**. It could be implemented in few lines of javascript code.

## Solution
I was using HUGO SSG(Static Site Generator) with Hyde-Y theme.

1. Find out the position of `<head>` part of your html code (It is usually `index.html` in the SSG case).
The position might be different according to the implementation of your theme.

2. Insert following snippet of code to the `<head>` part of your html code.

```html
  <script type="text/javascript">
  var loc = window.location.href+'';
  if (window.location.hostname!='localhost' && loc.indexOf('http://')==0){
      window.location.href = loc.replace('http://','https://');
	  }
  </script>

```

The code inserted will check the address and redirect the site to the same url with `https`. It does not redirect when the requested url is `localhost`.

Good luck.
