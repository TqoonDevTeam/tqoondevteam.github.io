---
title: "개발 가이드 템플릿"
description: "문서 설명"
tags: [개발가이드, 템플릿 ]
---

# 작업 전후 Git 환경 설정
운영 업무 시 코드 작업 전후 Visual Studio에서 Git 환경 설정하는 방법입니다.

[ pull, commit, push, pullrequset ]

## 코드 수정 작업 전 ( Pull )

1. 해당 프로젝트 최신버전을 패치 >> 끌어오기 후 빌드를 하여 오류가 없는지 확인하고 작업을 진행  합니다.

2. 개발은 master 브랜치에서 코드 (`패치 및 끌어오기`) 를 가져옵니다.

![image](https://user-images.githubusercontent.com/40411714/146315846-abe21f3d-f49c-4ce8-9fe8-0ae28bf089ab.png)

## 코드 수정 작업 후 (Commit, Push)

1. 분기 » `ex)bugfix/이니셜/레드마인번호_작업내용` 형식의 브랜치를 생성하고 활성화 시킵니다.
2. 변경 내용을 확인 후 ( commit , push 또는 게시 ) 합니다
   * 분기 확인 후 진행합니다.

![image](https://user-images.githubusercontent.com/40411714/146316226-8031ce06-1a1e-4b1b-bff4-35604bc66691.png)

## Pull Request

1. 게시 한 브랜치 이름 확인.

2. Pull request 작성 화면으로 이동.

3. `master` <- `본인 브랜치`인지 확인.

4. pull request 요청 페이지로 이동 

5. 주소를 가지고 코드리뷰 요청 및 배포신청 시 사용합니다.

  ![image](https://user-images.githubusercontent.com/40411714/146316451-02cb6f69-9851-4a6e-b954-a283591c5742.png)
