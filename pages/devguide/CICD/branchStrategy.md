---
title: "개발 가이드 템플릿"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---

# 브랜치 전략

> 티쿤글로벌의 개발부서에서 어떻게 브랜치를 관리하고 있는지 소개하는 글입니다.

## 브랜치 종류

- master - 운영환경에 배포되는 브랜치

- hotfix - 긴급오류 수정용 브랜치

- dev - 그룹/피쳐 브랜치 통합 브랜치

- bugfix - 일반오류 수정용 브랜치

- feature - 이슈별 기능 개발 브랜치


## 브랜치 플로우

>![branch](./img/branch1.png){: width="45%" height="70%"}

>> hotfix 브랜치는 운영환경에서 긴급하게 수정해야 하는 오류사항이 생겼을 때, 빠른 수정을 하기 위한 용도로 사용됩니다. 
master에서 hotfix 브랜치를 생성한 뒤 작업을 합니다.  작업이 끝나면 master로 배포 요청합니다.

>>dev 브랜치는 개발시 사용되는 메인 브랜치입니다. 마스터의 병렬 브랜치로, master 브랜치에 커밋 이벤트 발생시, dev 브랜치로 자동 병합됩니다.
dev 브랜치에는 bugfix 와 feature 브랜치들이 병합됩니다. dev 브랜치에서는 공통작업업무(ex. 결제, 다운로드 등)를 테스트를 합니다.

>>bugfix 와 feature 는 이슈나, 추가 작업이 있는 경우 dev 브랜치에서 생성하여 작업합니다.
각 브랜치에서 작업과 테스트를 마치면, dev 브랜치로 배포요청을 합니다. 

## 브랜치 네이밍

* 브런치 생성 규칙은 **[브런치 종류](#브랜치 종류)/이니셜/이슈번호_이슈내용**

  * ex ) bugfix/ahg/12345_이슈내용

  ![image](https://user-images.githubusercontent.com/40411714/146316800-4f1d95b4-7191-4956-8d84-b7514217f9d8.png)

## commit 규칙

* **화면단 백단별** / **기능별**로 commit할 것을 권장

* 각 commit마다 **이슈번호_commit내용**으로 commit

  * ex ) 12345 회원가입 개발 완료

  ![image](https://user-images.githubusercontent.com/40411714/146317354-0c4e60e8-c267-474c-8a81-d1ddd9b5dc0c.png){}