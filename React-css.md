1. styled-components方式
```
import React from "react";
import cn from "classnames";
import styled from "styled-components";

export default function Topbar(props) {
  const theme = props.theme; // 'white | black'

  const onClick = () => {
    console.log(1);
  };
  const Logo = styled.div`
    width: 40px;
    height: 40px;
    background: grey;
  `;
  const Nav = styled.nav`
    height: 30px;
    background: #333;
    width: 200px;
    color: white;
    margin-left: 10px;
  `;
  const Wrapper = styled.div`
    display: flex;
    align-items: center;
    border: 1px solid black;
    padding: 10px;
    background: ${theme};
  `;
  return (
    <Wrapper>
      <Logo>logo</Logo>
      <Nav>nav</Nav>
    </Wrapper>
  );
}
```
- 普通应用使用 styled-components 和 css modules，因为类名会变成随机字符串
- 库使用传统 CSS 方式，因为类名不会变成随机字符串
