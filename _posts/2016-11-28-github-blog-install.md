---
layout: post
title: Github에 hexo와 hueman 테마를 사용한 블로그 만들기(맥 환경)
date: 2016-11-28 12:03:31
toc: true
category: 컴퓨터
tags: [Github, hexo, hueman theme]
thumbnail: 
---


![](https://help.github.com/assets/images/site/set-up-git.gif)



github에 hexo와 hueman 테마를 사용해서 블로그를 만들었습니다. 그런데 설치해야할 프로그램과 플러그인이 다양하고 수정해야 할 내용들이 생각보다 여러가지가 있었습니다. 만약에 어떤 사고로 이 환경이 사라지고 나면 다시 복구하는데 무척 어려움이 있을 것이라는 생각이 들어서 기록해 놓습니다. 혹시라도 다른 분들께 참고가 된다면 그것도 좋은 일일 것 같습니다.

## 설치하기

### Setup Ruby On Rails on Mac OS X 10.11 El Capitan


루비를 설치하기 위해 먼저 Homebrew를 설치합니다.

terminal에서

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

이제 brew를 이용해서 Ruby를 설치합니다. 터미널에서 순서대로 입력합니다.

```
$ brew install rbenv ruby-build
```

```
$ echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
```

```
$ source ~/.bash_profile
```

```
$ rbenv install 2.3.3
```

```
$ rbenv global 2.3.3
```

```
$ ruby -v
```

### git 설치하기
https://sourceforge.net/projects/git-osx-installer/ 에서 인스톨 파일을 받아서 설치합니다.


### Node.js 설치하기[^1]

[^1]: http://junsikshim.github.io/2016/01/29/Mac에서-Node.js-설치하기.html

기존에 노드를 설치했다면 삭제합니다.


- /usr/local/lib 에 있는 node와 node_modules를 삭제
- /usr/local/include 에 있는 node와 node_modules를 삭제
- Homebrew로 설치하셨다면, brew uninstall node를 실행
- ~/local 또는 ~/lib 또는 ~/include 디렉토리 밑에 존재하는 node와 node_modules 삭제
- /usr/local/bin 에 있는 node 관련 실행파일들 삭제

추가로 아래의 명령을 실행합니다.

```
sudo rm /usr/local/bin/npm
sudo rm /usr/local/share/man/man1/node.1
sudo rm /usr/local/lib/dtrace/node.d
sudo rm -rf ~/.npm
sudo rm -rf ~/.node-gyp
sudo rm /opt/local/bin/node
sudo rm /opt/local/include/node
sudo rm -rf /opt/local/lib/node_modules
```

### nvm 설치하기

먼저 nvm(Node Version Manager)을 설치합니다.

```
$ curl https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash
```
터미널을 재실행하고 버전을 확인합니다.

```
$ nvm --version
```

### Node.js 설치하기

아래의 명령으로 가장 최신의 stable 버젼을 설치할 수 있습니다.

```
$ nvm install stable
```



### Hexo 설치하기(https://hexo.io/ko/docs/)

Node.js와 Git이 설치되있어야 합니다. 

```
$ npm install -g hexo-cli
```

### 블로그 생성

블로그 구조를 만듭니다. 여기서는 myBlog라는 이름으로 만듭니다.

```
$ hexo init myBlog
```
```
$ cd myBlog
```

```
$ npm install
```


로컬서버를 통해 확인합니다.

```
$ hexo server
```

브라우저에서 http://localhost:4000 을 입력하고 확인합니다.


## 설정하기

`myBlog/_config.yml` 파일을 수정합니다.






### Hueman 테마 적용하기

깃허브를 통해 테마 파일을 다운받습니다.

```
git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman
```

hueman 테마를 사용한다는 것을 지정해주어야 합니다. `myBlog/_config.yml` 에서 `theme:`의 값을 아래와 같이 수정합니다.

	theme: hueman

`myBlog/themes/hueman/_config.yml.example`파일의 이름 뒤에 붙어 있는 `.example`을 삭제해서 `_config.yml`로 바꿉니다.

브라우저로 localhost:4000으로 접속해서 테마가 적용된 것을 확인할 수 있습니다.

검색기능을 이용하기 위해서 hexo-generator-json-content를 설치합니다.

```
npm install -S hexo-generator-json-content
```

`_config.yml` 파일을 수정합니다.

참고 http://futurecreator.github.io/2016/06/14/get-started-with-hexo/


### cayman 테마의 색상 적용하기

hueman 테마의 색상이 조금 밋밋하다는 느낌이 들어서 cayman 테마의 알록달록한 색상을 적용시켜보았습니다. `myBlog/themes/hueman/source/css/_variables.styl` 파일의 안의 두곳을 찾아서 아래와 같이 값을 변경해줍니다..

```
color-header-background = linear-gradient(120deg, #155799, #159957);
...
color-footer-background = linear-gradient(120deg, #155799, #159957);
```


~~### toc 설정하기~~
~~toc(Table of Contents) 플러그인을 설치합니다.~~

```
npm install hexo-toc --save
```
markdown-toc도 설치합니다.

```
npm install markdown-toc --save
```


~~블로그 폴더의 `_config.yml` 파일에 아래 내용을 추가합니다.~~

```
toc:
  maxdepth: 3
  class: toc
  slugify: transliteration
  anchor:
    position: false
    symbol: '#'
    style: header-anchor
```

~~목차를 표시하고 싶은 포스트할 내용에 아래 코드를 추가합니다.~~

```
<!-- toc -->
```

~~목차가 자동으로 생성되는 것을 확인할 수 있습니다.[^2]~~

[^2]: `Plugin load failed: hexo-toc` `TypeError: Cannot read property 'slugify' of undefined` 라는 에러 메시지를 만나서 시행착오를 거쳤습니다. 문제는 `_config.yml`파일에 toc 관련 코드를 추가하지 않아서 발생했던 것이었습니다.

앵커 심볼이 생기는 것이 보기 싫어서 toc를 삭제하고 내장된 기능을 사용하기로 변경했습니다.

플러그인을 삭제합니다.

```
npm uninstall hexo-toc --save
npm uninstall markdown-toc --save
```

`myBlog/themes/hueman/layout/common/article.ejs`파일을 열고 `<%- post.context %> 코드 윗줄에 아래 코드를 추가합니다.

```
<% if(post.toc == true){ %>
	<div id="toc" class="toc-article">
	<strong class="toc-title">목 차</strong>
	<%- toc(post.content, {list_number: false}) %>
	</div>
<% } %>
```

위 코드는 변수 toc의 값이 true일 경우에 목차가 추가되는 기능을 수행합니다. 그러므로 목차를 넣고 싶은 글의 Front-matter 안에 `toc: true`라는 내용을 추가해야 합니다.
목차가 출력됩니다. 모양을 수정하기 위해 `myBlog/themes/hueman/source/css/_partial/article.styl`파일에 아래 내용을 추가합니다.

```

.toc-article {
    background: #eee;
    text-align: center;
    width: 100%;
    margin: 1em 0 0 -2.5em;
    padding: 1em 0;
}
.toc-article strong {
}
#toc {
    line-height: 1.6em;
    font-size: .9em;
    float: left
}
#toc .toc {
    padding-left: 2.5em;
    text-align: left;
}
#toc .toc li {
    list-style-type: none
}
#toc ol {
    margin-left: 0
}
#toc .toc-child {
    padding-left: 1.5em
}

