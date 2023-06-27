# ARP
- ARP는 무엇이며 그 기능은 무엇인가요?
    <details>
    <summary>답변 보기</summary>
    
    ARP는 Address Resolution Protocol의 약자로, 네트워크 상에서 IP 주소를 물리적인 MAC 주소로 변환하는 프로토콜입니다. 이를 통해 라우터나 스위치 등이 특정 IP 주소를 가진 호스트에게 패킷을 전송할 수 있게 됩니다.
    </details>
    
- ARP는 어떻게 작동하나요?
    <details>
    <summary>답변 보기</summary>
    
    ARP는 먼저 ARP 요청을 전송하여 해당 네트워크의 모든 장치에게 누가 특정 IP 주소를 가지고 있는지 묻습니다. 이 IP 주소를 가진 장치는 자신의 MAC 주소를 포함한 ARP 응답을 보냅니다.
    </details>
    
- ARP 테이블이란 무엇인가요?
    <details>
    <summary>답변 보기</summary>
    
    ARP 테이블은 호스트가 네트워크 상의 다른 장치들의 IP 주소와 해당 장치의 MAC 주소를 맵핑하여 저장한 테이블입니다. 이 정보는 패킷 전송에 사용되며, 일정 시간 동안 사용되지 않으면 만료됩니다.
    </details>
    
- ARP 스푸핑이란 무엇이며, 어떻게 방지할 수 있나요?
    <details>
    <summary>답변 보기</summary>
    
    ARP 스푸핑은 공격자가 피해자의 IP 주소와 자신의 MAC 주소를 연결하여 네트워크 트래픽을 가로채는 공격입니다. 이를 방지하기 위해서는 ARP Spoofing 방지 솔루션을 사용하거나, 정적 ARP 엔트리를 사용하는 것이 효과적일 수 있습니다.
    </details>
    
- ARP와 RARP의 차이점은 무엇인가요?
    <details>
    <summary>답변 보기</summary>
    
    ARP는 IP 주소를 통해 MAC 주소를 얻는데 사용되고, 반면에 RARP(Reverse Address Resolution Protocol)는 MAC 주소를 통해 IP 주소를 얻는데 사용됩니다. RARP는 주로 부트스트랩 프로세스에서 서버가 자신의 MAC 주소를 기반으로 IP 주소를 할당받는 데 사용됩니다.
    </details>
    
- ARP 요청과 ARP 응답 메시지의 차이점은 무엇인가요?
    <details>
    <summary>답변 보기</summary>
    
    ARP 요청은 브로드캐스트 메시지로, 특정 IP 주소를 가진 장치의 MAC 주소를 요청합니다. 반면, ARP 응답은 유니캐스트 메시지로, 요청받은 IP 주소를 가진 장치가 자신의 MAC 주소를 보내는 메시지입니다.
    </details>
    
- ARP 프로토콜이 사용하는 패킷 구조는 어떻게 되나요?
    <details>
    <summary>답변 보기</summary>
    
    ARP 패킷은 하드웨어 유형, 프로토콜 유형, 하드웨어 주소 길이, 프로토콜 주소 길이, 오퍼레이션(ARP 요청 또는 응답), 송신자 하드웨어 주소, 송신자 프로토콜 주소, 수신자 하드웨어 주소, 수신자 프로토콜 주소 등을 포함합니다.
    </details>
    
- Gratuitous ARP란 무엇이며, 어떤 경우에 사용되나요?
    <details>
    <summary>답변 보기</summary>
    
    Gratuitous ARP는 자신의 IP 주소를 다른 장치에게 알리거나, 네트워크 상의 IP 주소 충돌을 검사하거나, 스위치나 라우터 등의 ARP 캐시를 업데이트하기 위해 사용되는 ARP 메시지입니다. 또한, IP 주소를 변경하거나 NIC를 교체한 후에도 Gratuitous ARP가 사용될 수 있습니다.
    </details>
