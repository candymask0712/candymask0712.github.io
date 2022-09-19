---
title: "[React] lazy-import"
excerpt:
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - React
tags:
  - React-Query
last_modified_at:
---

## lazy-import란?

- SPA 특성상 빌드 시 하나의 js 파일로 변환 됨
- 하나의 파일에 모든 내용이 들어 있어 첫 페이지 로딩이 느려짐
- 메인페이지에서 활용하지 않는 페이지의 내용은 lazy-import 해오도록 처리 가능