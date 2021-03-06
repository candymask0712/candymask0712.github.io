---
title: "[Git] Git의 기본 사용법 1 - 버전관리  "
excerpt: 
toc: true
toc_sticky: true
toc_label: "페이지 컨텐츠 리스트"
categories:
  - Git
tags:
  - version
last_modified_at:
---
### **1. Git이란**
- 소스코드 기록을 관리/추적하는 버전 관리 시스템
- 크게 버전 관리/백업/협업 용도로 사용
- Github : 클라우드 기반 git repository 관리 서비스

### **2. Git 관련 주요개념**

1. Git Repository : 파일/폴더를 저장하는 저장소
  - Local Repository : 내 컴퓨터의 개인 저장소
  - Remote Repository : 원격 온라인 저장소(타인과 공유가능)

2. 깃에서 버젼을 만드는 단계  
   - 작업트리 : 눈에 보이는 디렉터리
   - 스테이지 : 버전으로 만들 파일이 대기
   - 저장소 : 파일을 버전으로 만들어 저장

### **3. 버전관리**

  1. git init : 깃 초기화
      - git 저장소를 만들 디렉토리에서 깃 초기화
      - 해당 디렉토리의 파일 버전관리 가능
      - 디렉토리 내에 .git 디렉토리 생성됨(숨김처리)
        : shift + cmd + . 을 눌러 숨김파일 보기 가능

  2. git add 파일/폴더명 : 스테이징
      - 스테이지에 파일을 추가

  3. git commit -m "내용" : 커밋
      - 추가된 파일의 버젼관리를 위한 메세지 기록

  4.  git commit -am : 스테이징 + 커밋
      - 스테이징과 커밋을 한 번에 처리
      - 한 번이라도 커밋한 적이 있는 파일 대상
  
### **4. 기록 확인하기**

  1. git log : 커밋 기록 확인
      - 커밋해시 : 커밋을 구별하는 ID
      - (HEAD -> master) : 최신 버전임을 표시

  2. git diff : 변경 사항 확인
      - 작업트리/스테이지/저장소 파일 비교
      - 최근 버전과 비교하여 다른 부분을 알려줌

  3. git status : 깃 상태 표시
      - 브랜치/커밋한 파일/커밋 대상 파일 표시
