# Tokenization(토큰화)란?
> 사용자의 프롬프트를 LLM이 처리할 수 있는 최소 단위인 토큰(Token) 으로 분할하고, 각 토큰에 고유한 ID를 매핑하는 단계

## ✂️ 토큰화의 동작 과정
1. "나는 인공지능을 공부한다."라는 문장은 `["나", "는", " 인공", "지능", "을", " 공부", "한다", "."]`와 같이 의미 있는 여러 단위(Token)로 나뉜다.
2. 각 Token은 사전(Vocabulary)에 정의된 고유한 정수 ID(Token ID)에 매핑된다.
3. 각 Token ID는 이후 Embedding 단계에서 해당 Token의 벡터를 조회하기 위한 index로 사용된다.

## ⚙️ 대표적인 Tokenizer 방식
| 구분 | Tokenizer | 대표 모델 | 핵심 아이디어 |
|---|---|---|---|
| Algorithm | **BPE (Byte Pair Encoding)** | GPT-2, Llama, Qwen 등 | 최소 단위로 쪼갠 후 자주 등장하는 token pair를 반복적으로 merge하며 vocabulary 구성 |
| Algorithm | **WordPiece** | BERT, DistilBERT, ELECTRA | BPE와 유사하지만 token pair의 가능도(likelihood) 기준으로 merge하며 vocabulary 구성 |
| Algorithm | **Unigram** | T5, mBART | 큰 후보 vocabulary에서 시작하여 likelihood에 미치는 영향이 작은 subword를 제거하며 vocabulary 구성 |
| Framework | **SentencePiece** | T5, ALBERT, XLNet 등 | 공백 기반 전처리에 의존하지 않고 raw text에서 BPE/Unigram 등의 subword tokenization 수행 |

-. Vocabulary 구성 방식
* BPE, WordPiece : 작은 단위에서 시작하여 결합 (Bottom-up)
* Unigram : 최대 조합에서 분할 (Top-down)

-. SentencePiece
* 공백 기반의 Pre-tokenization에 의존하지 않고 raw text를 직접 처리할 수 있는 프레임워크 혹은 구현 방식
* 한국어처럼 조사가 단어에 붙거나 공백의 의미가 크지 않은 언어를 처리하는 데 매우 효과적
