---
title: Slides
layout: default
---
test site?
{% if jekyll.environment == "development" %}
   Development
{% endif %}

[link]({{ site.baseurl }}{% post_url 2017-06-16-welcome-to-jekyll %})

{% highlight ruby linenos %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

<ul>
	{% for slide in site.slides %}
		<li>{{ slide.content }}</li>
	{% endfor %}
</ul>

{% include hint.html content="This is a sample hint." %}
