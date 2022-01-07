# Svelte 프로젝트를 만드는 방법
-  첫번째 방법은 sveltejs에서 만들어 놓은 템플릿을 가지고 시작하는 방법입니다.
```shell
npx degit sveltejs/template <project명>
```

> **degit** : https://www.github.com/sveltejs/template 을 쉽게 가져올 수 있도록 명령어에 대한 alias를 준 느낌이 난다. 현재도 git clone https://www.github.com/sveltejs/template <project명> 을 통해서 폴더를 생성하였다면, 위와 같이 간단히 표현하여 repository 위치만 안다면 쉽게 가져올 수 있도록 개선된 느낌이다.

- 두번째 방법으로 Svelte로 구동되는 애플리케이션 프레임워크로 시작하는 방법입니다.
```shell
npm init svelte@next <project명>
```
> sveltekit의 경우에는 현재(2022.01.07)에도 정식버젼으로 출시가 되어 있지 않다. 이에, 정식버젼이 출시되기 전까지는 계속적인 변경이 있을 것이라고 판단된다.

# Svelte 의 특징
- 적은 코드
- 순수한 리액티비티(반응형)
  - 스벨트 공식 사이트에서는 `Truly reactive` 정의하고 있습니다.

# Svelte 파일의 형식
- 스벨트 파일은 다음과 같은 형식으로 표현됩니다.
  - 확장자는 **.svelte**로 끝나게 됩니다.
  - 파일 안의 내용은 다음과 같습니다.
    
    ```html
    <!-- 자바스크립트 코드 -->
    <script>
        스크립트 블록
    </script>

    <!-- HTML 코드 -->
    <main>
        HTML 블록
    </main>

    <!-- CSS 코드 -->
    <style>
        스타일 블록
    </style>
    ```

> 중요점 : 순수한 리액티비티(반응형)을 사용하기 위해서는 반드시 할당 연산자(=)을 사용해야 합니다.

# 템플릿 기본 표현식
## if 블록
```
{#if}

{:else if}

{/if}
```

## each 블록
```
{#each array as item, index}

{/each}
```

> 참고 : json을 object로 만들시에는 Object.entries(<json 객체>)를 사용합니다.

## Promise를 위한 await 블록
```
{#await}
    // 동작 중일 때 처리
{:then res}
    // 정상 종료 후  처리
{:catch error}
    // 에러일 때 처리
{/await}
```

## 부분 rerendering
```
{#key <변수명>}
    // 변수의 값이 변경될 때마다 rerendering 될 수 있도록 하는 코디
{/key}
```

## html 출력
```
{@html <변수명>}
```

## debuging
```
{@debug <변수명>}
```

## reactive programing
```
`$:` 을 사용하여 반응성을 극대화 처리
```

