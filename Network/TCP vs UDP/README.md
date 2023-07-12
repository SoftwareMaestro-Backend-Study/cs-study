# TCP vs UDP


1. TCP는 어떻게 신뢰성 있는 데이터 전송을 보장하는가?
    <details>
    <summary>답변 보기</summary>
        ACK, SEQ를 사용해서 데이터 전송의 확인과 순서를 보장한다.
    </details>

2. TCP의 3-way handshake 과정을 자세히 설명하시오. ACK와 SEQ를 구체적으로 설명하세요.
    <details>
    <summary>답변 보기</summary>
        상대방에게 연결 의사를 전달(SYN bit를 1로 설정). 연결 요청을 받으면 연결 수락을 보낸다. 수락에 대한 ACK를 보낸다. 이때, ACK는 상대방 SEQ + (보내는 데이터의 byte수).
    </details>

3. TCP와 UDP의 차이점을 설명하시오.
    <details>
    <summary>답변 보기</summary>
        TCP- 연결, 신뢰성 있는 데이터 전송(ACK 전송), 속도가 느림. 혼잡 제어 & 흐름 제어 O
        UDP - 비연결, 신뢰성 없는 데이터 전송(ACK 전송 x), 속도 빨라서 스트리밍 서비스에 사용, 혼잡 제어 & 흐름 제어 X
    </details>

4. TCP의 혼잡 제어와 흐름 제어를 각각 설명하시오.
    <details>
    <summary>답변 보기</summary>
        혼잡 제어: 네트워크 혼잡 상태를 감지하고 전송 속도를 조절
        흐름 제어: 송신, 수신자의 데이터 처리 속도 제어(오버플로우 방지)
    </details>

5. 실시간 통신을 위해 TCP 대신 UDP를 사용하는 이유는 무엇인가?
    <details>
    <summary>답변 보기</summary>
        UDP는 헤더가 매우 단순해서 데이터 전송 속도가 빠르기 때
    </details>

8. 'slow start'이란 무엇이며, 이것이 TCP에서 왜 필요한지 설명하시.
    <details>
    <summary>답변 보기</summary>
        처음 통신을 시작할 때 패킷을 조금씩 보내다가 점차 증가시키는 방식
    </details>

9. TCP 세그먼트의 구조와 각 구성 요소의 역할에 대해 설명해주세요.
    <details>
    <summary>답변 보기</summary>
        발신지 포트주소, 수신지 포트주소, Seq number, Ack number, Window size 등등 
    </details>

