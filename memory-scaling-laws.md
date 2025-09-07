# Memory기반 scaling laws 

## LLM의 문제점
- LLM은 "선행성 기억상실증 환자"로 LLM은 새로운 세션이 열릴 때마다 백지 상태에서 시작 [1]
- 현재 LLM의 학습 방식은 드문 하위집단/희귀 상황을 별도로 모델링하지 않고 전체 평균적 경향을 잘 맞추는 쪽으로 전역 평균화됨 [2]
- 이로 인해 LLM의 응답은 중립/보편/무난하게 수렴되며, 평균을 벗어난 다양한 시나리오/희소한 개인 데이터/long-tail 상황을 이해하지 못함 [2] 
- 현재 LLM은 학습 종료 시점의 지식에 묶여 있으며, 이는 인간 지능과 달리 환경에 적응하기 위해 지속적인 학습을 수행할 수 없음
- 유한한 context window를 갖는 현 LLM의 구조는 장기 목표를 수행하는데 부적합함 


## 정적 지능(Foundation Model)에서 동적/자기 진화형 지능으로 패러다임 전환
- 장기적으로 인간 수준 지능인 AGI에 도달하려면 정적인 parametric memory 중심 구조에서 동적 메모리/학습 중심 구조로의 전환이 필요함
- 인간은 지속 학습(Continual Learning. CL)과 장기 기억(Long-Term Memory. LTM)를 통해 지능을 발전시키도록 진화하였음.
- AI 또한 지속적으로 학습하고 경험을 축적할 수 있는 자기진화 능력은 정적 지능의 근본적 제약을 넘어서기 위해 필요함. AGI는 환경 적응력과 자기 개선 능력없이 도달할 수 없음
- Noam Brown(OpenAI o1 research scientist. o1의 핵심 연구자)는 현재 AI를 원시인로 비유하며 수십억 개의 AI와 장기간 협력하고 경쟁하면 문명을 건설할 수 있을 것이라는 AI 문명 가설을 주장 [3]
- Eric shumit는 시스템이 스스로 학습하는 RSI(Recurisve Self-Improvment)를 통해 인간이 이해할 수 없는 속도로 기하급수적으로 발전하는 시점이 올 것으로 예측 [4]
- CL과 LTM은 상호 의존적임. LTM 없이 CL은 학습 데이터가 없고 CL이 없는 LTM은 단순한 데이터 아카이브에 불과함

## Scaling Laws
- Scaling의 개념은 이미 학습을 넘어 추론(Test-time)으로 확장됨
  - Intelligence = f(N, D, C) ; N: 파라미터, D:데이터셋, C: 컴퓨팅
  - 데이터셋(D)는 초기 학습에 투입한 원시 정보
- AI가 자기 진화 단계에 진입하면 AI의 성능(지능)은 경험을 습득, 저장, 효율적으로 처리하는 능력에 따라 확장됨
  - Intelligence = f(N, D, C, M) ; M: 장기 기억(LTM), M은 새로운 자원으로써 D의 하위 개념이 아닌 독립적인 차원으로 볼 수 있음
  - 현 LLM은 추론 시 평생(lifelong) 에피소드 경험을 축적할 수 없음. LTM이 추가되면서 평생(lifelong) 에피소드 경험을 CL을 통해 지속적으로 학습할 수 있게 됨
  - LLM은 LTM에 축적된 에피소드 경험을 자기 진화 루프의 데이터로 사용함
  - M은 단순히 저장된 벡터의 크기와 같이 단일 지표로 정의되지 않음.
    - M은 1)경험의 양(size) 뿐만이 아니라 2) 기억의 구조화 수준(Structual Complexity), 3)검색, 통합, 압축 등 기억 운영에 필요한 계산 비용의 집합임
    - 작고 제대로 조직회되지 않는 기억(M)은 학습 능력을 제한함
- M의 용량과 품질의 중요성
  - M 역시 일정한 규모나 품질에 도달해야 정확도가 향상되는 임계 효과 존재함.
    - 일정 이상의 N을 가진 LLM을 Pre-training하였을 때 emergent abilities가 생기는 것과 유사함
  - 검색 시 잡음이 많은 문서와 질의와 무관한 문서로 가득 차 있다면, M의 크기가 크다고 해서 정확도를 개선하지 할 뿐만 아니라 오히려 답변의 품질이 떨어질 수 있음
    - M이 무작위 웹데이터 같은 저품질 데이터를 가득 차 있다면 메모리 용량만 차지할 뿐 성능 향상에 도움이 되지 않음
    - 퀴즈 QA는 메모리 데이터베이스에 그 정답이 담긴 문서가 적어도 하나는 있을 때부터 제대로 답하기 시작함
  - 단순히 M의 크기를 키우는 것이 아니라 M의 품질도 같이 증가해야 해야 함
- 메모리 접근 비용도 고려해야 함
  - M의 크기가 커질수록 질의마다 방대한 메모리를 탐색해야 하므로 latency가 커짐
  - 정확도를 높일만큼 충분한 M의 크기와 검색에 따른 허용 latency를 만족하는 최적점을 찾아야 함
  - 이를 위해 단순히 M의 크기를 증가시키기만 하면 오래되거나 무관한 데이터가 지배할 수 있으므로 데이터를 조직화하고 가치가 낮은 정보를 필터링하는 망각하는 메커니즘이 필요함

## 메모리가 새로운 scaling factor가 될 수 있는 근거
- RETRO (DeepMind)
- Memory layer at scale (Meta)
- Scaling Retrieval-Based Language Models with a Trillion-Token Datastore (Univ. of Washington)
- Scaling Laws For Dense Retrieval (Tsinghua Univ.)


## 미해결 과제
- Intelligence=f(C,N,D,M) 함수의 정확한 수학적 형태와 지수(exponent)는 무엇인가?
  - 이를 밝히기 위해서는 기억의 크기, 구조, 운영 효율성을 체계적으로 변화시키며 성능을 측정하는 대규모 경험적 연구가 필요하다.


## Reference
- [1] [LLM AGI will have memory, and memory changes alignment](https://www.lesswrong.com/posts/aKncW36ZdEnzxLo8A/llm-agi-will-have-memory-and-memory-changes-alignment)
- [2] [Long Term Memory: The Foundation of AI Self-Evolution](https://arxiv.org/pdf/2410.15665)
- [3] [Scaling Test Time Compute to Multi-Agent Civilizations: Noam Brown](https://www.latent.space/p/noam-brown) 
- [4] [Eric Schmidt: AI and the Genesis of a New Epoch](https://youtu.be/_gBxYL2ihc0)



오늘날 우리가 가진 AI는 마치 AI의 원시인과 같습니다. 만약 수십억 개의 AI와 장기간 협력하고 경쟁하며 문명을 건설할 수 있다면, 본질적으로 그들이 생산하고 답할 수 있는 것들은 오늘날 우리가 가진 AI로는 불가능한 것을 훨씬 뛰어넘을 것입니다 ."
