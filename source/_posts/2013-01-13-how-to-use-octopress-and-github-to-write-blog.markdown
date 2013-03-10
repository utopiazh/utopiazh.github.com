---
layout: post
title: "How to use octopress and github to write blog"
date: 2013-01-13 15:30
comments: true
categories: tools 
---

Today spent about one hours to setup blogs on github, the main motivation is
to it's code friendly.

The setup steps are:
<h2> 1. Install Ruby With RVM </h2>
{% codeblock %}
curl -L https://get.rvm.io | bash -s stable --ruby
# Update .zshrc and add one more line:
source /etc/profile.d/rvm.sh
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
{% endcodeblock %}
<h2> 2. Setup Octopress </h2>
{% codeblock %}
cd ~/github/
git clone git://github.com/imathis/octopress.git utopiazh.github.com
cd ~/github/utopiazh.github.com
bundle update
rake install
{% endcodeblock %}
<h2> 3. Deploy as utopiazh.github.com </h2>
{% codeblock %}
git remote add utopiazh git@github.com:utopiazh/utopiazh.github.com.git
rake setup_github_pages
# creaete a test post
rake new_post["post title"]
rake generate
rake deploy
{% endcodeblock %}

<h2> 4. Commit the source </h2>
{% codeblock %}
git push -u utopiazh master
git add .
git commit -m 'your message'
git push origin source
{% endcodeblock %}

After setup, the publishing steps will be:
{% codeblock %}
rake new_post["post title"]
rake generate
rake deploy

git commit -a -m "new post"
git push origin source
{% endcodeblock %}

<strong>References:</strong><br/>
<ol>
<li>http://octopress.org/docs/setup/ </li>
<li>http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github</li>
<li>http://www.yangzhiping.com/tech/octopress.html</li>
</ol>



