# 🔔 실시간 데이터 연동형 스마트 골든벨 빙고 시스템
> **공항성산교회 중등부 여름수련회**를 위해 개발된 실시간 쌍방향 퀴즈 및 5x5 DIY 빙고 결합 플랫폼입니다.  
> 본 프로젝트는 **Firebase Realtime Database**를 기반으로 마스터(진행자) 화면과 모바일(학생 조별) 화면이 100% 실시간 동기화되어 작동합니다.

---

## 🚀 서비스 아키텍처 및 환경
* **Frontend**: Vanilla JS, HTML5, CSS3 (Flexible Mobile UI)
* **Backend / Database**: Google Firebase Realtime Database (Spark Free Plan)
* **Hosting**: GitHub Pages (정적 웹 호스팅)
* **CI/CD**: GitHub Actions (`Workflow permissions: Read and write` 자동 배포 완비)

---

## 🛠 데이터베이스 트리 구조 (Firebase RTDB)

```json
{
  "game": {
    "currentQuestion": 0,       // 현재 활성화된 문제 번호 (0: 대기, 1~25)
    "currentQuestionText": "",  // 실시간 출제된 퀴즈 본문 텍스트
    "currentCategory": "",      // 퀴즈 카테고리 (성경, TMI, 넌센스 등)
    "currentDifficulty": "",    // 난이도 (최상, 상, 중, 하)
    "status": "waiting"         // 게임 상태 ('waiting', 'playing', 'showing_answers')
  },
  "teams": {
    "team_id": {                // 1조 ~ 5조 (총 5개 조)
      "bingoBoard": [ ],        // 조별로 DIY 배치 완료한 5x5 빙고판 배열 (1~25)
      "answers": {
        "question_id": ""       // 학생들이 실시간 입력 및 제출한 단답형 정답
      },
      "occupied_cells": {
        "question_id": true     // 정답 인정(점령 성공) 여부 -> true 시 빙고판 불 켜짐
      }
    }
  }
}
