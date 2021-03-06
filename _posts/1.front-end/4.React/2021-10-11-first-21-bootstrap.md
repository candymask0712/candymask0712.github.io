---
title: "[React] Bootstrap 사용법"
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - Bootstrap
  - JavaScript
last_modified_at:
---

### **Bootstrap 시작**

1. react-bootstrap 시작페이지 접속 후 따라하기
   https://react-bootstrap.github.io/getting-started/introduction

- tip : npm install 로 되어 있는 명령어는 yarn add로 바꾸면 편하고 빠르게 설치 가능

2. 같은 페이지에 있는 CSS link 내용을 내 프로젝트 index.css 파일에 붙여넣기(public 또는 src폴더)  
   Tip. 차이점: src에 넣을 시 압축 됨, public에 넣을 시 절대경로

3. Bootstrap 사이트 docs에서 원하는 내용 검색 후 붙여넣기
   https://getbootstrap.com/

4. 가져온 내용 import 하기 (대문자로 시작하는 내용)

```javascript
import { Navbar, Container } from "react-bootstrap";
// import 내용의 예시
```

### **Bootstrap의 두가지 사용법**

1. React-bootstrap 설치 후 원하는 docs 복붙하기

```javascript
<Navbar bg="light" expand="lg">
  <Container>
    <Navbar.Brand href="#home">ShoeShop</Navbar.Brand>
    <Navbar.Toggle aria-controls="basic-navbar-nav" />
    <Navbar.Collapse id="basic-navbar-nav">
      <Nav className="me-auto">
        <Nav.Link href="#home">Home</Nav.Link>
        <Nav.Link href="#link">Link</Nav.Link>
        <NavDropdown title="Dropdown" id="basic-nav-dropdown">
          <NavDropdown.Item href="#action/3.1">Action</NavDropdown.Item>
          <NavDropdown.Item href="#action/3.2">Another action</NavDropdown.Item>
          <NavDropdown.Item href="#action/3.3">Something</NavDropdown.Item>
          <NavDropdown.Divider />
          <NavDropdown.Item href="#action/3.4">Separated link</NavDropdown.Item>
        </NavDropdown>
      </Nav>
    </Navbar.Collapse>
  </Container>
</Navbar>
```

2. 원조 Bootstrap 설치 후 class명 가져다 쓰기 (css사이즈가 커지는 단점)

- PC웹에서는 가로로, 모바일웹에서는 세로로 나열되는 코드 예시

```javascript
<div className="container">
  <div className="row">
    <div className="col-md-4">asdfasdf</div>
    <div className="col-md-4">asdfasdf</div>
    <div className="col-md-4">asdfasdf</div>
  </div>
</div>
```
