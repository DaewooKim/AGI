# Memory기반 scaling laws 

## LLM의 문제점
- LLM은 "선행성 기억상실증 환자"로 LLM은 새로운 세션이 열릴 때마다 백지 상태에서 시작 [1]
- 현재 LLM의 학습 방식은 드문 하위집단/희귀 상황을 별도로 모델링하지 않고 전체 평균적 경향을 잘 맞추는 쪽으로 전역 평균화됨 [2]
- 이로 인해 LLM의 응답은 중립/보편/무난하게 수렴되며, 평균을 벗어난 다양한 시나리오/희소한 개인 데이터/long-tail 상황을 이해하지 못함 [2] 
- 현재 LLM은 학습 종료 시점의 지식에 묶여 있으며, 이는 인간 지능과 달리 환경에 적응하기 위해 지속적인 학습을 수행할 수 없음


## 정적 지능(Foundation Model)에서 동적/자기 진화형 지능으로 패러다임 전환
- 장기적으로 인간 수준 지능인 AGI에 도달하려면 정적인 parametric memory 중심 구조에서 동적 메모리/학습 중심 구조로의 전환이 필요함
- Noam Brown(OpenAI o1 research scientist. o1의 핵심 연구자)는 현재 AI를 원시인로 비유하며 수십억 개의 AI와 장기간 협력하고 경쟁하면 문명을 건설할 수 있을 것이라는 AI 문명 가설을 주장 [3]
- Eric shumit는 시스템이 스스로 학습하는 RSI(Recurisve Self-Improvment)를 통해 인간이 이해할 수 없는 속도로 기하급수적으로 발전하는 시점이 올 것으로 예측 [4]

## Scaling Laws




## Reference
[1] [LLM AGI will have memory, and memory changes alignment](https://www.lesswrong.com/posts/aKncW36ZdEnzxLo8A/llm-agi-will-have-memory-and-memory-changes-alignment)
[2] Long Term Memory: The Foundation of AI Self-Evolution(https://arxiv.org/pdf/2410.15665)
[3] [Scaling Test Time Compute to Multi-Agent Civilizations: Noam Brown](https://www.latent.space/p/noam-brown) 
[4] [Eric Schmidt: AI and the Genesis of a New Epoch](https://youtu.be/_gBxYL2ihc0)
오늘날 우리가 가진 AI는 마치 AI의 원시인과 같습니다. 만약 수십억 개의 AI와 장기간 협력하고 경쟁하며 문명을 건설할 수 있다면, 본질적으로 그들이 생산하고 답할 수 있는 것들은 오늘날 우리가 가진 AI로는 불가능한 것을 훨씬 뛰어넘을 것입니다 ."
