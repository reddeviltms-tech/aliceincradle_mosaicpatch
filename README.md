# 🤖 Pathfinder - Language Model

Transformer 기반 한국어 언어 모델입니다. 텍스트를 학습하고 생성하는 능력을 갖춘 AI입니다.

---

## 📋 오늘의 작업 (2026년 9월 12일)

### 1️⃣ Transformer 모델 아키텍처 구축 (06-1 ~ 06-6)
- **ModelConfig**: 모델 설정 (vocab_size=128, d_model=512, n_layers=8 등)
- **SelfAttention**: Multi-Head Attention 구현
- **FeedForward**: 2층 신경망 (d_model → d_ff → d_model)
- **TransformerBlock**: Attention + FFN + Residual Connection + LayerNorm 조합
- **Pathfinder**: 8개 블록을 쌓은 완전한 Transformer 모델

### 2️⃣ 위치 정보 & 정규화 추가 (06-7 ~ 06-8)
- **PositionalEncoding**: Sin/Cos 위치 인코딩으로 시퀀스 정보 포함
- **Dropout**: 정규화로 과적합 방지 (dropout_rate=0.1)

### 3️⃣ 훈련 시스템 구축 (06-9)
- **TextDataset**: 토큰 ID를 context_length 길이 윈도우로 변환
- **DataLoader**: 배치 로딩 (batch_size=4)
- **완전한 훈련 루프**: 3개 epoch 실행
  - **Epoch 1**: Loss 1.9177
  - **Epoch 2**: Loss 0.3524
  - **Epoch 3**: Loss 0.1445 ✅ (수렴 완료)

### 4️⃣ 모델 저장 & 복원 (06-10)
- **체크포인트 저장**: 모델 가중치, 옵티마이저 상태, 설정 정보 저장
- **파일**: `checkpoints/maehwa_model.pt`

### 5️⃣ 추론 기능 (06-11)
- **inference.py**: 저장된 모델 로드 후 텍스트 생성
- **generate_text()**: 프롬프트 기반 텍스트 샘플링 생성

### 6️⃣ 모델명 변경
- **MaehwaAI** → **Pathfinder**
- 모든 파일에서 클래스명 및 import 업데이트

### 7️⃣ 대화형 인터페이스 추가
- **chat.py**: 사용자 입력을 받아 실시간 응답 생성
- 'quit' / 'exit' 입력으로 종료 가능

### 8️⃣ 훈련 데이터 업그레이드
- **이전**: 8개 문장 (약 200 토큰)
- **현재**: 40개 문장 (다양한 주제 + 대화 스타일)
  - 철학, 역사, 문학, 과학, 수학 등
  - 일상 대화, 캐릭터 대사, 감정 표현
  - 동양 문화 요소 (매화, 대나무, 난초 등)

### 9️⃣ 재훈련 진행 중 🔄
- 40개 문장으로 **재훈련** 중
- 반복 문제 해결 예정

---

## 📂 프로젝트 구조

```
maehwa-ai/
├── model/
│   ├── model.py          # Pathfinder 모델 정의
│   └── __init__.py       # 모듈 export
├── training/
│   └── train.py          # 훈련 스크립트
├── inference/
│   └── inference.py      # 추론 (배치 테스트)
├── chat/
│   └── chat.py           # 대화형 인터페이스
├── data/
│   └── corpus.txt        # 훈련 데이터 (40개 문장)
├── checkpoints/
│   └── maehwa_model.pt   # 저장된 모델 가중치
├── dataset.py            # TextDataset 클래스
└── tokenizer/
    └── maehwa.model      # SentencePiece 토크나이저
```

---

## 🚀 사용 방법

### 1️⃣ 훈련
```bash
python training/train.py
```

### 2️⃣ 대화형 채팅
```bash
python chat/chat.py
```

**예시:**
```
👤 You: 안녕!
🤖 Pathfinder: 안녕하세요. 함께 나아갑시다...

👤 You: 너는 누야?
🤖 Pathfinder: 나는 Pathfinder입니다. 길을 찾는 AI입니다...

👤 You: quit
```

### 3️⃣ 배치 추론
```bash
python inference/inference.py
```

---

## 📊 모델 사양

| 항목 | 값 |
|------|-----|
| **모델명** | Pathfinder |
| **구조** | Transformer |
| **Vocab Size** | 128 |
| **Context Length** | 1024 |
| **Hidden Dim (d_model)** | 512 |
| **Attention Heads** | 8 |
| **FFN Dim (d_ff)** | 2048 |
| **Layers** | 8 |
| **Dropout Rate** | 0.1 |
| **Optimizer** | Adam (lr=0.001) |
| **Loss Function** | CrossEntropyLoss |

---

## 🎯 현재 상태

✅ **완료:**
- Transformer 모델 완성
- 훈련 & 저장/로드 시스템
- 대화형 인터페이스
- 데이터 업그레이드

🔄 **진행 중:**
- 40개 문장으로 재훈련 중

❓ **다음 할 수 있는 것:**
- 웹 UI 추가
- API 서버 구축
- 더 큰 데이터셋 적용
- 모델 최적화

---

## 📝 기술 스택

- **Deep Learning**: PyTorch
- **Tokenizer**: SentencePiece
- **Python**: 3.14
- **GPU**: CUDA (RTX 2080)

---

## 🎓 학습 내용

이 프로젝트를 통해 다음을 학습했습니다:

1. **Transformer 아키텍처**: Self-Attention, Multi-Head Attention, Feed Forward
2. **위치 인코딩**: Sin/Cos 기반 위치 정보 포함
3. **모델 훈련**: 손실 함수, 역전파, 최적화
4. **텍스트 생성**: 샘플링, Temperature 조절
5. **체크포인트**: 모델 저장 & 복원
6. **대화형 시스템**: 실시간 추론

---

**작성일**: 2026년 9월 12일  
**상태**: 🔄 재훈련 진행 중
