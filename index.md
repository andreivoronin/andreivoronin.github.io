---
layout: default
---

<section class="container-md d-flex p-3 f4">

  <a href="{{ site.about.page }}" class="col-3 col-md-2 mr-3 mr-md-4 hover-grow">
    <img src="img/-cover.jpg"
      alt="{{ site.name }} photo"
      class="circle width-fit"
      width="{{ site.image.width }}"
    />
  </a>

  <div class="col-9 col-md-10">
    <h1 class="h1 lh-condensed">
      {{ site.about.line_1 }}
      <br class="hide-xl"/>
      {{ site.about.line_2 }}
    </h1>
    <p class="hide-sm">
      {{ site.about.line_3 }}
      <br/>
      {{ site.about.line_4 }}
    </p>
    
    {% if site.twitter %}
      <div class="mt-3">
        <a href="https://twitter.com/intent/follow?screen_name={{ site.twitter.username }}" target="_blank"
          class="mr-3">Follow @{{ site.twitter.username }}</a>

        {% if site.twitter.followers %}
          <span class="text-gray">{{ site.twitter.followers }}&nbsp;followers</span>
        {% endif %}
      </div>
    {% endif %}

  </div>

</section>

<div class="container-md p-3">

  {% for post in site.posts %}

    {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
    {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}

    {% if forloop.first %}
      <section class="mb-5">
        <h3 id="{{ this_year }}">{{this_year}}</h3>
        <div>
    {% endif %}

          <article class="d-flex my-2">
            {% assign image_path = '/img' | append: post.id | append: '/-cover.jpg' %}
            {% assign has_img = false %}

            <a href="{{ post.url }}" class="col-3 col-md-2 d-inline-flex flex-justify-center flex-items-center
                overflow-hidden text-uppercase no-underline f00-light text-gray-light bg-gray mr-3 mr-md-4 hover-grow"
              title="{{ post.subtitle }}"
              {% if forloop.first %}
                  autofocus
              {% endif %}
            >
              {% for static_file in site.static_files %}
                {% if static_file.path == image_path %}
                  {% assign has_img = true %}
                  <img src="{{ image_path }}" width="{{ site.image.width }}" class="width-fit" alt="{{ post.title | escape }}"/>
                {% endif %}
              {% endfor %}

              {% if has_img == false %}
                {{ post.title | slice: 0, 2 }}
              {% endif %}
            </a>

            <div class="col-9 col-md-10">
              <h2 class="h3 text-normal">
                <a href="{{ post.url }}"
                  tabindex="-1"
                  class="link-gray-dark mr-2 py-1 {% if post.favorite %}bg-yellow-light{% endif %}"
                  title="{{ post.subtitle }}"
                >{{ post.title }}</a><time
                  datetime="{{ post.date | date_to_xmlschema }}"
                  itemprop="datePublished"
                  title="{{ post.date | date_to_long_string }}"
                  class="text-small text-gray"
                >{{ post.date | date: "%-m/%-d" }}
                </time>
              </h2>
            </div>
          </article>

    {% if forloop.last %}
        </div>
      </section>
    {% elsif this_year != next_year %}
        </div>
      </section>

      <section class="mb-5">
        <h3 id="{{ next_year }}">{{next_year}}</h3>
        <div>
    {% endif %}

  {% endfor %}

</div>
