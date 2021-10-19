*요약
JSX 는 리액트에서 생김새를 정의할 때, 사용하는 문법입니다. 얼핏보면 HTML 같이 생겼지만 실제로는 JavaScript 입니다.

return <div>안녕하세요</div>;
리액트 컴포넌트 파일에서 XML 형태로 코드를 작성하면 babel 이 JSX 를 JavaScript 로 변환을 해줍니다.

Babel 은 자바스크립트의 문법을 확장해주는 도구입니다. 아직 지원되지 않는 최신 문법이나, 편의상 사용하거나 실험적인 자바스크립트 문법들을 정식 자바스크립트 형태로 변환해줌으로서 구형 브라우저같은 환경에서도 제대로 실행 할 수 있게 해주는 역할을 합니다.

JSX 가 JavaScript 로 제대로 변환이 되려면 지켜주어야 하는 몇가지 규칙이 있습니다. 다음 문법들을 준수해주시면 앞으로 리액트 컴포넌트를 개발함에 있어서 큰 어려움이 없을 것입니다!

꼭 닫혀야 하는 태그
태그는 꼭 닫혀있어야 합니다.

태그를 열었으면 꼭, <div></div> 이렇게 닫아주어야 합니다.

HTML 에서는 input 또는 br 태그를 사용 할 때 닫지 않고 사용하기도 합니다. 하지만 리액트에서는 그렇게 하면 안됩니다.

태그와 태그 사이에 내용이 들어가지 않을 때에는, Self Closing 태그 라는 것을 사용해야 합니다. 현재 Hello 컴포넌트를 사용 할 때에도 Self Closing 태그를 사용해주었는데요, 열리고, 바로 닫히는 태그를 의미합니다.

하지만, 이렇게 단순히 감싸기 위하여 불필요한 div 로 감싸는게 별로 좋지 않은 상황도 있습니다. 예를 들어서 스타일 관련 설정을 하다가 복잡해지게 되는 상황도 올 수 있고, table 관련 태그를 작성 할 때에도 내용을 div 같은걸로 감싸기엔 애매하죠. 그럴 땐, 리액트의 Fragment 라는 것을 사용하면 됩니다.

태그를 작성 할 때 이름 없이 작성을 하게 되면 Fragment 가 만들어지는데, Fragment 는 브라우저 상에서 따로 별도의 엘리먼트로 나타나지 않습니다.

style 과 className
JSX 에서 태그에 style 과 CSS class 를 설정하는 방법은 HTML 에서 설정하는 방법과 다릅니다.

우선, 인라인 스타일은 객체 형태로 작성을 해야 하며, background-color 처럼 - 로 구분되어 있는 이름들은 backgroundColor 처럼 camelCase 형태로 네이밍 해주어야 합니다.

JSX 내부의 주석은 {/* 이런 형태로 */} 작성합니다.
추가적으로, 열리는 태그 내부에서는 // 이런 형태로도 주석 작성이 가능합니다.


## 1. JSX의 정의와 장점
JSX는 함수 호출과 객체 생성을 위한 문법적 편의를 제공하는 자바 스크립트의 확장으로, 특히 React.createElement() 호출을 반복해야 하는 불편을 해소한다. 

JSX의 장점을 정리해 보면 다음과 같다.
- 개발자 경험 개선
- 팀의 생산성 향상
- 문법 오류와 코드량 감소

JSX 를 자바스크립트로 변환하여 사용하는 과정 

JSX -> 트랜스파일러 -> 자바스크립트 -> 브라우저
JSX를 사용해야 하는 주된 이유는 대부분의 사람들이 React.createElement()가 많은 코드보다 화살괄호(<>)가 있는 코드를 더 편하게 읽기 떄문이다. 

## 2. JSX의 이해

### JSX로 React 엘리먼트 생성하기
```
React.createElement(
    name,
    {key1: value1, key2: value2, ...},
    child1, child2, child3, ..., childN
)
```
이것을 JSX 로 옮기면 다음과 같다.
```
<name key1=value1 key2=value2>
    <child1/>
    <child2/>
    <child3/>
    <child4/>
    <child5/>
    <child6/>
</name>
```


