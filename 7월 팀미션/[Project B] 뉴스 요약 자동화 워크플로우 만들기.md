# AI 뉴스 요약 자동화 프로젝트

## 1. 프로젝트 개요
이 프로젝트는 RSS로 수집한 뉴스 데이터를 자동으로 가져와, Gemini AI를 이용해 핵심 내용을 요약한 뒤 Notion 데이터베이스에 저장하는 자동화 시스템입니다.  
Make를 활용하여 뉴스 수집, 중복 검사, AI 요약 생성, Notion 저장까지의 과정을 하나의 시나리오로 구성했습니다.

---

## 2. 프로젝트 목표
- 관심 키워드 기반 뉴스 자동 수집
- 중복 뉴스 저장 방지
- AI를 활용한 뉴스 요약 자동 생성
- Notion을 활용한 뉴스 아카이빙 자동화

---

## 3. 사용 도구
- **Make**: 자동화 시나리오 구성
- **Google Gemini API**: 기사 요약 생성
- **Notion Database**: 결과 저장 및 관리

---

## 4. 자동화 흐름
전체 시나리오는 다음과 같은 순서로 동작합니다.

1. 매일 오후 6시 RSS에서 뉴스 기사 수집
2. Notion 데이터베이스에서 동일한 원문 링크가 이미 존재하는지 검색
3. 중복이 아니면 Gemini API를 호출하여 기사 요약 생성
4. 제목, 요약, 원문 링크, 발행일을 Notion에 저장
5. 오류 발생 시 Retry에 따라 재시도

### 시나리오 구조

<img width="1911" height="991" alt="image" src="https://github.com/user-attachments/assets/b6633736-1eec-4748-bef3-4c788e3da08b" />



---

## 5. Notion 데이터베이스 구성
본 프로젝트에서는 아래 4개의 속성을 사용했습니다.

| 속성명 | 타입 | 설명 |
|---|---|---|
| 제목 | Title | 뉴스 기사 제목 |
| 요약 | Text | Gemini가 생성한 요약문 |
| 원문링크 | URL | 뉴스 원문 주소 |
| 발행일 | Date | 기사 발행일 |

---

## 6. 핵심 기능

### 6-1. RSS 뉴스 수집
RSS 모듈을 통해 지정한 뉴스 피드에서 최신 기사를 자동으로 가져오도록 설정했습니다.

### 6-2. 중복 필터링
Notion의 `Search Objects` 모듈을 사용하여,  
이미 저장된 기사와 **원문링크(URL)** 가 동일한 경우 저장하지 않도록 구성했습니다.

- 중복 기준: `원문링크`
- 목적: 동일 기사 반복 저장 방지

### 6-3. AI 요약 호출
Gemini API를 활용하여 수집한 뉴스 기사 내용을 자동으로 요약하도록 구성했습니다.

#### 적용 여부
- [x] 기사 내용을 기반으로 Gemini에 요약 요청
- [x] Gemini 응답 결과를 Notion의 `요약` 속성에 저장
- [x] 실행 기록에서 요약 생성 결과 확인 완료


### 6-4. Notion 자동 저장
중복이 아닌 기사에 대해서만 제목, 요약, 원문링크, 발행일이 Notion 데이터베이스에 자동 저장되도록 구현했습니다.

---

## 7. 에러 처리 정책
자동화 과정에서 외부 API 또는 네트워크 문제로 인해 일시적인 오류가 발생할 수 있으므로, 아래와 같이 에러 처리 정책을 적용했습니다.

### 적용한 정책
- **Retry 에러 핸들러 사용**
- **재시도 횟수: 2회**
- **재시도 간격: 5분**

### 기대 효과
- 실행 중단 시 원인 추적 가능
- 자동화 안정성 향상

---

## 8. 키워드
본 프로젝트는 AI 기술 관련 뉴스 요약 자동화를 목표로 하였으며,  
빠르게 변화하는 기술 트렌드를 효율적으로 파악하기 위해 관련 뉴스 키워드를 중심으로 구성했습니다.

