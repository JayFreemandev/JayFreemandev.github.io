---
layout  : wiki
title   : 사내 쿠버네티스 배포가 지속적으로 실패했던 이유 
summary : 예약 메모리
date    : 2024-05-17 22:02:31 +0900
updated : 2024-05-17 22:02:31 +0900
tag     : 
toc     : true
public  : true
parent  : 
latex   : false
resource: 9CF24E3A-32C4-409C-8E62-2F62A45F020F
---
* TOC
{:toc}

## 문제 상황
사내 쿠버네티스 클러스터에 추가적으로 Pod를 생성하여 애플리케이션을 배포할 때, 예약된 메모리 설정이 충분하지 않아 배포 과정에서 실패가 발생했다. 가장 최소 단위의 메모리 할당부터 시작했지만 실패했다. Pod의 리소스 요청(RAM)이 실제 노드의 가용 메모리보다 많은 경우 쿠버네티스는 해당 Pod를 스케줄링할 수 없기 때문이다. 

CPU request limit이 너무 낮게 설정되어도 문제를 일으킨다. 하나의 노드에 많은 pod들을 운영하기 위한 방법이지만 node overcommitted라는 초과할당 문제가 발생한다. 초기에 이미 가용할 수 있는 자원을 설정해놨지만 더 자원을 쓰는 경우 CPU throttle 발생으로 어플리케이션 지연이 발생하기도 한다.

## 해결 방안
위에 언급한 cpu, ram 모두 적게 할당해도 문제가 생기고 초과 할당을해도 문제가 발생한다. cpu는 limit 도달시 throttle로 인한 지연 발생이지만 메모리가 limit에 도달해버리면 pod가 죽어버린다. 따라서 설정시 Guaranteed QoS에 의해 request와 limit 할당량을 동일하게 설정한다. 
```
      requests:
        memory: "128Mi"
        cpu: 2
      limits:
        memory: "128Mi"
```

워커 노드의 모든 리소스를 실행에 사용할 수 없다
![image](https://github.com/JayFreemandev/JayFreemandev.github.io/assets/72185011/a94965ac-aeb9-4f94-8cee-784834fb121d)
1 CPU / 2 RAM 클러스터가 있을때 리소스를 500mb, cpu 60m으로 지정했을때 다음과 같다. 이때 100mb는 eviction threshold로 빠진다. 퇴거 임계값이라고 불리는건데 노드의 리소스가 부족할때 pod를 종료시켜 리소스를 확보하는 기준이다. 리소스 부족으로 완전히 멈추는걸 방지하기 위한 안전 장치를 말한다.

이때 노드의 메모리가 임계값보다 적어지면 일부 pod를 종료시켜 메모리 확보에 들어간다.
![image](https://github.com/JayFreemandev/JayFreemandev.github.io/assets/72185011/ee2ab5d5-5b7f-4e4f-8b92-72d4fe53e9ac)
보면 30% 메모리와 6%의 cpu가 사용이 불가능하다. 

kubernetes-instance-calculator를 이용해서 각 클라우드별 서버 종류를 선택했을때 계산할 수 있는 사이트를 이용하면 편리하다.
![image](https://github.com/JayFreemandev/JayFreemandev.github.io/assets/72185011/dcdf4646-9cf1-4834-8be6-84b57e3c3673)
AWS-CNI 1.9 사용 여부에따라 aws 기준 eks pod 제한이 달라진다. pod끼리 통신을 위해 고유한 ip 주소를 요구하는데 인스턴스에 따라 할당받을 수 있는 ip 주소의 수가 제한이 되있다. 

인스턴스 유형 선택
워크로드에 2GB의 메모리 요청이 필요하고 최소 ~10개의 복제본이 필요하다고 예상한다고 가정
- '2GB * 10 = 20GB'보다 작은 대부분의 작은 인스턴스는 이미 배제 -> 32gb 선택

해당 인스턴스에 배포할 수 있는 최대 파드 수
예를 들어, 리노드 32GB의 CPU와 메모리 유닛일때, 110pod가 max
- 메모리 장치 257MB(예: (32GB - 3.66GB 예약) / 110)
- CPU 유닛의 경우 71m(예: (8000m - 90m 예약) / 110)

노드에 얼마나 많은 워크로드가 들어갈 수 있는지 예측


추가 자료 :
- [10 most common mistakes using kubernetes](https://coffeewhale.com/kubernetes/mistake/2020/11/29/mistake-10/)
- [클러스터 효율성](https://www.linode.com/ko/blog/kubernetes/how-to-right-size-a-kubernetes-cluster-for-efficiency/)
