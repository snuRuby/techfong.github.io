# [Start Bootstrap - Clean Blog](https://startbootstrap.com/template-overviews/clean-blog/) - Official Jekyll Version 을 사용한 스마트 스터디 기술 블로그



## Preview

[![Preview](https://s3-ap-northeast-1.amazonaws.com/smartstudy.io/blog/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2019-01-09+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+7.12.33.png)](http://blackrockdigital.github.io/startbootstrap-clean-blog-jekyll/)


Build your site: `bundle exec jekyll serve`

**[jekyll 설정 및 기본 용어들](https://jekyllrb-ko.github.io/docs/configuration/)**

##포스트하는 법
1. _posts 폴더에 YYYY-MM-DD-title.markdown 형식으로 포스트할 문서를 만든다.
2. 아래와 같이 처음에 설명을 넣는다. 
{% highlight ruby %}
---
layout: post
title:  "알렉사 스킬을 만들면서 느낀 점"
date:   2019-01-09 18:39:35 +0900
category: "개발 경험" #카테고리로 구분 가능
author: Totoro #글쓴이로 변경
published: True
---
{% endhighlight %}

date포맷은 위와 같이 맞추고, published로 post list에 게시글 보여주는 것을 조절할 수 있다. 
