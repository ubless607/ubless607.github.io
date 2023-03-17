---
layout: post
title: Example Content
subtitle: 안녕
category: review
tag: classification
---
* this unordered seed list will be replaced by the toc
{:toc}

# Introduction
WSL을 활용하여 나만의 의료영상 환경을 구축해볼 수 있습니다.

# 1. WSL 설치
<a href="https://docs.microsoft.com/ko-kr/windows/wsl/install" target="_blank">WSL(Linux용 Windows 하위 시스템)</a>을 사용하면 개발자가 기존 가상 머신의 오버헤드 또는 듀얼 부팅 설정 없이 대부분의 명령줄 도구, 유틸리티 및 애플리케이션을 비롯한 GNU/Linux 환경을 수정하지 않고 Windows에서 직접 실행할 수 있습니다.

1. 관리자 모드로 Windows 명령 프롬프트에서 아래 명령을 입력합니다.
![](https://velog.velcdn.com/images/ubless607/post/d4e5dd0e-3a8f-4282-8722-f657a5a6c76b/image.png)


2. Command 창에서 ```bash``` (또는 ```wsl```)를 입력하면  바로 WSL이 실행되는 것을 확인할 수 있습니다.
![](https://velog.velcdn.com/cloudflare/ubless607/7a723ec3-97ca-40b5-9cab-bd757f76c46d/carbon.png)

3. home directory로 이동한 다음, ```wget``` 명령어를 활용하여 <a href="https://conda.io/en/latest/miniconda.html#linux-installers" target="_blank">Miniconda</a>를 다운로드 및 설치합니다.
![](https://velog.velcdn.com/cloudflare/ubless607/8d9a40a3-69a4-444f-9b29-f74154644e34/carbon.png)

> ⚠️ wget: unable to resolve host address error 발생한 경우
  &nbsp;&nbsp;1. <code>sudo vi /etc/resolv.conf</code>
  &nbsp;&nbsp;2. <code>nameserver 8.8.8.8</code> 추가
(ref: <a href="https://heum-story.tistory.com/29" target="_blank">https://heum-story.tistory.com/29</a>)

<hr>

# 2. conda 환경 설치
1. WSL내 Miniconda 환경 아래 conda environment를 설치합니다.
python 버전은 3.10, name이 MIP_2023인 환경을 새로 생성하겠습니다.
![](https://user-images.githubusercontent.com/5417257/224182035-545e86f9-b1c8-4bf8-98f0-07d633485223.png)

2. 이후, 실습 파일을 실행하는데 필요한 라이브러리를 설치합니다.
![](https://velog.velcdn.com/cloudflare/ubless607/4b6d5d73-5156-4bcb-84f2-f79aab48b1d6/carbon.png)

3. ```conda list``` 명령어를 사용하면 환경 내 설치된 라이브러리 목록을 확인할 수 있습니다.
일부 library만 표기해보면 다음과 같습니다.
![](https://velog.velcdn.com/cloudflare/ubless607/5db847b2-88bc-442d-b27c-591ac8d162c8/carbon.png)

> ⚠️ conda 명령어 사용시 Solving Environment에서 무한 로딩이라면?
나의 경우, stackoverflow 페이지에 올라와 있는 channel priority로 해결되지 않았다. C++로 작성된, 빠른 conda package 관리자인 <code>mamba</code>를 사용하면 이런 문제가 발생하지 않았다.
(참고: <a href="https://github.com/mamba-org/mamba" target="_blank">https://github.com/mamba-org/mamba</a>)

> ✅ 가상환경 내에 tensorflow를 설치하는 올바른 방법
tensorflow 공식 페이지에 나와 있듯이 tensorflow 설치시 conda가 아닌 pip로 설치를 권장하고 있다. <code>cudatoolkit</code>이나 <code>cudnn</codE> 등은 conda로 설치하고, 페이지를 참고하여 tensorflow를 설치하면 된다.
(참고: <a href="https://www.tensorflow.org/install/pip?hl=en" target="_blank">https://www.tensorflow.org/install/pip?hl=en</a>)
  
> ✅ WSL2에 CUDA 설치하는 방법
tensorflow 2.10 버전까지만 native Windows에서 GPU를 지원한다고 한다. 이후 버전부터는 Ubuntu 또는 WSL 환경을 권장하고 있다.
(참고: <a href="https://dsaint31.tistory.com/entry/ML-WSL2-Install-Tensorflow-GPU" target="_blank">[ML] WSL2 : Install Tensorflow (GPU)</a>)
  
<hr>

# 3. git 설정

1. ssh-keygen 명령어를 사용해 ssh key를 생성합니다.
![](https://velog.velcdn.com/cloudflare/ubless607/b737499c-ac13-4ee8-b6b3-1cd1ac0ddeca/carbon.png)

2. Github Repository에 SSH public key를 등록합니다. 위치: ```Settings``` → ```SSH and GPG keys```
![](https://velog.velcdn.com/cloudflare/ubless607/86d8e8d2-db03-4826-9a77-94820b3ebcfd/%EA%B7%B8%EB%A6%BC1.png)


3. repository를 clone합니다.
![](https://velog.velcdn.com/cloudflare/ubless607/31c135ac-3fd2-4d37-87a3-5334fddf7a21/carbon.png)

<hr>


# 4. vscode 연동
1. visual studio code에서 [‘Remote Development’](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension을 추가합니다.
그러면 vscode 내에서 WSL 환경에 접속하여 파일 작업을 할 수 있습니다.
![](https://velog.velcdn.com/cloudflare/ubless607/9dd36507-2c28-40e6-b895-a8febe5b3816/%EA%B7%B8%EB%A6%BC2.png)
![](https://velog.velcdn.com/cloudflare/ubless607/23c2f023-4aae-49bf-afb1-0464bb4541b1/%EA%B7%B8%EB%A6%BC3.png)

2. 설치한 가상환경 내에서 ipynb 파일 내 code block이 정상적으로 동작함을 확인할 수 있습니다.
![](https://velog.velcdn.com/cloudflare/ubless607/8d93773b-08d2-4b4c-876e-0ea25972ba55/%EA%B7%B8%EB%A6%BC6.png)