## 3. JSX에서 속성 사용하기

DOM 요소에 속성으로 정보를 넣는 것은 흔히 사용하는 방식이다. 다음 예제 코드는 react-is-awesome과 id속성을 사용하고 있다.
```
<li react-is-awesome="true" id="320"> React is awesome! </li>
```
DOM의 HTML 비표준 속성에 데이터를 저장하는 것은 일반적으로 안티패턴으로 여겨진다. DOM에서 데이터를 가져오는 것은 메모리상의 가상 저장소에서 데이터를 가져오는 것보다 느리다. 

JSX를 사용할 때 데이터를 반드시 HTML 요소의 속성으로 저장해야 하는 경우에는 data-* 속성을 사용한다. 
```
<li data-react-is-awesome="true">React is awesome!</li>
```

확실히, 사용자 지정 컴포넌트 클래스에는 내장 렌더러가 없고, 표준 HTML 요소나 다른 사용자 지정 엘리먼트에 의존하므로 데이터를 다루기 위해 data-* 속성을 사용할 필요는 없다. this.props를 통해서 입력한 모든 속성에 접근할 수 있기 때문이다.

```
class HelloWord extends React.Component {
    render() {
        return React.createElement(
            'h1',
            this.props,
            'Hello ' + this.props.frameworkName + ' world!'
        )
    }
}
```
만약 위의 코드를 jsx로 구현하여 속성을 전달하려면 어떻게 해야할까?  
JSX에서는 이에대한 해결책으로 생략 부호(...)처럼 생긴 펼침 연산자를 사용할 수 있다.

```
class HelloWorld extends React.Component {
    render() {
        
        return <h1> {...this.props}>Hello {this.props.frameworkName} world!!! </h1>
    }
}

ReactDOM.render(
    <div>
        <HelloWorld
            id='emeber'
            frameworkName='Ember.js'
            title='Aframework for creating ambitious web applications.'/>,
        <HelloWorld
            id='backbone'
            frameworkName='backbone.js'
            title='Aframework for creating ambitious web applications.'/>,
        <HelloWorld
            id='emeber'
            frameworkName='angular.js'
            title='Aframework for creating ambitious web applications.'/>
    </div>
    , document.getElementById('content')
```

## 4 React 컴포넌트 메서드 생성하기

React 컴포넌트에 애플리케이션을 위한 메서드를 자유롭게 추가할 수 있다. React 컴포넌트가 클래스이기 때문이다. 

```
class Content extends React.Component
{
    getUrl() {
        return 'http://webapplog.com'
    }
    render() {
        ...
    }
}
```

## 5 JSX의 if/else 처리
동적 변수를 렌더링했던 것과 유사하게, 개발자는 if/else 조건의 결과에 따라 컴포넌트가 뷰를 변경할 수 있도록 작성해야 하는 경우도 있따. 먼저 컴포넌트 클래스에 조건에 따라 다른 링크 엘리멘트를 렌더링 하는 간닪나 예제를 본다.

```
render() {
    if (user.session)
        return React.createElement('a', {href: '/logout'}, 'Logout')
    else
        return React.createElement('a', {href: '/login'}, 'Login')
}
```

이와 비슷한 방법으로 JSX를 사용하면 다ㅡㅇㅁ과 같다.
```
render() {
    if (this.props.user.session)
        return <a href="/logout">Logout</a>
    else
        return <a href="/login">Login</a>
}
```

선호하는 방식
```
render(){
    let sessionFlag = this.props.user.session
    return <div>
        <a href={(sessionFlag) ? '/logout' : '/login'}>
            {(sessionFlag) ? 'Logout' : 'Login'}
        </a>
    </div>
}

```

## 6 JSX의 주석 작성방법

```
let content = (
    <div>
        {/* 표준 자바스크립트의 주석과 같으나 {} 감싸주는게 다르다*/}
    </div>
)

