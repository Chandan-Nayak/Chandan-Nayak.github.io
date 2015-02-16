---
layout: post_page
title: Blog using Jekyll and GitHub Pages
---

This was <b>The perfect sunday</b> watching India vs Pakistand and i was sitting infornt of the screen watching the match wondering if i could use this time to do something while watching the match. I had my newly purchased mac book pro on my lap which was tempting me to type some thing on terminal. I had this idea of starting a blog site of my own and i had already invested some time with blogger and wordpress and i was not convincted as i was searching for some simple way of just putting the text on the page which shall speak for itself not the design or the features. 

I was going through github explore feature and i landed up on a site which said username.github.io and it was a blog, i started searching more on this and i could finish setting up my blogging site using jkelly and githubpages by the time the match was over. I was happy because i was able to create and edit posts from my termianl. To add to the perfect sunday India won the match. I thought to write this post because my frined wanted to know how to get this stuff done ..

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