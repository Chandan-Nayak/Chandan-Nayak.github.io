---
layout: post_page
title: Blog using Jekyll and GitHub Pages
---

<h4>What is Jekyll -</h4>

Jekyll is a parsing engine bundled as a ruby gem used to build static websites from dynamic components such as templates, partials, liquid code, markdown, etc. Jekyll is known as "a simple, blog aware, static site generator". Jekyll takes away the complexity and configuration to allow you on the content - which matters most. For more info <a href="http://jekyllrb.com/docs/home/">http://jekyllrb.com/docs/home/</a>

<h4>Why Jekyll for Blog -</h4>

1. It is Static, So faster and lighter
2. More secure by avoiding dynamic front-end
3. No server-side language nor database
4. No heavy stack to manage
5. You do not need a heavy blogging editor, simple plain text editor,VIM or even terminal will do
6. Manage with git,github and you do not have to worry about SCM
7. Simplest deployment - change plain files > commit > push and you are done !!
<BR>
<h4>Configuration Steps -</h4>
<ol type="1">
	<li>
	Install Ruby on your machine - For Mac Ruby is already installed
	{% highlight ruby%}
	$ ruby -v
ruby 2.1.4p265 (2014-10-27 revision 48166) [x86_64-darwin12.0]
	{% endhighlight %}
	</li>

	<li>
	Go to your <a href="https://github.com">https://github.com/</a> and create a new repository named username.github.io
	</li>
	<li>
		Run these commands
	{% highlight ruby %}
$ git clone https://github.com/plusjade/jekyll-bootstrap.git username.github.io
$ cd username.github.io
	{% endhighlight %}
	</li>
	<li>
		If you want to change or check the content locally you will need to install jekelly gem
		{% highlight ruby%}
$ gem install jekyll
	{% endhighlight %}	
	</li>
		<li>
		Run these commands
	{% highlight ruby %}
$ cd username.github.io 
$ jekyll serve
	{% endhighlight %}
	</li>
	<li>
		After running jekyll serve you should be able to see your changes at <a href="http://localhost:4000">http://localhost:4000</a>
	</li>
	<li>
		If all looks good push the changes to github
	{% highlight ruby %}
$ git push origin master
	{% endhighlight %}
	</li>
</ol>

Your setup is done. Try to access <b><i>http://username.github.io/</i>
<BR>
<BR>	
<h4>Customizing Jekyll -</h4>
You can change jekyll themes which are supported. Coming up..