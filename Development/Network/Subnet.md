### 서브넷이란?
![[CleanShot 2023-09-19 at 14.59.58@2x.png]]
서브넷(서브네트워크)는 **네트워크 내부의 네트워크**이다. 서브넷을 통해 트래픽은 불필요한 라우터를 통과하지 않고 더 짧은 거리를 이동하여 대상에 도달할 수 있다.
### IP 주소란?
인터넷에 연결되는 모든 장치에는 고유한 인터넷 프로토콜([[IP]]) 주소가 할당되므로 인터넷을 통해 전송된 데이터가 인터넷에 연결된 수십억 개의 장치 중 올바른 장치에 도달할 수 있다.
### 서브넷이 필요한 이유
- IP 주소가 구성되는 방식을 통해 인터넷 라우터는 데이터를 라우팅할 올바른 네트워크를 간단하게 찾을 수 있다. 
- IP 주소는 네트워크 및 장치 주소를 나타내는 것으로 제한되므로 IP 주소를 사용하여 IP 패킷이 이동해야 하는 서브넷을 나타낼 수 없다.
	- 따라서 네트워크 내의 라우터는 **서브넷 마스크**를 사용하여 데이터를 하위 네트워크로 정렬한다.

