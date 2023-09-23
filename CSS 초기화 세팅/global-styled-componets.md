# styled-components 초기화 세팅

## ❗️styled-components가 깔려 있어야 세팅이 가능

<br />

1. styled-reset 설치

    ```shell
    npm install styled-reset
    ```


2. globalStyle.js 파일 생성
3. 아래 내용 기입

    ```js
    // globalStyle.js
    import { createGlobalStyle } from "styled-components";
    import reset from 'styled-reset';

    const GlobalStyles = createGlobalStyle`
      ${reset}
      a {
        text-decoration: none;
        color: inherit;
      }

      * {
        box-sizing: border-box;
      }

      input, textarea { 
        -moz-user-select: auto;
        -webkit-user-select: auto;
        -ms-user-select: auto;
        user-select: auto;
      }

      input:focus {
        outline: none;
      }


      button {
        border: none;
        background: none;
        padding: 0;
        cursor: pointer;
      }
    `

    export default GlobalStyles;
    ```

4. App.js 파일에 태그 생성
    ```js
    // App.js
    function App() {
      return (
        <Router>
          <GlobalStyles />
          <Routes>
            <Route path="/movie/:id" element={<Detail />} />
            <Route path="/" element={<Home />} />
          </Routes>
      </Router>
      );
    }
    ```