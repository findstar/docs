---
date: "2018-03-08T18:47:30+09:00"
title: "[Docker 기본(1/8)] Hello Docker!"
authors: ["1000jaeh"]
series: ["docker"]
categories:
  - posts
tags:
  - docker
  - caas
  - container
cover:
  image: "../images/docker-official.svg"
draft: false
---
Docker란 리눅스의 응용프로그램들을 소프트웨어 Container 안에 배치시키는 일을 자동화하는 오픈 소스 프로젝트로서, Docker 공식 문서에 따르면 **Containers as a Service(CaaS) Platform**으로 정의하고 있습니다.

Docker는 홈페이지에 Docker의 기능을 아래와 같이 명시 하고 있습니다.

> Docker Container는 일종의 소프트웨어 실행에 필요한 모든 것들을 포함하는 완전한 파일 시스템 안에 감싼다. 여기에는 코드, 런타임, 시스템 도구, 시스템 라이브러리 등 서버에 설치되는 무엇이든 전부 아우른다. 이는 실행 중인 환경에 관계 없이 언제나 동일하게 실행될 것을 보증한다.

Docker는 리눅스에서 운영체제 수준 가상화에 대한 추상화 및 자동화 계층을 추가적으로 제공합니다. 또한, 리눅스 커널, 통합 파일 시스템의 리소스 격리 기능을 사용하며, 이를 통해 독립적인 **Container**가 하나의 리눅스 인스턴스 안에서 실행할 수 있게 함으로써 가상 머신에 대한 유지보수 부담을 덜어줍니다.

## Monolithic에서 Microservice로

지금까지는, 절대로 변하지 않을 듯한 Infrastructure를 기반으로 OS/Runtime/Middleware는 잘 정돈되어져 있었고, 그 위에 수 많은 기능들을 제공하는 대형 Application이 실행되고 있었습니다. 해당 Application에서 장애란 있을 수 없는 일로 간주되어 왔습니다. 하지만, Application의 이런 구조는 Mobile 기기를 필두로 한 전반적인 IT 산업의 변화에 있어서 독이 되었고, 이는 곧 Application의 유연성을 크게 해치게 되었습니다.

이런 흐름에 맞춰 Application들의 전체적인 구조는 모두 바뀌게 되었습니다. 대형 Application들은 다양한 기기와 환경들에 맞춰 빠르게 지원하기 위해 잘게 쪼개졌으며, 개발자들은 최상의 성능을 위해서 사용 가능한 Service들을 개별적으로 조립하여 제공하였습니다. 또한, 조립된 Service들에 맞춰 Infrastructure도 Public / Private / Virtualized된 다양한 환경을 구성하여 사용하게 되었습니다.

## 그렇다면, 왜 Docker인가

이러한 변화 속에서, 다음과 같은 새로운 과제들이 나타나기 시작했습니다.

- 다양한 방식으로 조립된 서비스가 일관되게 상호 작용할 수 있도록 보장하는 방법은 무엇인가?
- 각 Service별 "Dependency Hell"을 피할 수 있는 방법은 무엇인가?
- 수많은 Application을 다양한 환경으로 신속하게 Migration 및 확장할 수 있는가?
- 각 환경에 배포된 Application들의 호환성이 보장 되는가?
- n개의 Service가 n개의 Infrastructure에서 잘 구동될 수 있도록 하는 수 많은 설정들을 어떻게 피할 수 있는가?

과제들에 대한 해결책으로 나타난 것이 **Container**입니다. Container는 Library, 시스템 도구, Code, Runtime 등 Application에 필요한 모든 것이 포함되어 있는 표준화된 유닛으로, 환경에 구애받지 않고 Application을 신속하게 배포 및 확장 할 수 있는 환경을 제공해 줍니다.

{{% center %}}
***따라서, Docker는 이런 Container들을 관리할 수 있는 Service를 제공함으로써,<br/> Application들이 다양한 환경 속에서 일관된 서비스를 제공할 수 있도록 보장합니다.***
{{% /center %}}

## Docker를 사용한다면

### 동일한 Application을 다양한 환경으로 빠르게 배포할 수 있습니다

Docker는 Application 및 Service를 Container를 사용하여 표준화된 환경에서 구동할 수 있도록 함으로써, 개발 주기를 단축시킵니다. 이러한 Container의 이점은 CI/CD Workflow에서 극대화됩니다.

### 환경에 따라, 배포와 확장이 자유롭습니다

