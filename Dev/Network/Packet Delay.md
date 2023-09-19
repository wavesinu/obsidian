실제 [[Packet]]들이 전송되는 과정에서 여러가지 요인들로 지연이 발생한다. 패킷이 지연되는 요소는 아래와 같이 4가지로 생각해볼 수 있다.
1. **Processing delay**
2. **Queueing delay**
3. **Transmission delay**
4. **Propagation delay**
즉, 패킷이 전송될 때 발생되는 총 지연은 다음과 같다.
```text
**Nodal delay** = Processing delay + Queueing delay + Transmission delay + Propagation delay
```
___
### Processing delay
- Processing delay는 매우 짧은 시간 동안만 발생하며, 라우터 내의 하드웨어의 성능에 따라 의존하기 때문에 가변적이지 않다.
### Queueing delay
- 라우터로 패킷들이 한번에 많이 들어올 경우, 라우터는 패킷들으 queue 형태로 보관하여 차례대로 처리한다.
	- 이때 전송을 위해 output link의 queue에서 대기하는 동안 발생하는 지연을 Queue delay라고 한다.
- Queueing delay는 라우터의 congestion(혼란) 정도가 결저하며, Processing delay와 달리 상황에 따라 가변적이고 예측이 어렵다.
### Transmission delay
![[Pasted image 20230919140553.png]]
- 패킷이 queue를 빠져나가 라우터의 output link를 통해 빠져나가기 전까지 발생하는 delay이다. 즉, 전송하려는 패킷을 output link로 밀어내는데 걸리는 시간이다.
	- 패킷이 전송되는 link의 성능에 의존하며, 좋은 link를 사용할 경우 Transmission delay가 감소한다.
- Transmission delay는 link의 **bandwidth(link가 최대로 전송할 수 있는 데이터 양)**에 따라 결정되며, link bandwidth는 **불변값**이며 패킷의 길이도 대부분 비슷하기 대문에 비교적 가변적이지 않다.
```
Transmission delay = (Packet Length) / (link bandwidth)
```

### Propagation delay
![[Pasted image 20230919140606.png]]
- 실제 link를 타고 데이터가 전송될 때 발생하는 delay이다.
- Propagation delay는 거리와 link의 매체가 결정하는 delay로, 요즘 같이 광통신을 하는 경우에는 거의 발생하지 않는다고 볼 수 있다.
```
Propagation delay = (distance) / (Propagation speed)
```
