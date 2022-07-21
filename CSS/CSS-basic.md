# CSS 방법론 정리

<br>

개별항목에 대해 CSS를 작성하면 중복되는 코드가 많아진다. 더욱이 협업 프로젝트이고 규모가 커진다면 유지보수는 더더욱 어려운 일이 된다. 따라서 원칙을 정해두고 그 안에서 작성하는 것이 효율적이며 CSS 방법론은 그런 고민 위에 성립하는 것이다


## CSS 방법론의 종류

+ OOCSS
+ SMACSS
+ BEM

<br>
### OOCSS

> **Object Oriented CSS**의 약자. 구조/외양의 분리, 컨테이너와 컨텐츠의 분리를 주요 개념으로 삼는다. 

```
//구조 : 같은 구조에서 공통적인 정의
.btnbase{
  border: ...;
  padding : ...;
}

//외양 : 요소마다 다른 외양
.google{
  background: ...;
}

//컨테이너 : 컨텐츠를 담는 그릇
.header{
  position: ...;
  top: ...;
}
```

### SMACSS

> **Scalable and Modular Architecture for CSS**의 약자. base, layout, module, state, theme을 주요 개념으로 삼는다.

```

//base : 구조를 표현. 리셋도 포함된다.
body, form, input{
  margin: ...;
  padding: ...;
}

//layout : 주요 컴포넌트, 하위요소를 나누고 id, class를 병용하여 제어한다. 
#header{
  width: ...;
}

//하위 요소
,l-width #header{
  width: ...;
  padding: ...;
}

//module : 재사용을 위한 요소, id/element를 사용하지 않는다. 
.slider{
  width: ...;
  background: ...;
}

//state: 상태를 나타내는 스타일. class에 is- 혹은 s-를 붙여서 나타낸다.
.is-active{
  background-color:...;
}

//theme: 사이트의 전반적인 색채
.mod{
  border: ...;
}
```
<br>
### BEM

>**Block Element Modifier**의 약자. 객체지향과 유사하며 보이는 모습보다 목적에 초점을 두고 작성한다. 

```
//block : 재사용성이 있고 기능적으로 독립 가능. element를 담고 있는 컴포넌트.
.header {...}
.menu{...}

//element : block안에서 특정 기능을 수행함
.header__logo{...}
.header__menu{...}

//modifiers : block, element요소의 속성 외관/상태를 변화시킨다. 
.header--hide{...}
.header__tap--big{...}
```