```


### 본문 들여쓰기 스타일 적용하기


위 `article.styl`파일의 아랫 부분에 코드를 추가합니다.
```
.article-entry {
    padding-left: 2.5em;
}
.article-entry h2 {
    margin-top: 3.5em;
    margin-left: -1.5em;
}
.article-entry h3 {
    margin-top: 2.5em;
    margin-left: -1em;
}
.article-entry p {
    margin: 1em 0;
}
```

### footnote 설치하기

주석 기능을 사용하기 위해서 설치합니다.

```
npm install hexo-footnotes --save
```

`myBlog/theme/hueman/_config.yml`파일에서 `plugins:` 아래에 다음 코드를 추가합니다.

```
  hexo-footnotes:
```

주석과 본문 사이에 조금 여백을 주고 싶습니다. css 스타일을 조금 고칩니다. 위의 `article.styl`의 아래쪽에 다음 코드를 추가합니다.

```
#footnotes {
    margin-top: 3.5em;
}
```


> 사용 가능한 사이즈
- s small square 75x75
- q large square 150x150
- t thumbnail, 100 on longest side
- m small, 240 on longest side
- n small, 320 on longest side
- medium, 500 on longest side
- z medium 640, 640 on longest side
- c medium 800, 800 on longest side
- b large, 1024 on longest side
- o original image, either a jpg, gif or png, depending on source format


## 인터넷에 올리기
### github에 push하기

필요한 플러그인을 설치합니다.

```
$ npm install hexo-deployer-git --save
```
```
hexo generate
hexo deploy
```
아래와 같이 한 줄로 실행할 수도 있습니다.

```
hexo g -d
```

## 트러블슈팅
어제까지 잘 돌아가던 서버가 `hexo server`라는 명령에 대해서 `command not found: hexo`라는 메시지를 내놓습니다. 순간 당황스럽습니다. 먼저 터미널을 종료시킨 후 다시 열어서 실행해보아도 마찬가지입니다. `hexo`를 다시 설치해야하는게 하면서 `npm install -g hexo-cli`를 입력했더니 이번에도 마찬가지로 `command not found: npm`라는 메시지를 내뿜습니다. 이것이 무슨 조화인가요? 이해가 되지 않지만 하는 수 없이 nvm을 다시 설치합니다. `nvm install stable` 그랬더니 이번에는 `v7.2.0 is already installed.`라고 합니다. 그래서 혹시나 하는 마음으로 `hexo server`를 실행했더니 언제 그랬냐는 듯 아무 문제 없이 Hexo가 다시 잘 돌아가기 시작합니다.


## 참고 사이트

- [워드프레스보다 쉬운 Hexo 블로그 시작하기](http://futurecreator.github.io/2016/06/14/get-started-with-hexo/)
- [実録。WordpressからHexoにブログ移行して分かったメリット・デメリット](https://tea3.github.io/p/wordpress-to-hexo/)
- [markdownの記法まとめ・hexoで記事を書く方法](https://tea3.github.io/p/hexo-markdown-notation/)
- [CSS 여백속성(Margin, Padding Property)](http://webdir.tistory.com/346)
