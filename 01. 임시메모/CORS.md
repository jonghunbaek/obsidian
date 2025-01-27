---
category: 임시 메모
author: 
number: 
tags: 
date: 2025-01-27
from: 
aliases:
---
### 날짜 : 2025-01-27 11:26
### 태그 : CORS

### 메모 
- Spring Boot 3.3.5버전에서 CORS 설정 시 Spring Security에 설정 해줘야 함
- WebConfigurer에 설정하면 작동 안함
- 정확히는 spring security에 설정되어 security의 관리를 받지 않는 url 은 webconfigurer 설정에 영향을 받고, spring security의 관리를 받는 url은 spring security의 cors 설정에 영향을 받음

### 원문 (인용) 

### 생각 (질문) 

### 출처 (인물) 

### 연결 (이유)