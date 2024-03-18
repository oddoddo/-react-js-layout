# React Router를 이용한 프로젝트 시작하기

https://github.com/oddoddo/-react-js-layout

## 설치하기

### - 리액트 패키지 설치하기

-   리액트 프로젝트를 시작하기 전에 먼저 리액트 패키지를 설치해야 한다.

```js
npx create-react-app -react-js-layout
cd router-tutorial
```

### - 프로젝트에 라우터 설치하기

-   라우터를 적용하기 위해서는 react-router-dom 라이브러리를 설치해야 한다.

```js
yarn add react-router-dom
npm install react-router-dom
```

## layout 컴포넌트 만들기

### - Header 컴포넌트 만들기

-   `src/components/layout` 디렉토리에 `Header.jsx` 파일을 만든다.

```jsx
import React from 'react'

const Header = () => {
    return (
        <div>
            <h1>Header</h1>
            <nav>
                <ul>
                    <li>
                        <a href="/">Home</a>
                    </li>
                    <li>
                        <a href="/about">About</a>
                    </li>
                    <li>
                        <a href="/signup">SignUp</a>
                    </li>
                </ul>
            </nav>
        </div>
    )
}

export default Header
```

### - Footer 컴포넌트 만들기

-   `src/components/layout` 디렉토리에 `Footer.jsx` 파일을 만든다.

```jsx
import React from 'react'

const Footer = () => {
    return <div>Footer</div>
}

export default Footer
```

### - Layout 컴포넌트 만들기

-   `src/components/layout` 디렉토리에 `Layout.jsx` 파일을 만든다.

```jsx
import { Outlet } from 'react-router-dom'
import Footer from './Footer'
import Header from './Header'

const Layout = () => {
    return (
        <div>
            <Header />
            <main id="main">
                <Outlet />
            </main>
            <Footer />
        </div>
    )
}

export const LayoutNone = () => {
    return (
        <div>
            <main id="main">
                <Outlet />
            </main>
        </div>
    )
}

export default Layout
```

## 페이지 컴포넌트 만들기

### - Home 컴포넌트 만들기

-   `src/views` 디렉토리에 `Home.jsx` 파일을 만든다.

```jsx
import React from 'react'

const Home = () => {
    return <div>Home</div>
}

export default Home
```

### - About 컴포넌트 만들기

-   `src/views` 디렉토리에 `About.jsx` 파일을 만든다.

```jsx
import React from 'react'

const About = () => {
    return <div>About</div>
}

export default About
```

### - SignUp 컴포넌트 만들기

-   `src/views` 디렉토리에 `SignUp.jsx` 파일을 만든다.

```jsx
import React from 'react'

const SignUp = () => {
    return <div>SignUp</div>
}

export default SignUp
```

## 라우터 설정하기

### - Router 컴포넌트 만들기

-   `src` 디렉토리에 `Routers.jsx` 파일을 만든다.

```jsx
import React from 'react'
import { BrowserRouter, Route, Routes } from 'react-router-dom'
import Home from './views/Home'
import About from './views/About'
import SignUp from './views/SignUp'

const Routers = () => {
    return (
        <BrowserRouter>
            <Routes>
                <Route element={<Layout />}>
                    <Route path="/" element={<Home />} />
                    <Route path="/marketplace" element={<MarketPlace />} />
                    <Route path="/datatables" element={<DataTables />} />
                    <Route path="/profile" element={<Profile />} />
                </Route>

                <Route element={<LayoutNone />}>
                    <Route path="/signin" element={<Signin />} />
                </Route>
            </Routes>
        </BrowserRouter>
    )
}

export default Routers
```

### - App 컴포넌트 수정하기

-   `src` 디렉토리에 `App.js` 파일을 수정한다.

```jsx
import React from 'react'
import Routers from './Routers'

const App = () => {
    return <Routers />
}

export default App
```

## Chakra UI 적용하기

### - Chakra UI 설치하기

-   Chakra UI를 설치하기 위해서는 @chakra-ui/react와 @emotion/react, @emotion/styled 라이브러리를 설치해야 한다.

```js
yarn add @chakra-ui/react @emotion/react @emotion/styled framer-motion
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
```

### - Chakra UI Theme 만들기

-   `src/theme` 디렉토리에 `theme.js` 파일을 만든다.

```jsx
import { extendTheme } from '@chakra-ui/react'
import { breakpoints } from './foundations/breakpoints'
import { globalStyles } from './styles'
export default extendTheme(
    { breakpoints }, // Breakpoints
    globalStyles
)
```

### - Chakra UI Provider 적용하기

-   `src` 디렉토리에 `App.js` 파일을 수정한다.

```jsx
import Routers from './Routers'
import Routers from './Routers'
import { ChakraProvider } from '@chakra-ui/react'
import { ThemeProvider } from 'styled-components'
import theme from './theme/theme'

const App = () => {
    return (
        <ChakraProvider theme={theme}>
            <ThemeProvider theme={theme}>
                <Routers />
            </ThemeProvider>
        </ChakraProvider>
    )
}

export default App
```

## 실행하기

-   프로젝트를 실행하기 위해서는 다음 명령어를 실행한다.

```js
yarn start
npm start
```

## build 하기

-   프로젝트를 빌드하기 위해서는 다음 명령어를 실행한다.

```js
yarn build
npm run build
```
