### **display 속성이란?**

- display 태그는 화면에 어떻게 드러나게 할지를 결정하는 속성이다.
- 사실 이렇게 들으면 감이 잘 안오는데 **요소 크기를 어떻게 결정할건가** 를 결정하는 속성이라고 이해하는게 조금 더 감이 잘 잡히는 것 같다

### **display 속성값의 종류**

### **예제 코드**

### **HTML**

```xml
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="./index.css" />
  </head>
  <body>
    <div class="none_div">I am none</div>
    <div class="block_div">I am block</div>
    <div class="inline_div">I am inline</div>
    <div class="inline-block_div">I am inline-block</div>
  </body>
</html>

```

### **CSS**

```css
body div {
  font-size: large;
  margin-bottom: 50px;
}

.none_div {
  display: none;
  background-color: blueviolet;
}

.block_div {
  display: block;
  background-color: aqua;
}

.inline_div {
  display: inline;
  width: 500px;
  background-color: chartreuse;
}

.inline-block_div {
  display: inline-block;
  width: 500px;
  background-color: gold;
}

```

**실행 결과**

![https://k.kakaocdn.net/dn/blGJKR/btrQQiu1BOZ/fE3dhrntQTNhrEZlGcpwVK/img.png](https://k.kakaocdn.net/dn/blGJKR/btrQQiu1BOZ/fE3dhrntQTNhrEZlGcpwVK/img.png)

**display: none**

- 화면에서 사라진다.
- 크기 자체도 차지하지 않는다.

**display: block**

- 일반적으로 설정하지 않아도 div가 갖게되는 기본값이다. (태그에 따라 기본값이 다를 수 있다.)
- 기본적으로 width 가 자신의 컨테이너의 100% 가 되게끔 한다. 쉽게 말하자면, **가로 한 줄을 다 차지하게 된다**.
- block은 height와 width 값을 지정 할 수 있다.
- block은 margin과 padding을 지정 할 수 있다.

**display: inline**

- 컨텐츠를 딱 감쌀정도의 크기만 갖게됩니다. block태그와 다르게 줄바꿈이 되지 않고, 반드시 컨텐츠를 감싸게 되고, **크기를 변화시킬 수 없습니다.**
- 예시 css에서도 width를 임의로 500px 로 바꾸어줬지만 크기는 여전히 글의 길이 만큼입니다. (width와 height를 명시 할 수 없다)
- margin과 padding 속성은 **좌우 간격만 반영**이 되고, **상하 간격은 반영**이 되지 않는다.

**display: inline-block**

- inline과 block의 특성을 합쳐놓은 속성이다. 기본적으로는 inline의 속성을 지니고 있지만, block 처럼 **width 와 height를 지정 할 수 있다.**
- 줄바꿈이 이루어지지 않는다.
- 만약 width와 height를 지정하지 않을 경우, inline과 같이 컨텐츠만큼 영역이 잡힌다.
- 참고로 Explorer 7 이하에서는 **사용할 수 없다.**


