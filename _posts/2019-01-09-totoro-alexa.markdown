---
layout: post
title:  "알렉사 스킬을 만들면서 느낀 점"
date:   2019-01-10 14:55:00 +0900
category: "개발 경험"
author: Totoro
published: True
---

인턴을 한지 4개월차. 알렉사 스킬을 2 종류 만들면서 느낀 점을 말해보려고 한다. 

### Dino Buddy Lab  
인턴 1개월이 채 되지 않았을 무렵 알렉사 스킬 dino buddy에 대한 업무를 받았다. 유아용 AI게임을 만드는 것이었다. 이미 앞의 개발자 분께서 코드 뼈대를 짜놓은 상태였고, 음원과 함께 게임 진행과 추가적인 intent작업을 해야 했다.

알렉사 스킬은 ask-sdk를 사용했다. ask-sdk란 json으로 request/response 주고 받는 것을 좀 더 쉽게 코딩할 수 있도록 아마존에서 만든 api이다. <br>
[ask-sdk 공식문서 구경하기][ask-sdk] 

---

<img src="https://s3-ap-northeast-1.amazonaws.com/smartstudy.io/blog/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA+2019-01-11+%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE+3.50.17.png" width="100%" />  

게임의 로직은 위와 같았다. 질문을 하고 답을 하면 가지를 쳐서 계속 질문하고 결국 정답을 하나 내는 퀴즈의 로직이다. 이 로직 사이에 사용자가 질문을 하거나 도움을 요청하면 인텐트로 받아서 반응한 뒤 질문으로 돌아가야 했다.

처음에는 음원을 아마존 Audio Player 로 플레이시켜 좋은 음질로 진행하고자 했다.(음원 품질이 뛰어났음) 근데 Audio Player로 돌리자마자 잘 돌아가던 로직이 삐그덕대기 시작했다. session attributes를 사용해서 값을 저장해 진행했었는데 전혀 작동하지 않았다. 다음 문제로 넘어가지 않아서 삽질을 하다가 persistent attributes를 사용했더니 그나마 작동하기 시작했다. 그러나 audio player자체가 prompting을 하지 못하는 것이 또다시 문제가 됐다. player가 음원을 튼 다음 질문을 하려고 하면 audioplayer intent 목록의 intent를 작동시키고 에러를 낸 다음 물어봐야 다른 인텐트를 인식했다(audioplayer intent만 인식). 또 삽질이 시작되었다. ask-sdk python버전에 대한 자료가 잘 나오지 않아서, 알렉사팀에 직접 물어보기로 하고 [amazon developer forum][develop]에 게시글을 올리고 메일을 보내서 물어봤다. 답변으로 알렉사는 audioplayer를 쓰면 세션이 닫히며, 세션을 열어놓은 상태에서 진행하길 바라고 음원이 그렇게 길지 않다면 ssml을 사용하여 플레이하라는 답변을 받았다. ('세션을 닫지 않는 방법은 없다'라는 답변을 원한게 아니였는데..)

그러면 새로운 마음으로 다시 ssml을 사용하여 만들기로 했다. 먼저, 음원을 ffmpeg을 사용해 Alexa ssml에 맞는 포맷으로 변경했다. 
{% highlight python %}
#terminal에서 ffmpeg으로 포맷 변경하기
ffmpeg -y -i input.mp3 -ar 44100 -ab 48k -codec:a mpeg2 -ac 1 output.mp3
{% endhighlight %} 
(변경 전 음악파일)
(변경 후 음악파일)
변경 후 알렉사로 한 번 틀어봤는데, 알렉사 스피커가 그렇게 좋지 않아서인지 큰 차이가 나지 않았다. 안심하며 전체 게임에 음원을 붙이기 시작했다. 


람다 자동화

[ask-sdk]: https://github.com/alexa/alexa-skills-kit-sdk-for-nodejs
[develop]: https://forums.developer.amazon.com/topics/alexa+skills+kit.html