### 선정 이유
- AI 및 IT 분야는 최신 이슈 변화 속도가 빠름
- 많은 기사를 직접 읽지 않고도 핵심 내용을 빠르게 확인 가능
- 요약 데이터를 Notion에 누적하여 개인/팀 지식 관리에 활용 가능

> 키워드: AI, Gemini, OpenAI, 생성형 AI, 빅테크, 반도체 등  

---

## 9. 팀 역할


| 이름 | 역할 |
|---|---|
| 손재형 | Make 시나리오 설계 |
| 김규리 | 테스트 및 오류 검토 |
| 박현준 | 보고서 작성 |



## 10. 기능 검증 결과

### 검증 항목 체크리스트
- [x] RSS 뉴스 수집 정상 동작
- [x] Notion 데이터베이스 연동 성공
- [x] Gemini 요약 생성 성공
- [x] 중복 기사 필터링 적용
- [x] URL 매핑 정상 동작
- [x] 최종 테스트 성공

### 최종 결과
RSS에서 수집한 뉴스가 Gemini를 통해 요약된 뒤,  
중복 여부를 확인하고 Notion 데이터베이스에 자동 저장되는 전체 흐름이 정상적으로 동작함을 확인했습니다.

---

## 11. 실행 화면


### Make 시나리오
<img width="1911" height="991" alt="스크린샷 2026-08-03 175701" src="https://github.com/user-attachments/assets/3afccb4a-effe-4d3a-827a-a702e946921e" />
<img width="808" height="944" alt="스크린샷 2026-08-03 173700" src="https://github.com/user-attachments/assets/9a282447-40b9-428c-80c1-06251e52081f" />
<img width="796" height="852" alt="스크린샷 2026-08-03 173710" src="https://github.com/user-attachments/assets/f1c2a3ad-9519-4765-93a7-c89224cb49f4" />
<img width="788" height="330" alt="스크린샷 2026-08-03 173730" src="https://github.com/user-attachments/assets/496f50d5-3609-4349-a80c-209a4c04d585" />
<img width="808" height="545" alt="스크린샷 2026-08-03 173738" src="https://github.com/user-attachments/assets/9330c9fb-7d55-44ef-a7ec-d0cf445eee0e" />
<img width="800" height="629" alt="스크린샷 2026-08-03 173816" src="https://github.com/user-attachments/assets/5281bb0a-0361-446d-9c67-6d4826cf7517" />
<img width="809" height="508" alt="스크린샷 2026-08-03 173839" src="https://github.com/user-attachments/assets/acefd3cb-6764-406c-994e-86ae7d5b0041" />
<img width="764" height="235" alt="스크린샷 2026-08-03 173843" src="https://github.com/user-attachments/assets/0a71fa0e-40c7-4b88-b017-59ae0811a1c7" />
<img width="813" height="975" alt="스크린샷 2026-08-03 173850" src="https://github.com/user-attachments/assets/de5ff7b3-a84c-4c77-86a4-febeb53a4fda" />

### 실행 결과
<img width="2005" height="1000" alt="스크린샷 2026-08-03 180101" src="https://github.com/user-attachments/assets/40a64946-52cc-4b0a-8d2a-ff2c31daeedd" />



### Notion 저장 결과
<img width="2510" height="1144" alt="image" src="https://github.com/user-attachments/assets/7e87ff75-175a-4681-9a7f-0feace5dee30" />





---


이번 프로젝트를 통해 단순 뉴스 수집을 넘어,  
AI 요약 기능과 데이터베이스 저장을 결합한 실용적인 자동화 시스템을 구현할 수 있었습니다.

특히 다음과 같은 점을 확인할 수 있었습니다.

- 반복적인 정보 수집 업무를 자동화할 수 있음
- AI 요약 기능을 통해 정보 소비 시간을 줄일 수 있음
- Notion과 연계하여 체계적인 뉴스 아카이빙이 가능함
- 예외 처리와 중복 방지 설계가 자동화 품질에 매우 중요함

---

## 13. 향후 개선 방향
- 뉴스 카테고리별 분류 기능 추가
- 요약 품질 향상을 위한 프롬프트 개선
- 특정 키워드 포함 시 알림 기능 추가
- 요약 호출 횟수 및 사용량 로그 저장 기능 추가
