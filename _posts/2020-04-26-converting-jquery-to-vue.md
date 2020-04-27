# 대충 만든 jQuery 코드를 Vue로 이전하기 😎

학교에서 사용할 동아리 통합 지원 시스템을 제작하고 있다.

이 중 지원서를 작성하는 페이지가 jQuery로 만들어져 있는데 제대로 작동하지 않는다고 한다. 우엑,,

기존 소스를 그대로 사용하기는 어렵다고 판단하고 "The Progressive JavaScript Framework" 라는 Vue를 사용해보려고 한다.



## 개요

'동아리 통합 지원 시스템'은 학교의 각 동아리들을 손쉽게 지원할 수 있는 서비스다.

![image-20200427110228787](/Users/hyungju/Library/Application Support/typora-user-images/image-20200427110228787.png)



1,2,3 지망 동아리를 선택하면 API 서버에서 동아리에 대한 정보를 받아와 표시하는 '지원하기' 페이지로, 어떻게 보면 이 프로젝트에서 제일 중요한 부분 이라고 할 수 있겠다.

```js
$.get( "club/"+third, function( data ) { }
```

동아리를 선택하면 jQuery AJAX를 사용해서 동아리 정보를 받아온다.

```js
let question = JSON.parse(data)[1]
let settings = JSON.parse(data)[2]
let club_data = JSON.parse(data)[0];
```

그 후, 각종 정보를 불러와 

```js
$("#questions").append("     <div class=\"card questions\" data-question-uuid=\""+item.uuid+"\" data-club-shortname=\""+club_data.shortname+"\" >\n" +
    "                    <div class=\"card-body\">\n" +
    "                        <h1 class=\"page-title font-size-24 mb-1\">"+club_data.name+" 질문 "+(index+1)+"</h1>\n" +
    "                        <label for=\"exampleInputPassword1\">"+item.question+"</label>\n" +
    "                        <label class=\"count\">(현재 0자 / 최대 "+item.count+"자)</label>\n" +
    "                        <textarea class=\"form-control new-question\"  data-max-count=\""+item.count+"\" rows=\"10\"></textarea>\n" +
    "\n" +
    "                    </div>\n" +
    "                </div>")
```

데이터를 Append 하는 다소 간단한 구조다.

하지만 기능이 개발 도중에 추가되면서 중복 코드가 늘어나고, 더 이상 수정할 수 없는 코드가 되어버렸다.



앞서 이야기 했듯이 Vue는 점진적인 웹 프레임워크라고 한다.



무려 jQuery와 동일하게 CDN을 통해 Vue를 임포트해 사용할 수 도 있다.

이번 글에서는 해당 작업을 진행한 과정을 간략하게 적어보았다.

