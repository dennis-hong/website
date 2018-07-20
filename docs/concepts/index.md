---
title: 개념
---

개념 섹션에서는 Kubernetes 시스템의 일부와 Kubernetes가 클러스터를 구현하는 데 사용하는 추상화에 대해 학습하고 Kubernetes의 작동 방식을보다 깊이 이해할 수 있도록 도와줍니다.

## 개요

Kubernetes와 함께 작업하려면 *Kubernetes API objects*를 사용하여 클러스터의 *원하는 상태*를 설명하십시오. 실행할 응용 프로그램 또는 기타 작업 부하, 사용하는 컨테이너 이미지, 복제본 수, 원하는 네트워크 및 디스크 자원 이용 가능하게하고, 더. Kubernetes API를 사용하여 객체를 생성하여 원하는 상태를 설정합니다. 일반적으로 명령 행 인터페이스 인 kubectl을 사용합니다. Kubernetes API를 직접 사용하여 클러스터와 상호 작용하고 원하는 상태를 설정하거나 수정할 수도 있습니다.

원하는 상태를 설정하면 *Kubernetes Control Plane*이 작동하여 클러스터의 현재 상태가 원하는 상태와 일치하게됩니다. 그렇게하기 위해 Kubernetes는 컨테이너 시작 또는 재시작, 주어진 응용 프로그램의 복제본 확장 등과 같은 다양한 작업을 자동으로 수행합니다. Kubernetes Control Plane은 클러스터에서 실행되는 프로세스 모음으로 구성됩니다.

* **Kubernetes Master**는 마스터 노드로 지정된 클러스터의 단일 노드에서 실행되는 세 가지 프로세스로 구성됩니다. 이러한 프로세스는 [kube-apiserver](/docs/admin/kube-apiserver/), [kube-controller-manager](/docs/admin/kube-controller-manager/) 및 [kube-scheduler](/admin/kube-scheduler/).
* 클러스터의 각 비 마스터 노드는 두 가지 프로세스를 실행합니다.
  * **[kubelet](/docs/admin/kubelet/)**, Kubernetes Master와 통신합니다.
  * **[kube-proxy](/docs/admin/kube-proxy/)**는 각 노드에서 Kubernetes 네트워킹 서비스를 반영하는 네트워크 프록시입니다.

## Kubernetes 객체

Kubernetes에는 시스템의 상태를 나타내는 많은 추상화가 포함되어 있습니다. 컨테이너 화 된 응용 프로그램 및 작업 부하, 연관된 네트워크 및 디스크 자원 및 클러스터가 수행하는 작업에 대한 기타 정보입니다. 이러한 추상화는 Kubernetes API의 객체로 표현됩니다. 자세한 내용은 [Kubernetes Objects overview](/docs/concepts/abstractions/overview/)를 참조하십시오.

기본 Kubernetes 객체는 다음과 같습니다.

* [Pod](/docs/concepts/workloads/pods/pod-overview/)
* [Service](/docs/concepts/services-networking/service/)
* [Volume](/docs/concepts/storage/volumes/)
* [Namespace](/docs/concepts/overview/working-with-objects/namespaces/)

또한 Kubernetes에는 Controllers라고하는 더 높은 수준의 추상화가 포함되어 있습니다. 컨트롤러는 기본 객체를 기반으로 추가 기능과 편의 기능을 제공합니다. 그들은 다음을 포함합니다 :

* [ReplicaSet](/docs/concepts/workloads/controllers/replicaset/)
* [Deployment](/docs/concepts/workloads/controllers/deployment/)
* [StatefulSet](/docs/concepts/workloads/controllers/statefulset/)
* [DaemonSet](/docs/concepts/workloads/controllers/daemonset/)
* [Job](/docs/concepts/workloads/controllers/jobs-run-to-completion/)

## Kubernetes Control Plane

Kubernetes Master와 kubelet 프로세스와 같은 Kubernetes Control Plane의 다양한 부분이 Kubernetes가 클러스터와 통신하는 방법을 제어합니다. 제어 평면은 시스템에있는 모든 Kubernetes 객체의 기록을 유지하고 연속적인 제어 루프를 실행하여 객체의 상태를 관리합니다. 주어진 시간에 제어 평면의 제어 루프는 클러스터의 변경 사항에 응답하고 시스템의 모든 개체의 실제 상태를 사용자가 제공 한 원하는 상태와 일치하게 만듭니다.

예를 들어 Kubernetes API를 사용하여 Deployment 개체를 만들면 시스템에 대해 원하는 새 상태를 제공합니다. Kubernetes Control Plane은 객체 생성을 기록하고 필수 응용 프로그램을 시작하고 노드를 클러스터 노드로 예약하여 지침을 수행하므로 클러스터의 실제 상태가 원하는 상태와 일치하게됩니다.

### Kubernetes Master

Kubernetes 마스터는 클러스터의 원하는 상태를 유지 관리합니다. `kubectl` 명령 줄 인터페이스를 사용하는 등 Kubernetes와 상호 작용할 때 클러스터의 Kubernetes 마스터와 통신하고 있습니다.

> "마스터"는 클러스터 상태를 관리하는 프로세스 모음을 나타냅니다. 일반적으로 이러한 프로세스는 모두 클러스터의 단일 노드에서 실행되며이 노드는 마스터라고도합니다. 또한 마스터는 가용성 및 중복성을 위해 복제 될 수 있습니다.

### Kubernetes Node

클러스터의 노드는 응용 프로그램 및 클라우드 워크 플로를 실행하는 컴퓨터 (VM, 물리적 서버 등)입니다. Kubernetes 마스터는 각 노드를 제어합니다. 노드와 직접 상호 작용하지 않는 경우가 많습니다.

#### Object Metadata

* [Annotations](/docs/concepts/overview/working-with-objects/annotations/)

### What's next

개념 페이지를 작성하하고 싶으시다면 개념 페이지 타입 및 템플릿에 대한 정보를 위해 [페이지 템플릿 사용](/docs/home/contribute/page-templates/)을 참조하십시오. 
