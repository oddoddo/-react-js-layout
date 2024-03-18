# React를 이용한 layout 컴포넌트, React Router(리액트 라우터) 페이지 이동 구현하기

> React에서는 컴포넌트를 사용하여 UI를 재사용할 수 있다.  
> Header, Footer, Content 등의 레이아웃을 Layout 컴포넌트로 만들어 사용할 수 있다.

Chakra-ui를 사용해서 DashBoard의 Layout을 만들어보려고 합니다.  
아래 url의 디자인을 참고해 만들었습니다.

[https://www.figma.com/file/BUftfMT534u7HVEu59yBQI/Horizon-UI---Trendiest-Open-Source-Admin-Template-Dashboard-(Community)?type=design&node-id=0%3A1&mode=design&t=0NT1hIAfKRQKTVGJ-1](<https://www.figma.com/file/BUftfMT534u7HVEu59yBQI/Horizon-UI---Trendiest-Open-Source-Admin-Template-Dashboard-(Community)?type=design&node-id=0%3A1&mode=design&t=0NT1hIAfKRQKTVGJ-1>)

[##_Image|kage@c4MqW8/btsyOWKoL34/uD27Rt53Ih7p0VZwu8Yoek/img.jpg|CDM|1.3|{"originWidth":1920,"originHeight":1152,"style":"alignCenter","filename":"Tables.jpg"}_##]

## 1\. Layout 컴포넌트 만들기

-   Layout 컴포넌트는 Layout, Header, Footer, Content 컴포넌트를 사용하여 만들 수 있다.
-   Layout, Header, Footer, Content 컴포넌트는 각각 다음과 같이 만들 수 있다.

### 폴더 이름 가이드

-   컴포넌트를 만들 때, 컴포넌트 이름과 파일 이름을 같게 만들어 주는 것이 좋다.
-   보통 디렉토리 파일명은 소문자로 한다.
-   컴포넌트의 파일 이름은 PascalCase(파스칼 표기법, 대문자로 시작)로 작명한다.
-   Section 같은 불분명한 의미는 짓지 않는다. 명확한 이름으로 표시를 한다. 어쩔수 없이 길어져도 괜찮다.

---

아래 경로로 폴더를 만들어준다.

-   src/components/layout/Header.jsx
-   src/components/layout/Footer.jsx
-   src/components/layout/Layout.jsx

### Header 컴포넌트

-   src/components/layout/Header.jsx

```
import React from 'react';
import { Link } from 'react-router-dom';
import styled from 'styled-components';
import Gnb from './Gnb';
import { Heading } from '@chakra-ui/react';
import DividerCus from '../../common/DividerCus';

const Header = () => {
    return (
        <HeaderWapper>
            <HeaderStyle as="h1" id="logo">
                <Link to="/">
                    <span>horizon</span> free
                </Link>
            </HeaderStyle>
            <DividerCus />
            <Gnb />
        </HeaderWapper>
    );
};

const HeaderStyle = styled(Heading)`
    a {
        display: block;
        transition: color 0.3s ease-in-out;
        text-transform: uppercase;
        text-align: center;
        font-size: 26px;
        /* font-family: 'Poppins', sans-serif; */
        color: var(--primary-dark);
        span {
            font-weight: 700;
        }
        &:hover {
            color: var(--primary);
        }
    }
`;

const HeaderWapper = styled.header`
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 290px;
    padding: 50px 32px;
    background-color: var(--white);
`;

export default Header;
```

-   src/components/layout/Gnb.jsx

```
import React from 'react';
import { Link, useLocation } from 'react-router-dom';
import styled from 'styled-components';
import { AiFillHome, AiOutlineShoppingCart } from 'react-icons/ai';
import { BsBarChartFill } from 'react-icons/bs';

const Gnb = () => {
    const location = useLocation();

    return (
        <GnbWapper>
            <ul>
                <li className={location.pathname === '/' ? 'active' : ''}>
                    <Link to="/">
                        <AiFillHome /> Dashboard
                    </Link>
                </li>
                <li className={location.pathname === '/marketplace' ? 'active' : ''}>
                    <Link to="/marketplace">
                        <AiOutlineShoppingCart />
                        NFT Marketplace
                    </Link>
                </li>
                <li className={location.pathname === '/tables' ? 'active' : ''}>
                    <Link to="/tables">
                        <BsBarChartFill />
                        Tables
                    </Link>
                </li>
                <li className={location.pathname === '/kanban' ? 'active' : ''}>
                    <Link to="/kanban">
                        <BsBarChartFill /> Kanban
                    </Link>
                </li>
                <li className={location.pathname === '/profile' ? 'active' : ''}>
                    <Link to="/profile">
                        <BsBarChartFill /> Profile
                    </Link>
                </li>
                <li className={location.pathname === '/signin' ? 'active' : ''}>
                    <Link to="/signin">
                        <BsBarChartFill /> Sign in
                    </Link>
                </li>
            </ul>

            {/* <ul>
                <li className={location.pathname === '/' ? 'active' : ''}>
                    <Link to="/">홈</Link>
                </li>
                <li className={location.pathname === '/about' ? 'active' : ''}>
                    <Link to="/about">소개</Link>
                </li>
            </ul> */}
        </GnbWapper>
    );
};

const GnbWapper = styled.nav`
    ul {
        li {
            position: relative;
            margin-left: 3px;
            &::after {
                opacity: 0;
                transition: opacity 1s;
            }
            &.active {
                &::after {
                    content: '';
                    position: absolute;
                    top: 50%;
                    right: -32px;
                    transform: translateY(-50%);
                    width: 4px;
                    height: 36px;
                    border-radius: 25px;
                    background: var(--primary);
                    opacity: 1;
                }
                a {
                    color: var(--primary-dark);
                    font-weight: 700;
                    svg {
                        color: var(--primary);
                    }
                }
            }
            a {
                display: flex;
                align-items: center;
                gap: 10px;
                padding: 16px 0;
                color: var(--secondary-grey-600);
                font-weight: 500;
                &:hover {
                    color: var(--primary-dark);
                }
            }
            svg {
                font-size: 20px;
            }
        }
    }
`;

export default Gnb;
```

### Title, History 컴포넌트

-   src/components/common/Title.jsx

```
import React from 'react';
import { VStack, Heading } from '@chakra-ui/react';

const Title = ({ title }) => {
    return (
        <VStack alignItems={'flex-start'} spacing={4}>
            <Heading as={'h2'} fontSize={'34px'} fontWeight={700}>
                {title}
            </Heading>
            {/* <Text variant={'txt164'}>{props.desc}</Text> */}
        </VStack>
    );
};

export default Title;
```

-   src/components/Common/History.jsx

```
import { Link } from 'react-router-dom';
import { Breadcrumb, BreadcrumbItem, BreadcrumbLink } from '@chakra-ui/react';

const History = ({ pagename }) => {
    // const { pagename } = props;
    return (
        <Breadcrumb color="secondary_grey_700" fontSize="14px" fontWeight="500">
            <BreadcrumbItem>
                <BreadcrumbLink as={Link} to="/">
                    Home
                </BreadcrumbLink>
            </BreadcrumbItem>
            <BreadcrumbItem isCurrentPage>
                <BreadcrumbLink as={Link} to={`/${pagename.toLowerCase()}`}>
                    {pagename}
                </BreadcrumbLink>
            </BreadcrumbItem>
        </Breadcrumb>
    );
};

export default History;
```

### Footer 컴포넌트

-   src/components/layout/Footer.jsx

```
import React from 'react';
import styled from 'styled-components';

const Footer = () => {
    return (
        <FooterWrapper>
            <p>footer</p>
        </FooterWrapper>
    );
};

const FooterWrapper = styled.footer`
    display: flex;
    justify-content: center;
    align-items: center;
    height: 70px;
    background-color: #eee;
`;

export default Footer;
```

### Layout 컴포넌트

-   src/components/layout/layout.jsx

```
import React from 'react';
import Header from './header/Header';
import styled from 'styled-components';
import Title from '../common/Tilte';
import History from '../common/History';
import { Box } from '@chakra-ui/react';

const Layout = ({ title, pagename, children }) => {
    // const { pagename, children } = props;
    return (
        <Wrap>
            <Header />
            <main id="main">
                <Box p="0 0 35px 10px">
                    <History pagename={pagename} />
                    <Title title={title} />
                </Box>
                {children}
            </main>
        </Wrap>
    );
};

const Wrap = styled.div`
    display: flex;
    flex-direction: column;
    padding-left: 290px;
    background: var(--secondary-grey-300, #f4f7fe);
    #main {
        min-height: 100vh;
        padding: 50px 20px;
    }
`;

export default Layout;
```

## 2\. Page 만들기

-   src/pages/index.jsx

```
import React from 'react';
import Layout from '../components/layout/Layout';

const Home = () => {
    return (
        <Layout title="DashBoard" pagename="DashBoard">
            Dashboard
        </Layout>
    );
};

export default Home;
```

## 3\. App.js 에서 라우팅하기

-   src/App.js

```
import React from 'react';
import { Route, Routes } from 'react-router-dom';
import Home from './pages';
import { ChakraProvider, CSSReset } from '@chakra-ui/react';
import GlobalStyles from './assets/styles/GlobalStyles.styles';
import theme from './theme/';
import MarketPlace from './pages/MarketPlace';
import Tables from './pages/Tables';
import Kanban from './pages/Kanban';
import Profile from './pages/Profile';
import SignIn from './pages/SignIn';

function App() {
    return (
        <ChakraProvider theme={theme}>
            <CSSReset />
            <GlobalStyles />
            <BrowserRouter>
              <Routes>
                  <Route path="/" element={<Home />} />
                  <Route path="/marketplace" element={<MarketPlace />} />
                  <Route path="/tables" element={<Tables />} />
                  <Route path="/kanban" element={<Kanban />} />
                  <Route path="/profile" element={<Profile />} />
                  <Route path="/signin" element={<SignIn />} />
              </Routes>
            </BrowserRouter>
        </ChakraProvider>
    );
}

export default App;
```
