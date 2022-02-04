---
date: '2022-01-06'
title: 'Virtual DOM'
categories: ['React', 'TIL', 'Virtual-DOM']
summary: 'Virtual DOM에 대해서 알아보자'
thumbnail: './test.jpeg'
---

# Virtual DOM이란?

## DOM

문서 객체 모델로 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는 역할을 한다.

## Virtual DOM Work

- 데이터가 업데이트 되면 전체 UI를 Virtual Dom에 리렌더링 한다.
- 이전 Virtual Dom에 있던 내용과 현재의 내용을 비교한다.
- 바뀐 부분만 실제 DOM에 적용시킨다.
