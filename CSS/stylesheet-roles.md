# SASS 스타일 가이드 규칙



이 정리글은 SASS에 대한 것을 요약 및 알기 쉽게 정리한 문서이며, 

이 글의 원 저자인 <u>Hugo Giraudel</u>의 문서를  [참고](https://sass-guidelin.es/ko/) 하였습니다.



## 핵심 전략

-   **KISS(Keep It Simple Stupid)** - 단순하게 하라
-   **YAGNI(You Ain't Gonna Need It** - 정말 필요할 때까지 그 기능을 만들지 마라
    -   미리 필요없는 기능을 추가해두면 코드 자체가 길어지기 때문에 분석 자체가 더 어려워지며 또한 버그가 발생할 가능성이 커집니다.
-   **DRY(Don't Repeat Yourself** - 똑같은 일을 반복하지 마라
    -   중복되는 함수나 코드는 하나의 공통의 콤포넌트에 넣고 사용한다.
    -   큰 시스템을 여러조각으로 나누고 서로 참조한다.
    -   프로젝트가 소규모일때는 코드분석이 쉬운 반면 대규모로 커질시에는 복잡도가 기하급수적으로 높아지게 된다.
    -   중복을 줄여야 **개발과 유지보수비용이 절감**된다.
-   **클린코드**
    -   함수나 클래스를 다른 프로그래머가 당연하게 여길 만한 동작과 기능을 넣어야 한다.



## 핵심 원칙

-   **Sass는 가능한 한 간단하게 유지되어야 한다**
    -   SASS는 CSS를 작성하도록 의도 되었으므로, 보통의 CSS 보다 더 복잡해져선 안 됩니다.
    -   위 정리한 KISS전략이 핵심



## 구문 & 서식

-   탭 대신 스페이스 두 칸 들여쓰기
-   이상적인 행의 너비는 80글자
-   적절하게 쓰인 여러행의 CSS 규칙
-   공백의 의미 있는 사용

```scss
// Yes!
.foo {
  display: block;
  overflow: hidden;
  padding: 0 1em;
}

// No!!
.foo {
		display: block; overflow: hidden;
		padding: 0 1em;
}
```



## 문자열

#### 인코딩

*   메인 스타일시트에서 @charset 지시어를 사용해 UTF-8 인코딩을 강제하는 것이 강력하게 권장됩니다.

*   가장 첫 번째 요소이며, 어떤 종류의 문자도 앞에 오지 않도록 주의하세요.

    ```SCSS
    @charset 'utf-8';
    ```



#### 따옴표

*   **문자열은 언제나 작은 따옴표(')로 감싸져야 합니다.**
*   색 이름은 따옴표가 없으면 색으로 취급되는데, 이는 심각한 문제로 이어질 수 있다.
*   대부분의 구문 강조기는 따옴표 없는 문자열을 지원하지 못할 것이다.
*   전반적인 가독성에 도움이 된다.
*   문자열을 따옴표로 감싸지 않을 적절한 이유가 없다.

```SCSS
// Yes!
$direction: 'left';

// No!!
$direction: left;
```



#### CSS 값인 문자열

*   initial 이나 sans-serif 같은 특정 CSS 값은 따옴표로 싸여서는 안됩니다.
*   font-family: 'sans-serif' 같은 선언의 경우 CSS는 인용부호가 붙은 문자열이 아니라 식별자를 기대하고 있습니다.
    *   따라서 아무 경고도 없이 작동하지 않을 것 입니다.

```SCSS
// Yes!
$font-type: sans-serif;

// No!!
$font-type: 'sans-serif';

// Okay I guess
$font-type: unquote('sans-serif');
```

따라서, 우리는 앞의 예처럼 CSS 값 (CSS 식별자)으로 사용될 문자열과 맵 키와 같은 Sass 자료 유형에 쓰일 문자열을 구별할 수 있습니다.

전자에는 따옴표를 붙이지 않지만, 후자는 작은 따옴표로 감쌉니다.



#### 따옴표를 포함한 문자열

만약 문자열이 하나 혹은 여러개의 작은 따옴표를 포함하고 있다면, 문자열 안에서 과도한 문자 이스케이프를 피하기 위해 대신 큰 따옴표(")로 문자열 감싸는 것을 고려해 볼 수 있습니다.

```SCSS
// Okay
@warn 'You can\'t do that.';

// Okay
@warn "You can't dn that.";
```

#### URL

URL 역시 위와 동일한 이유로 따옴표로 감싸여야 합니다.

```SCSS
// Yes!
.foo {
  background-image: url('/imgaes/kittens.jpg');
}

// No!!
.foo {
  background-image: url(/images/kittens.jpg);
}
```



## 숫자

#### 영

*   숫자는 1보다 작은 소수 앞에 앞장서는 영을 표기해야 합니다. 
*   뒤따르는 영은 절대 표기하지 마세요.

```SCSS
// Yes!
.foo {
  padding: 2em;
  opacity: 0.5;
}

// No!!
.foo {
  padding: 2.0em;
  opacity: .5;
}
```

#### 단위

*   길이를 다룰 때, 0은 절대로 단위를 가져서는 안 됩니다.

```SCSS
// Yes!
$length: 0;

// No!!
$length: 0em;
```

Sass에서 숫자와 관련해 제가 생각할 수 있는 가장 흔한 실수는 단위가 숫자에 안전하게 덧붙여질 수 있는 문자열이라고 생각하는 것입니다. 이게 그럴 듯하게 들리긴 하지만, 단위가 작동하는 방식은 분명히 아닙니다. 단위를 대수 기호라고 생각해 보세요. 예를 들어 실제 세계에서, 5인치에 5인치를 곱하면 25 제곱 인치가 나옵니다. 똑같은 논리가 Sass에도 적용됩니다.

단위를 숫자에 붙이기 위해서는, 이 숫자에 *1단위*를 곱해야 합니다.

```Scss
$value: 42;

// Yes!
$length: $value * 1px;

// No!!
$length: $value + px;
```

*0단위*를 더하는 것도 역시 같은 결과를 내긴 하지만, *0단위*를 더하는 것은 약간 혼란스러울 수 있기 때문에 앞서 언급한 방법을 추천합니다. 사실, 숫자를 다른 호환되는 단위로 변환하려고 할 때, 0을 더하는 것은 효과가 없습니다.

```SCSS
$value: 42 + 0px;
// -> 42px

$value: 1in + 0px;
// -> 1in

$value: 0px + 1in;
// -> 96px
```

결국에는, 여러분이 달성하려고 하는 것이 무엇인지에 달려있습니다. 단위를 문자열로서 더하는 것은 좋은 방법이 아니라는 점을 명심하세요.

값의 단위를 제거하기 위해서는, *그 종류의 한 단위*로 나누어야 합니다.

```SCSS
$length: 42px;

// Yes!
$value: $length / 1px;

// No!!
$value: str-slice($length + unquote(''), 1, 2);
```

단위를 문자열로서 숫자에 덧붙이면 결과물은 문자열이 되며, 그 값으로 더 이상 연산을 할 수 없습니다. 숫자의 숫자 부분을 단위에서 잘라내면 그 결과 역시 문자열이 됩니다. 이것은 여러분이 원하는 것이 아닙니다.



#### 연산

**최상위 숫자 계산은 언제나 괄호로 감싸져야 합니다.** 이 요건은 가독성을 향상시킬 뿐만 아니라, Sass가 괄호 안의 수치를 계산하도록 강제함으로써 일부 예외적인 상황을 방지합니다.

```scss
// Yes!
.foo {
  width: (100% / 3);
}

// No!!
.foo {
  width: 100% / 3;
}
```

#### 매직 넘버

"매직 넘버는" *익명의 숫자 상수*를 일컫는 [전통적인 프로그래밍 용어](https://en.wikipedia.org/wiki/Magic_number_(programming)#Unnamed_numerical_constants)입니다. 기본적으로, 이 숫자는 어쩌다보니 *맞아떨어지지만* 어떤 논리적인 설명과도 관련되지 않은 임의의 숫자입니다.

말할 것도 없이 **매직 넘버는 역병 같은 존재이며 무슨 수를 써서라도 피해야 합니다.** 왜 매직넘버가 효과를 내는지에 대한 합리적인 설명을 찾을 수 없을 때는, 어떻게 거기에 도달했고 왜 효과를 낸다고 생각하는지를 설명하는 충분한 주석을 달하놓으세요. 무언가가 제대로 작동하는 이유를 모른다고 인정하는 것이 그래도 아무런 사전 정보 없이 알아내게 하는 것보다 다음 개발자에게 더 도움이 됩니다.

```scss
/**
 * 1. 매직 넘버. `.foo`의 상단을 부모에 맞춰 정렬시키기 위해 찾은
 * 낮은 값이다. 가능하다면, 적절하게 고쳐야 할 것.
 */
.foo {
  top: 0.327em; /* 1 */
}
```



## 색

색은 CSS 언어에서 중요한 위치를 차지하고 있습니다. 자연스럽게, Sass는 몇 가지 [강력한 함수](https://sass-lang.com/documentation/modules)를 제공함으로써 색 조작에 있어 소중한 동맹이 되었습니다.

#### 색 서식

색을 가능한 한 간단하게 만들기 위한 제 조언은 색 서식에 대한 다음의 우선 순위를 따르라는 것입니다.

1.  [CSS 색 키워드]()
2.  [HSL 표기법](http://en.wikipedia.org/wiki/HSL_and_HSV)
3.  [RGB 표기법](http://en.wikipedia.org/wiki/RGB_color_model)
4.  16진법 표기법. 가급적 소문자와 가능한 경우 단축형으로.

우선, 키워드는 자명한 서식입니다. HSL 표기는 인간의 두뇌로 이해하기에 가장 쉬울 뿐만 아니라 스타일 시트 작성자가 색상, 채도, 명도를 조정함으로써 색을 변경하는 일을 쉽게 만듭니다. RGB 역시 색이 청색, 녹색, 적색 중 어느 것에 가까운지 바로 보여주는 이점을 갖고 있지만 세 속성으로부터 색을 제조하는 일을 쉽게 만들어주진 않습니다. 마지막으로 16진법은 인간의 머리로는 거의 해독이 불가능합니다.

```SCSS
// Yes!
.foo {
  color: hsl(0, 100%, 50%);
}

// Also Yes!
.foo {
  color: rgb(255, 0, 0);
}

// Humm..
.foo {
  color: #f00;
}

// No!!
.foo {
  color: #FF0000;
}

// No!!
.foo {
  color: red;
}
```

HSL이나 RGB 표기를 사용할 때, 쉼표(`,`) 뒤에는 언제나 스페이스 한 칸을 더하고 괄호(`(`, `)`)와 내용 사이에는 스페이스를 넣지 마세요.

```scss
// Yes!
.foo {
  color: rgba(0, 0, 0, 0.1);
  background: hsl(300, 100%, 100%);
}

// No!!
.foo {
  color: rgba(0,0,0,0.1);
  background: hsl( 300, 100%, 100% );
}
```



#### 색과 변수

색을 한 번 이상 사용할 때는 색을 대변하는 의미 있는 이름을 붙여 번수에 저장하세요.

```scss
$sass-pink: hsl(330, 50%, 60%);
```

이제 이 변수를 언제든 원할 때마다 자유롭게 사용할 수 있습니다. 하지만, 만약 변수의 용도가 테마와 깊은 관련이 있다면, 변수를 그대로 사용하지말라고 조언하겠습니다. 대신, 그 변수가 어떻게 사용도어야 하는지 설명하는 이름을 붙여 다른 변수에 저장하세요.

```scss
$main-theme-color: $sass-pink;
```

이렇게 함으로써 테마 변경이 $sass-pink: blue 같은 사태를 초래하는 것을 방지 할 수 있습니다.



#### 색 명암 조절

[lighten](http://sass-lang.com/documentation/Sass/Script/Functions.html#lighten-instance_method)과 [darken](http://sass-lang.com/documentation/Sass/Script/Functions.html#darken-instance_method) 두 함수는 HSL 공간에서 색의 명도를 증감하여 조정합니다. 기본적으로, 이들은 [adjust-color](http://sass-lang.com/documentation/Sass/Script/Functions.html#adjust_color-instance_method) 함수의 $lightness 매개 변수의 가명일 뿐입니다.

문제는, 이들 함수가 가끔 기대되는 결과를 제공하지 않는다는 것입니다. 반면에, [mix](http://sass-lang.com/documentation/Sass/Script/Functions.html#mix-instance_method) 함수는 색을 white나 black과 혼합함으로써 명암을 조절하는 좋은 방법입니다.

앞서 언급한 두 함수보다 mix를 사용하는 것의 이점은 색의 비율을 감소시킴에 따라 점진적으로 검은 색(혹은 흰 색)으로 나아간다는 점입니다. 반면 darken과 lighten은 색을 순식간에 완전한 검은 색이나 흰 색으로 보내버릴 것입니다.

만약 매번 mix 함수를 쓰는 것을 원치 않으신다면, 두 가지 사용하기 쉬운 tint와 shade 펑션을 만들어 같은 일을 할 수 있습니다.

```scss
/// 색을 약간 밝게 한다
/// @access public
/// @param {Color} $color - 밝게 만들려는 색
/// @param {Number} $percentage - 반환될 색 내 `$color`의 백분율
/// @return {Color}
@function tint($color, $percentage) {
  @return mix(white, $color, $percentage);
}

/// 색을 약간 어둡게 한다
/// @access public
/// @param {Color} $color - 어둡게 만들려는 색
/// @param {Number} $percentage - 반환될 색 내 `$color`의 백분율
/// @return {Color}
@function shade($color, $percentage) {
  @return mix(black, $color, $percentage);
}
```



## 리스트

리스트는 Sass에서 배열에 상당하는 개념입니다. 리스트는 어떤 타입의 값이든(리스트도 포함. 이 경우 내포 리스트가 된다) 저장할 수 있게 의도된 ([맵](https://sass-guidelin.es/ko/#section-32)과 달리) 평면적인 데이터 구조입니다.

리스트는 다음의 가이드라인을 준수해야 합니다:

-   한 줄 혹은 여러 줄
-   80자 줄에 안 들어갈 정도로 길면 반드시 여러 줄에 표기한다
-   CSS 상에서 그대로 사용되지 않는 한, 언제나 쉼표로 분리한다
-   언제나 괄호로 감싼다
-   여러 줄인 경우 뒤따르는 쉼표를 붙이고, 한 줄인 경우 제외한다.

```scss
// Yes!
$font-stack: ('Helvetica', 'Arial', sans-serif);

// Yes!
$font-stack: (
  'Helvetica',
  'Arial',
  sans-serif,
);

// No!!
$font-stack: 'Helvetica' 'Arial' sans-serif;

// No!!
$font-stack: 'Helvetica', 'Arial', sans-serif;

// No!!
$font-stack: ('Helvetica', 'Arial', sans-serif,);
```

리스트에 새로운 아이템을 추가할 때는, 언제나 제공된 API를 이용하세요. 수동으로 새로운 아이템을 추가하려고 하지 마세요.

```scss
$shadows: (0 42px 13.37px hotpink);

// Yes!
$shadows: append($shadows, $shadow, comma);

// No!!
$shadows: $shadows, $shadow;
```



## 맵

Sass 3.3부터, 스타일시트 작성자는 맵을 정의할 수 있는데, 이는 연관 배열, 해쉬 혹은 JavaScript 오브젝트에 해당하는 Sass 용어입니다. 맵은 키를 모든 유형의 값과 연결하는 자료 구조입니다 (키는 어떤 자료 유형도 될 수 있습니다. 추천하지는 않지만 맵도 포함됩니다).

맵은 다음과 같이 작성되어야 합니다:

-   콜론(`:`) 다음에 스페이스
-   여는 괄호 (`(`)는 콜론(`:`)과 같은 줄에
-   (99%의 경우에 해당하는) 문자열인 **키는 따옴표로 감싼다**
-   각각의 키/값 쌍은 새 줄을 차지한다
-   각 키/값 뒤에는 쉼표(`,`)
-   추가, 제거 혹은 순서를 바꾸기 쉽도록 마지막 아이템 **뒤에 따라오는 쉼표**(`,`)
-   닫는 괄호(`)`)는 새 줄을 차지한다
-   닫는 괄호(`)`)와 세미콜론(`;`) 사이에는 스페이스나 새 줄을 넣지 않는다.

```scss
// Yes!
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);

// No!!
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );
```

#### SASS 맵 디버그

어떤 미친 마법이 Sass 맵에서 일어나고 있는 건지 알 수 없어 헤매는 스스로를 발견하게 된다면, 아직 구원받을 수 있는 방법이 있으니 걱정하지 마십시오.

```scss
@mixin debug-map($map) {
  @at-root {
    @debug-map {
      __toString__: inspect($map);
      __length__: length($map);
      __depth__: if(function-exists('map-depth'), map-depth($map), null);
      __keys__: map-keys($map);
      __properties__ {
        @each $key, $value in $map {
          #{'(' + type-of($value) + ') ' + $key}: inspect($value);
        }
      }
    }
  }
}
```

맵의 깊이를 알고 싶으시면 아래 함수를 추가하세요. 위의 믹스인이 자동으로 값을 표시할 것입니다.

```scss
/// 맵의 최대 깊이를 계산한다
/// @param {Map} $map
/// @return {Number} `$map`의 최대 깊이
@function map-depth($map) {
  $level: 1;

  @each $key, $value in $map {
    @if type-of($value) == 'map' {
      $level: max(map-depth($value) + 1, $level);
    }
  }

  @return $level;
}
```



## CSS 규칙

*   관련된 선택자는 같은 줄에. 관련 없는 선택자는 새 줄에
*   여는 중괄호({)는 마지막 선택자와 스페이스 한 칸의 간격을 둔다
*   각각의 선언은 저마다 새 줄을 차지한다
*   콜론(:) 뒤에는 스페이스 한 칸을 둔다
*   모든 선언의 끝은 세미콜론(;)으로 마무리한다
*   닫는 중괄호(})는 새 줄을 차지한다
*   닫는 중괄호(}) 뒤에 새 줄

```scss
// Yes!
.foo, .foo-bar
.baz {
  display: block;
  overflow: hidden;
  margin: 0 auto;
}

// No!!
.foo,
.foo-bar, .baz {
  display: block;
  overflow: hidden;
  margin: 0 auto;
}
```

CSS와 관련된 가이드라인에 더해, 우리는 다음 사항들에 관심을 기울여야 합니다.

*   지역 변수는 어떤 선언보다 먼저 선언되어야 하며, 새 줄 하나로 다른 선언들과 간격을 둔다.
*   @content가 없는 믹스인 호출은 다른 선언보다 앞에 위치한다.
*   내포된 선택자는 언제나 새 줄 뒤에 온다.
*   @content를 가진 믹스인 호출은 내포된 선택자보다 뒤에 위치한다.
*   닫은 중괄호(}) 앞에는 새 줄이 없어야 한다.

```scss
.foo, .foo-bar,
.baz {
  $length: 42em;
  
  @include ellipsis;
  @include size($length);
  display: block;
  overflow: hidden;
  margin: 0 auto;
  
  &:hover {
    color: red;
  }
  
  @include respond-to('small') {
    overflow: visible;
  }
}
```



## 선언 정렬

전 CSS 선언을 정렬하는 문제 만큼 견해가 갈리는 주제를 별로 떠올릴 수가 없습니다. 구체적으로, 여기 두 파가 없습니다

*   알파벳 순서 고수하기
*   유형 별로 정렬하기(position, display, colors, font, 기타 등등...).

두 가지 방법 모두 장단점이 있습니다. 우선, 알파벳순은 (적어도 로마자를 사용하는 언어에서는) 보편적인 만큼 한 속성을 다른 속성 앞에 정렬하는 문제가 논쟁거리가 못됩니다. 하지만, bottom과 top 같은 속성들이 서로 붙어있지 않은 모습이 제겐 엄청나게 이상해보입니다. 왜 애니메이션이 디스플레이 유형보다 먼저 나와야 합니까? 알파벳순에는 이상한 점이 많이 있습니다.

```scss
.foo {
  background: black;
  bottom: 0;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
  height: 100px;
  overflow: hidden;
  position: absolute;
  right: 0;
  width: 100px;
}
```

반면, 유형별로 속성을 정렬하는 것은 아주 타당합니다. 모든 폰트 관련 선언들이 한데 모이고, top과 bottom은 재결합하며 규칙들을 보면 마치 짧은 이야기를 읽는 느낌입니다. 그러나 <u>Idiomatic CSS</u>와 같은 관례를 고수하지 않는 한 이 방식은 여러가지로 해석될 수 있습니다. white-space는 어디로 가야 할까요, 폰트 혹은 디스플레이? overflow는 정확히 어디에 속할까요? 그룹 내에서 속성들의 순서는 어떻게 되어야 할까요(역설적이게도, 알파벳순으로 정렬할 수도 있겠죠)?

```scss
.foo {
  height: 100px;
  width: 100px;
  overflow: hidden;
  position: absolute;
  bottom: 0;
  right: 0;
  background: black;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
}
```

유형별 정렬의 다른 흥미로운 하위 갈래로 Concentric CSS라는 것이 