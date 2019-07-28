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
2. emotion方法
```
/** @jsx jsx */ 这一行不能省略
import React from "react";
import { jsx } from "@emotion/core";

export default function X(props) {
  const theme = props.theme;
  return (
    <div
      css={{
        display: "flex",
        alignItems: "center",
        background: theme,
        padding: 10
      }}
    >
      <div
        css={{
          display: "inline-block",
          color: "red",
          fontSize: 20,
          white: 40,
          height: 40,
          background: "grey"
        }}
      >
        logo
      </div>
      <nav
        css={{
          width: 200,
          height: 30,
          background: "#333",
          marginLeft: 10
        }}
      />
    </div>
  );
}

```
- 普通应用使用 styled-components 和 css modules，因为类名会变成随机字符串
- 库使用传统 CSS 方式，因为类名不会变成随机字符串
