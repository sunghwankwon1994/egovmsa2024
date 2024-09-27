- [1. 쿠버네티스란? (Kubernetes)](#1-쿠버네티스란-kubernetes)
- [2. 등장 배경](#2-등장-배경)
    - [문제](#문제)
    - [해결책](#해결책)
- [3. 쿠버네티스 아키텍처](#3-쿠버네티스-아키텍처)
    - [Control Plane Components (Master Node)](#control-plane-components-master-node)
    - [Node Components (Worker Node)](#node-components-worker-node)
- [4. 컨테이너 오케스트레이션 툴 비교](#4-컨테이너-오케스트레이션-툴-비교)


# 1. 쿠버네티스란? (Kubernetes)
> **분산형 애플리케이션 및 서비스 규모에 맞게 실행하도록 설계된 오픈소스 컨테이너 오케스트레이션 플랫폼**

![아키텍처](./img/architecture.png)


# 2. 등장 배경
### 문제
> Traditional Deplooyment(전통적인 배포 시대)
>   → Virtualized Deployment(가상화된 배포 시대)
>   → Container Deployment(컨테이너 개발 시대)

![등장 배경](./img/Container_Evolution.svg)

물리 서버에서 리소스 할당 문제를 해결하고자 가상화 기술이 등장하였습니다. 하나의 물리 서버에 여러 가상 시스템(VM)을 실행할 수 있게 되었지만, 가상화 기술은 무겁고 느리다는 단점이 있었습니다. 운영체제를 공유하며 애플리케이션을 격리하는 컨테이너 기술이 등장하며 이러한 단점을 해결하였습니다.

도커가 컨테이너 기반의 서버 환경이 많아지면서 컨테이너 관리에 어려움을 겪게 되었습니다. 프로덕션 환경에서 여러 대의 서버에 동작중인 컨테이너가 정상적으로 동작하는지, 다운되었을 때 어떻게 대처할지 등을 시스템에 의해 처리하기 위해 컨테이너 오케스트레이션 시스템이 필요해졌습니다.

### 해결책
이를 해결하고자 쿠버네티스가 등장하게 됩니다. 수동으로 제어하던 컨테이너의 배포, 운영을 자동화하는 오케스트레이션 시스템으로, 여러 서버들을 클러스터로 구성하여 손쉽게 관리할 수 있게 되었습니다.

쿠버네티스의 기능은 다음과 같습니다.

- 서비스 디스커버리와 로드 밸런싱
- 스토리지 오케스트레이션
- 자동화된 롤아웃과 롤백
- 자동화된 빈 패킹(bin packing)
- 자동화된 복구(self-healing)
- 시크릿과 구성 관리

# 3. 쿠버네티스 아키텍처
> 쿠버네티스 클러스터는 컴퓨터 집합인 `Node Components`와 `Control Plane Components`로 구성됩니다.

![컴포넌트](./img/components-of-kubernetes.png)

### Control Plane Components (Master Node)
> 클러스터에 관한 전반적인 결정을 수행하고 클러스터 이벤트를 감지하고 반응합니다.
- `kube-apiserver` : 쿠버네티스 API 서버이자 쿠버네티스 controle plane의 프론트 엔드
- `etcd` : 모든 클러스터 데이터를 저장하는 저장소. key-value 형태로 데이터를 저장
- `kube-scheduler` : 새로 생성된 파드를 감지하고 실행할 노드 선택
- `kube-controller-manager` : 컨트롤러 프로세스를 실행
- `cloud-controller-manager` : 클라우드 공급자의 API와 통신

### Node Components (Worker Node)
> 동작 중인 파드를 유지시키고 쿠버네티스 런타임 환경을 제공하며, 모든 노드 상에서 동작합니다.
- `kubelet` : 클러스터 각 노드에서 실행되는 에이전트. 파드에서 컨테이너가 실행되도록 관리
- `kube-proxy` :클러스터 각 노드에서 실행되는 네트워크 프록시. 
- `Container Runtime` : 컨테이너 실행을 담당하는 소프트웨어. Docker, containerd 등

# 4. 컨테이너 오케스트레이션 툴 비교
| 특징 | Kubernetes | Docker Swarm | Apache Mesos | Nomad | Rancher | OpenShift |
|------|------------|--------------|--------------|-------|---------|-----------|
| 복잡성 | 높음 | 낮음 | 중간 | 낮음 | 중간 | 높음 |
| 확장성 | 매우 높음 | 중간 | 매우 높음 | 높음 | 높음 | 매우 높음 |
| 학습 곡선 | 가파름 | 완만함 | 가파름 | 중간 | 중간 | 가파름 |
| 커뮤니티 지원 | 매우 강함 | 강함 | 중간 | 중간 | 강함 | 강함 |
| 기업용 기능 | 있음 | 제한적 | 있음 | 제한적 | 있음 | 매우 강함 |
| 클라우드 지원 | 뛰어남 | 좋음 | 좋음 | 좋음 | 뛰어남 | 뛰어남 |
| 설치 난이도 | 복잡함 | 간단함 | 복잡함 | 간단함 | 중간 | 복잡함 |
| 모니터링 도구 | 내장 + 확장 가능 | 기본 | 확장 가능 | 기본 | 강력함 | 강력함 |
| 자동 스케일링 | 내장 | 제한적 | 지원 | 지원 | 지원 | 지원 |
| 롤링 업데이트 | 지원 | 지원 | 지원 | 지원 | 지원 | 지원 |