Docker는 개발자의 Laptop, Datacenter의 VM, Cloud 환경 또는, 여러 다양한 환경에 쉽게 이식하여 사용할 수 있습니다. Docker의 이런 특성으로 인해, 비즈니스 요구 사항에 맞춰 Application과 Service를 부하에 따라 동적으로 관리할 수 있으며, 거의 실시간으로 축소 또는 확장할 수 있습니다. 타 Platform에 비해 같은 Hardware에서 더 많은 작업을 수행할 수 있습니다. Docker는 가볍고 빠르게 동작하기 때문에, Hypervisor 기반의 Virtual Machine 보다 실용적이고 비용 효율적입니다. 따라서, 적은 Resources로 많은 작업을 수행해야하는 중소규모의 배포 환경 및 고밀도 밀집 환경에 이상적입니다.

## Hello Docker

Docker는 로컬 개발 환경 구성을 위한 Community Edition(CE) 과 실 운영 환경을 위한 Enterprise Edition(EE)의 두 가지 버전으로 제공되고 있습니다.
**Docker Community Edition(CE)**은 각 운영체제 환경에 맞는 설치파일이 제공되고 있습니다.

- [Docker for Mac](https://docs.docker.com/docker-for-mac/install/#download-docker-for-mac)
- [Docker for Windows](https://docs.docker.com/docker-for-windows/)

{{% notice note %}}
Docker의 Version 및 지원 Platform에 대한 자세한 정보는 **[Install Docker](https://docs.docker.com/engine/installation/)**에서 확인하실 수 있습니다.
{{% /notice %}}

Docker 환경 구성 방법은 다음과 같습니다.

1. 로컬 환경의 운영체제에 맞는 Docker 설치파일을 다운받아 설치한 뒤, 실행합니다.
2. `docker version`으로 설치된 Docker의 Version을 확인합니다.
    ```bash
      $ docker version
      Client:
        Version:      18.03.0-ce-rc4
        API version:  1.37
        Go version:   go1.9.4
        Git commit:   fbedb97
        Built:        Thu Mar 15 07:33:28 2018
        OS/Arch:      darwin/amd64
        Experimental: false
        Orchestrator: swarm

      Server:
        Engine:
          Version:      18.03.0-ce-rc4
          API version:  1.37 (minimum version 1.12)
          Go version:   go1.9.4
          Git commit:   fbedb97
          Built:        Thu Mar 15 07:42:29 2018
          OS/Arch:      linux/amd64
          Experimental: true

      $ docker-compose version
      docker-compose version 1.20.0-rc2, build 8c4af54
      docker-py version: 3.1.1
      CPython version: 3.6.4
      OpenSSL version: OpenSSL 1.0.2n  7 Dec 2017

      $ docker-machine version
      docker-machine version 0.14.0, build 89b8332
    ```
3. 구성된 Docker 환경에 Server(Docker Daemon)과 Client외에도 docker-compose와 docker-machine Tool도 같이 설치된 것을 확인하실 수 있습니다.
4. `docker run` 명령어로 `hello-world` Image를 Pull 받아서 Conatiner 생성하여 실행시킵니다.
      ```bash
        $ docker run hello-world
        Unable to find image 'hello-world:latest' locally
        latest: Pulling from library/hello-world
        ca4f61b1923c: Pull complete
        Digest: sha256:97ce6fa4b6cdc0790cda65fe7290b74cfebd9fa0c9b8c38e979330d547d22ce1
        Status: Downloaded newer image for hello-world:latest

        Hello from Docker!
        This message shows that your installation appears to be working correctly.

        To generate this message, Docker took the following steps:
        1. The Docker client contacted the Docker daemon.
        2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            (amd64)
        3. The Docker daemon created a new container from that image which runs the
            executable that produces the output you are currently reading.
        4. The Docker daemon streamed that output to the Docker client, which sent it
            to your terminal.

        To try something more ambitious, you can run an Ubuntu container with:
        $ docker run -it ubuntu bash

        Share images, automate workflows, and more with a free Docker ID:
        https://cloud.docker.com/

        For more examples and ideas, visit:
        https://docs.docker.com/engine/userguide/
      ```
5. 위와 같이 정상적으로 메시지가 나타난다면, Docker 환경 구성이 완료된 것입니다.

## 한 번의 Build로 어디서든 Run

지금까지 Docker환경을 구성하여, `hello-world`라는 Image로부터 Container를 구동시켰습니다. Docker가 설치되어 있다면, `hello-world`는 어디에서든지 100% 동일한 형태로 실행할 것입니다. 이는 Application들이 더 이상 환경에 제약받지 않고, 일관된 서비스를 제공할 수 있음을 의미합니다.

한 번의 Build로 어디서든 Run할 수 있는 Docker. 이런 편리함을 제공하는 Docker가 어떻게 구성되어 있는지, 어떤 식으로 동작되는지가 더욱 궁금해집니다.
