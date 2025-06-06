# Project-PestGuard
PestGuard 프로젝트 소스코드 주소 첨부
-->> https://github.com/Azruine/project_pestguard


# 페스트가드 프로젝트 – 무인 해충 방제 시스템 구축
<div align="center">
  <img src="https://github.com/user-attachments/assets/db3aefd7-fe78-4298-8f78-8d297287dcb3" alt="패스트가드 로고" width="300"/>

  ![image](https://github.com/user-attachments/assets/8ff477cf-0661-4474-9bd8-ec3b1a22f1d6)  ![image](https://github.com/user-attachments/assets/797fd306-5ec9-47ab-a74f-9265e9837a81)
  
  ![image](https://github.com/user-attachments/assets/a9e99b19-aa23-4a9e-b442-ffe638194268)
</div>  

## 🛠 Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Jetson%20Nano-76B900?style=for-the-badge&logo=nvidia&logoColor=white"/>
  <img src="https://img.shields.io/badge/ROS-22314E?style=for-the-badge&logo=ros&logoColor=white"/>
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white"/>
  <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white"/>
  <img src="https://img.shields.io/badge/OpenCR-FF5A00?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Raspberry%20Pi-C51A4A?style=for-the-badge&logo=raspberrypi&logoColor=white"/>
  <img src="https://img.shields.io/badge/Android%20Studio-3DDC84?style=for-the-badge&logo=androidstudio&logoColor=white"/>
  <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=java&logoColor=white"/>
  <img src="https://img.shields.io/badge/Qt-41CD52?style=for-the-badge&logo=qt&logoColor=white"/>
  <img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white"/>
  <img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white"/>
  <img src="https://img.shields.io/badge/TCP/IP-0A0A0A?style=for-the-badge"/>
</p>



## 1.프로젝트 개요

**페스트가드 프로젝트는 무인 해충 방제 시스템으로, CCTV 카메라가 바퀴벌레를 탐지하면 터틀봇이 자동으로 해당 위치로 이동하여 해충약을 분사하는 시스템을 구축하는 것을 목표로 했습니다. 이를 위해 OpenCV를 활용한 객체 탐지 및 이동 경로 분석, ROS 기반의 터틀봇 제어, 안드로이드 및 Qt 기반의 사용자 인터페이스 개발 등을 수행하였습니다. 또한 하나의 보드에서 객체 탐지, 데이터 처리, 네트워크 통신, 로봇제어까지 모두 수행하는 저비용의 "엣지 컴퓨팅 기반의 올인원 IoT 시스템"을 목표로 프로젝트를 구현하였습니다.**

## 2.역할 및 기여
본 프로젝트에서 저는 객체 탐지를 제외한 전체 시스템을 구축하였습니다. 주요 역할은 다음과 같습니다.

### ✔ 서버 및 클라이언트 환경 구축

TCP/IP 소켓 통신을 이용한 서버 구축

터틀봇이 객체 탐지 시스템으로부터 좌표 데이터를 수신하고 해당 위치로 이동하도록 제어

방제 작업 수행 후 초기 위치로 복귀하는 로직 구현

### ✔ 터틀봇 동작 및 제어 구현

LDS-02 LiDAR 센서를 활용하여 SLAM(Simultaneous Localization and Mapping) 기능을 구현

실내 공간을 자율적으로 주행하며 지도를 생성하고, 로봇의 현재 위치와 방향을 실시간 추정

Jetson Nano 보드를 **ROS 마스터(roscore)**로 설정하고, TurtleBot3를 클라이언트로 연결

OpenCR 보드에 클라이언트 및 약 방제 로직 펌웨어 빌드

TurtleBot3의 Raspberry Pi 4와 OpenCR 보드는 각각 ROS 노드로 동작하며, Jetson Nano와 실시간 메시지 주고받기를 구현

### ✔ 사용자 인터페이스 개발 (Android Studio & Qt Creator 활용)

사용자가 직접 터틀봇을 원격 조작할 수 있도록 앱 개발

특정 좌표 입력 및 해충약 분사 기능 추가

CCTV를 통해 탐지된 바퀴벌레 이미지를 실시간 확인할 수 있도록 HTTP 기반 이미지 업로드 시스템 구축

### ✔ MariaDB 연동 및 데이터 관리

터틀봇이 객체 탐지 시스템으로부터 좌표 명령을 수신하고 수행한 내역을 데이터베이스에 저장하도록 구현

봇의 정상 작동 여부, 약제 분사 시각 및 위치 등을 기록하여 앱에서 확인 가능하도록 구성

## 3.트러블슈팅 및 해결 과정
프로젝트 진행 중 주요한 두 가지 문제를 겪었고, 이를 해결하며 많은 경험을 쌓았습니다.

### ✔ 가상환경 Linux OS 시스템 손상으로 인한 프로젝트 데이터 손실

두 차례의 시스템 오류로 인해 프로젝트 파일이 모두 삭제되는 사고 발생

처음에는 큰 좌절을 겪었지만, 침착하게 처음부터 다시 구축하면서 기존에 놓쳤던 부분을 보완

결과적으로 프로젝트의 완성도를 높이는 계기가 되었으며, 어려움 속에서도 포기하지 않는 끈기의 중요성을 체감

### ✔ Jetson Nano의 성능 한계로 인한 탐지 방식 변경

초기에는 CUDA 기반의 객체 탐지 및 서버까지 하나의 Jetson Nano에서 구현하려 했으나, 성능 부족 문제로 실행이 어려움

고성능 적외선 카메라를 이용한 탐지 방식을 시도했으나, Jetson Nano가 높은 프레임을 감당하지 못해 실패

일반 카메라로 변경했으나 여전히 성능 문제로 완벽한 해결이 어려워, 배경 제거 기법을 활용하여 탐지 방식을 수정

탐지 방식 변경에 많은 시간이 소요되었으나, 빠른 판단과 발상의 전환을 통해 프로젝트를 완성할 수 있었음

## 4.프로젝트의 의의 및 배운 점
이번 프로젝트를 통해 로봇 시스템 개발, 네트워크 통신, 데이터 관리, UI/UX 개발 등 다양한 기술을 실무적으로 적용할 수 있었습니다. 또한, 문제가 발생했을 때 해결책을 찾고 대안을 마련하는 능력, 그리고 위기 속에서도 포기하지 않고 끝까지 해결하는 끈기와 인내의 중요성을 다시 한번 깨닫게 되었습니다.

페스트가드 프로젝트는 자동화된 해충 방제 시스템 구축을 목표로 하였으며, 실제로 터틀봇을 활용하여 실시간 해충 탐지 및 방제 기능을 구현하였습니다. 이번 경험을 바탕으로 더욱 발전된 시스템을 개발하는 데 기여할 수 있도록 노력하겠습니다.
