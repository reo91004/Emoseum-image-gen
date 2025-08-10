# README.md

# Emoseum

감정 일기 기반 이미지 생성 및 자기 전시 시스템을 활용한 ACT 기반 디지털 치료제

## 📖 프로젝트 소개

Emoseum은 ACT(Acceptance and Commitment Therapy) 이론에 기반한 디지털 치료 시스템이다. 사용자가 작성한 감정 일기를 GPT와 Stable Diffusion을 통해 개인화된 이미지로 시각화하여, 감정 수용과 심리적 유연성을 증진시키는 혁신적인 치료적 경험을 제공한다.

본 시스템은 4단계 ACT 치료 여정(The Moment → Reflection → Defusion → Closure)을 통해 사용자가 자신의 감정을 안전하게 탐색하고 수용할 수 있도록 도우며, 궁극적으로 희망을 찾아가는 과정을 지원한다.

## 📅 개발 기간

**2024년 6월 29일 ~ 8월 14일** (약 7주)

## 👥 개발자 소개

### 팀 구성 및 역할 분담

| 역할           | 개발자 | GitHub                                       | 담당 업무                                                                                                                                      |
| -------------- | ------ | -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **AI 개발**    | 박용성 | [@reo91004](https://github.com/reo91004)     | • GPT 프롬프트 엔지니어링 (이미지 생성, 도슨트)<br>• Stable Diffusion 이미지 생성<br>• GoEmotions VAD 감정 분석<br>• LoRA/DRaFT+ 개인화 시스템 |
| **AI 개발**    | 송인규 | [@enqueue01](https://github.com/enqueue01)   | • GPT 프롬프트 엔지니어링 (이미지 생성, 도슨트)<br>• 안전성 검증 시스템<br>• GPT API 서비스<br>• 비용 추적 및 모니터링                         |
| **백엔드**     | 이선진 | [@Seonjin-13](https://github.com/Seonjin-13) | • FastAPI 서버 구축<br>• MongoDB 데이터베이스 설계<br>• 사용자 관리 시스템<br>• Unity 연동 API                                                 |
| **Unity 개발** | 추성재 | [@qOLOp](https://github.com/qOLOp)           | • 모바일 게임 UI/UX<br>• 미술관 인터페이스<br>• 클라이언트-서버 통신<br>• 게임화 요소 구현                                                     |

## 💻 개발 환경

### 시스템 요구사항

- **OS**: Windows 10/11, macOS 10.15+, Ubuntu 18.04+
- **Python**: 3.8 이상
- **GPU**: CUDA 11.8+ 지원 GPU (권장) 또는 Google Colab
- **메모리**: 최소 8GB RAM
- **Unity**: 2022.3 LTS

### 설치 및 실행

#### 1. 기본 서버 설정

```bash
# 저장소 클론
git clone https://github.com/Emoseum/emoseum-AI.git
cd emoseum-AI

# 가상환경 생성 및 활성화
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 의존성 설치
pip install -r requirements.txt

# 환경 변수 설정
cp .env.example .env
# .env 파일에서 필요한 API 키 설정:
# - OPENAI_API_KEY
# - MONGODB_URI
# - SUPABASE_URL
# - SUPABASE_KEY
```

#### 2. Google Colab GPU 서버 실행 (권장)

Google Colab에서 `tests/colab_server.ipynb`를 실행하여 GoEmotions와 Stable Diffusion 서버를 구동:

1. [Google Colab](https://colab.research.google.com)에서 `tests/colab_server.ipynb` 열기
2. ngrok 인증 토큰 설정
3. 모든 셀 실행
4. 생성된 Public URL을 `config/settings.yaml`에 설정

#### 3. 시스템 실행

```bash
# CLI 모드 실행
python main.py

# FastAPI 서버 실행 (Unity 클라이언트용)
python run_api.py

# 또는 uvicorn으로 직접 실행
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
```

## 🛠 기술 스택

### AI/ML

- **OpenAI GPT-4o-mini**: 프롬프트 생성 및 도슨트 메시지
- **Stable Diffusion 1.5**: 감정 기반 이미지 생성
- **GoEmotions (DistilBERT)**: 28가지 감정 분류 및 VAD 매핑
- **PyTorch**: 딥러닝 프레임워크
- **Transformers**: 자연어 처리
- **LoRA & DRaFT+**: 고급 개인화 모델 학습

### 백엔드

- **FastAPI**: 비동기 웹 프레임워크
- **MongoDB**: 사용자 데이터 및 감정 여정 저장
- **SQLite**: 로컬 비용 추적 및 설정 관리
- **Uvicorn**: ASGI 서버
- **Pydantic**: 데이터 검증

### 인프라

- **Google Colab**: GPU 기반 AI 모델 서빙
- **Supabase**: 이미지 저장 및 관리
- **ngrok**: Colab 서버 터널링
- **Docker**: 컨테이너화 지원

### 프론트엔드

- **Unity 2022.3 LTS**: 모바일 게임 엔진
- **C#**: Unity 스크립팅

## ✨ 주요 기능

### 🎭 ACT 기반 4단계 치료 여정

#### 1. The Moment - 감정 인식

- 자유로운 감정 일기 작성
- GoEmotions 기반 28가지 감정 실시간 분류
- VAD(Valence-Arousal-Dominance) 차원적 감정 분석
- 동적 임계값 기반 의미있는 감정 추출

#### 2. Reflection - 감정 시각화

- GPT 기반 개인화 프롬프트 생성
- Stable Diffusion을 통한 감정 이미지 생성
- 대처 스타일별 맞춤형 시각적 표현
- 1:1 비율 최적화 (모바일 갤러리용)

#### 3. Defusion - 인지적 탈융합

- 방명록 작성을 통한 감정 거리두기
- 작품 제목과 태그를 통한 감정 재구성
- 부정적 사고 패턴 완화
- 감정 객관화 촉진

#### 4. Closure - 희망 발견

- GPT 기반 개인화 도슨트 메시지
- 치료적 통찰과 격려 제공
- 미래 지향적 시각 형성
- 긍정적 재구성 지원

### 🧠 GoEmotions VAD 감정 분석 시스템

#### 28가지 감정 분류

- **긍정 감정(12개)**: admiration, amusement, approval, caring, excitement, gratitude, joy, love, optimism, pride, relief
- **부정 감정(11개)**: anger, annoyance, disappointment, disapproval, disgust, embarrassment, fear, grief, nervousness, remorse, sadness
- **모호한 감정(5개)**: confusion, curiosity, desire, realization, surprise
- **중립(1개)**: neutral

#### VAD 차원 매핑

- **Valence(쾌-불쾌)**: 감정의 긍정/부정 정도 (0.1~0.9)
- **Arousal(각성)**: 감정의 활성화 수준 (0.25~0.85)
- **Dominance(통제감)**: 감정에 대한 통제 수준 (0.2~0.8)

#### 동적 감정 분석

```python
# 적응적 임계값 계산
adaptive_threshold = max(0.1, min(0.4, mean_score * 0.6))

# 감정 강도 계산 (arousal + score 결합)
intensity = ["low", "medium", "high"]

# 가중치 기반 VAD 통합
weighted_vad = Σ(emotion_vad * √score) / Σ(√score)
```

### 🎯 3단계 개인화 시스템

#### Level 1: 기본 프로파일링

- **심리검사 통합**:
  - PHQ-9: 우울증 선별
  - CES-D: 우울 증상 평가
  - MEAQ: 경험 회피 측정
  - CISS: 대처 스타일 분석
- **대처 스타일 분류**:
  - 회피형: 부드러운 은유적 표현
  - 직면형: 직접적이고 진솔한 표현
  - 균형형: 적응적 혼합 접근
- **시각적 선호도**:
  - 화풍: realistic, anime, abstract, impressionist
  - 색감: warm, cool, vibrant, muted
  - 복잡도: simple, moderate, complex

#### Level 2: GPT 기반 실시간 학습

- 방명록 반응 데이터 수집 및 분석
- 메시지 참여도 측정 (읽기 시간, 재방문율)
- 감정 변화 패턴 추적
- 실시간 프롬프트 조정

#### Level 3: 고급 AI 개인화

- **LoRA 훈련** (50개 이상 긍정 반응):
  - 사용자별 이미지 스타일 학습
  - 개인화된 시각적 표현 생성
- **DRaFT+ 강화학습** (30개 이상 완성 여정):
  - 도슨트 메시지 최적화
  - 치료적 효과 극대화

### 🏛 디지털 미술관

- 개인 감정 여정 아카이브
- 시간순 감정 변화 시각화
- 작품별 상세 정보 (일기, 감정, 방명록, 도슨트)
- 과거 작품 재감상 및 재해석
- 감정 패턴 분석 대시보드

### 🛡 안전성 시스템

- **다층 안전 필터링**:
  - 자해/자살 관련 키워드 감지
  - 폭력적 콘텐츠 차단
  - 치료적 부적절 응답 필터링
- **위기 대응 시스템**:
  - 고위험 상황 자동 감지
  - 전문가 상담 즉시 권유
  - 응급 연락처 제공
- **YAML 기반 규칙 관리** (`config/safety_rules.yaml`)

## 🏗 프로젝트 아키텍처

### 시스템 구조

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Unity Client  │    │  FastAPI Server │    │  AI/ML Engine   │    │   Colab GPU     │
│                 │    │                 │    │                 │    │                 │
│ • Game UI       │◄──►│ • RESTful API   │◄──►│ • GPT Service   │◄──►│ • GoEmotions    │
│ • Gallery View  │    │ • User Manager  │    │ • Emotion Analyzer│   │ • Stable Diff   │
│ • Mobile UX     │    │ • Data Storage  │    │ • Personalization│   │ • VAD Mapping   │
└─────────────────┘    └─────────────────┘    └─────────────────┘    └─────────────────┘
```

### 모듈 구조

```
emoseum-AI/
├── api/
│   └── main.py                    # FastAPI 서버 엔트리포인트
├── src/
│   ├── core/
│   │   └── act_therapy_system.py  # ACT 치료 시스템 통합 코어
│   ├── managers/
│   │   ├── user_manager.py        # 사용자 프로필 및 심리검사
│   │   ├── gallery_manager.py     # 감정 여정 데이터 관리
│   │   └── personalization_manager.py # 3단계 개인화 엔진
│   ├── services/
│   │   ├── gpt_service.py         # OpenAI GPT API 통합
│   │   ├── emotion_analyzer.py    # GoEmotions VAD 분석
│   │   └── image_generator.py     # Stable Diffusion 서비스
│   ├── therapy/
│   │   ├── prompt_architect.py    # 대처 스타일별 프롬프트
│   │   └── docent_message.py      # 치료적 도슨트 메시지
│   ├── training/
│   │   ├── lora_trainer.py        # LoRA 개인화 훈련
│   │   └── draft_trainer.py       # DRaFT+ 강화학습
│   └── utils/
│       ├── safety_validator.py    # 안전성 검증 시스템
│       └── cost_tracker.py        # API 비용 모니터링
├── config/
│   ├── settings.yaml              # 시스템 설정
│   ├── gpt_prompts.yaml          # GPT 프롬프트 템플릿
│   └── safety_rules.yaml        # 안전 규칙 정의
├── tests/
│   ├── colab_server.ipynb       # Google Colab GPU 서버
│   └── test.py                  # 통합 테스트
└── main.py                       # CLI 인터페이스
```

### 데이터 흐름

```
감정 일기 입력
    ↓
GoEmotions 28가지 감정 분류
    ↓
VAD 차원 매핑 및 강도 계산
    ↓
대처 스타일별 프롬프트 생성 (GPT)
    ↓
개인화 이미지 생성 (Stable Diffusion)
    ↓
방명록 작성 (Defusion)
    ↓
도슨트 메시지 생성 (GPT)
    ↓
개인화 데이터 학습 및 업데이트
```

### 데이터베이스 스키마

#### MongoDB Collections

- **users**: 사용자 기본 정보 및 심리검사 결과
  - user_id, username, psychometric_results, coping_style, visual_preferences
- **gallery_items**: 감정 여정 전체 데이터
  - item_id, user_id, diary_text, emotions, vad_scores, image_url, guest_book, docent_message, created_at
- **personalization_data**: 개인화 학습 데이터
  - user_id, interaction_history, positive_reactions, journey_completions, lora_status, draft_status

#### SQLite Tables

- **cost_tracking**: API 사용량 및 비용 추적
- **user_preferences**: 로컬 사용자 설정

## 📡 API 엔드포인트

### FastAPI 서버

```python
# 사용자 관리
POST   /api/v1/users/register      # 사용자 등록
GET    /api/v1/users/{user_id}     # 사용자 정보 조회
PUT    /api/v1/users/{user_id}     # 사용자 정보 수정

# ACT 치료 여정
POST   /api/v1/therapy/analyze     # 감정 분석 (GoEmotions + VAD)
POST   /api/v1/therapy/generate    # 이미지 생성 (Stable Diffusion)
POST   /api/v1/therapy/guest-book  # 방명록 작성
POST   /api/v1/therapy/docent      # 도슨트 메시지 생성

# 갤러리 관리
GET    /api/v1/gallery/{user_id}   # 사용자 갤러리 조회
GET    /api/v1/gallery/item/{id}   # 개별 작품 조회
DELETE /api/v1/gallery/item/{id}   # 작품 삭제

# 개인화
GET    /api/v1/personalization/{user_id}/status  # 개인화 레벨 조회
POST   /api/v1/personalization/{user_id}/update  # 개인화 데이터 업데이트
```

### Colab GPU 서버

```python
# GoEmotions 감정 분석
POST   /analyze_emotion
{
    "text": "오늘은 정말 힘든 하루였다...",
    "threshold": 0.3  # 선택적, 동적 threshold 사용
}

# Stable Diffusion 이미지 생성
POST   /generate
{
    "prompt": "A peaceful garden with soft morning light...",
    "width": 512,
    "height": 512
}

# 헬스 체크
GET    /health
```

## 🔬 연구적 가치

### 혁신성

- **ACT 이론의 디지털 구현**: 검증된 심리치료를 모바일 환경으로 전환
- **멀티모달 AI 통합**: 텍스트(GPT) + 이미지(SD) + 감정(GoEmotions)
- **적응적 개인화**: 사용자 반응 기반 실시간 학습
- **게임화 치료**: 미술관 메타포를 통한 치료 접근성 향상

### 주요 연구 질문

1. **감정 시각화의 치료적 효과**: VAD 기반 이미지 생성이 감정 수용에 미치는 영향
2. **대처 스타일별 차별화**: 회피형/직면형/균형형 접근의 효과성 비교
3. **인지적 탈융합 메커니즘**: 방명록 시스템의 심리적 거리두기 효과
4. **개인화 수준의 영향**: Level 1-3 개인화가 치료 성과에 미치는 차이

### 임상적 검증 계획

- IRB 승인 후 파일럿 연구 (n=30)
- PHQ-9, CES-D 사전/사후 평가
- 4주간 일일 사용 프로토콜
- 정성적 인터뷰 및 사용성 평가

### 확장 가능성

- **다양한 정신건강 영역**: 불안장애, PTSD, 조절장애 적용
- **연령별 맞춤화**: 아동/청소년/노인 특화 버전
- **집단 치료 프로그램**: 메타버스 공동 전시 공간
- **의료 시스템 통합**: 전자건강기록(EHR) 연동

## 📈 성능 및 최적화

### 응답 시간

- 감정 분석: ~500ms (GoEmotions)
- 이미지 생성: ~30s (Stable Diffusion on Colab T4)
- 도슨트 메시지: ~2s (GPT-4o-mini)

### 확장성

- FastAPI 비동기 처리로 동시 사용자 100명 지원
- MongoDB 샤딩 준비
- 마이크로서비스 아키텍처 전환 가능

---
