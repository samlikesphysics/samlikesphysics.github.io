---
layout: full-width
title: Publications
# Note that this index page uses a full-width layout!
---
{% newthought Preprints %}
  <ul class="content-listing ">
    {% for pub in site.data.preprints %}      
        <li class="listing">
          <span class="smaller">
            {{pub.authors}}
            <b>{{pub.title}}.</b>
            <i>Submitted to {{pub.submitted}}.</i> {{pub.year}}.
            arxiv:<a href="https://arxiv.org/abs/{{pub.arxiv}}">{{pub.arxiv}}</a>
          </span>
        </li>
    {% endfor %}
  </ul>

  <hr class="slender">

{% newthought Published %}

  <ul class="content-listing ">
    {% for pub in site.data.pubs %}      
        <li class="listing">
            <span class="smaller">
                {{pub.authors}}
                <b>{{pub.title}}.</b>
                <i>{{pub.journal}}.</i> {{pub.year}}.
                DOI:<a href="https://doi.org/{{pub.doi}}">{{pub.doi}}</a>
            </span>
        </li>
    {% endfor %}
  </ul>