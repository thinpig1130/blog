---
layout : post
categories : Spring
title: 우아한 스프링 부트 정리
excerpt: 우아한Tech 우아한 스프링 부트 (발표자/ 백기선) 
---

스프링 부트
스프링을 쉽게 사용하기 위해 제공해 주는 틀

스프링 
자바 Enterprise Application 개발을 편리하게 해주기 위한 프레임워크

선수지식
스프링, JEE

빌드
    프로젝트 생성
    의존성 관리
    애플리케이션 패키징

코딩
    개발 툴 제공
    자동 설정
    외부 설정

배포 및 관리
    도커 이미지 생성
    Actuator
    스프링 부트 어드민
----------------------------------
빌드1. 프로젝트 생성

자바프로젝트를 만든다는 것.
디렉토리 만들고, 소스코드 생성, 소스코드가 사용하는 리소스 파일 넣어 놓는 것.
생성시 빌드툴(Maven, Gradle)을 고려하여 빌드툴이 정해놓은 특정한 디렉토리의 구조로 만들어야 함.

start.spring.io >  자바프로젝트를 자동 생성 할 수 있도록 지원함.
    메이븐, 그래들 빌드 툴 선택
    자바, 코틀린, 그루비 
    스프링 버전 선택
    프로젝트 기본 정보 입력
    의존성 추가
    패키징 방법 선택
    자바 버전 선택

Spring Boot 버전 선택
    SNAPSHOT > 아직 개발중인 버전 (되도록 선택하지 않는다.)
    M(Milestone) > 마에스톤으로 배포한 버전, 공식적으로 배포 하였으나 바뀔 수 있음. (얼리어덥터 용)
    RC(Release Candidate)
    아무것도 안달려 있는 것 GA(Generally available) 버전 > 정식 배포 버전
Project Metadata 
    프로젝트의 기본적인 정보
    Group + Aritifact + version 정보가 합쳐져서 사용 할 수 있는 프로젝트 식별 정보가 된다. (처음 생성시 버전은 1.0.0_SNAPSHOT 으로 만들어짐)
    
    Group : 
    Aritifact : 프로젝트 명
    Name : 
    Description : 부가정보
    Package name : 부가정보
    Packaging : 디폴트 패키지로 쓰이는 패키지
    Java :
        Jar(Java Archive) 
        War(Web Application Archive) 
            웹 애플리케이션 구조/ 웹과 관련된 설정 및 디렉토리 리소스 등

빌드2. 의존성 관리
프로젝트에 필요한 의존성 쉽게 관리하기
버전이 명시 되어 있지 않은 상태에서 
지금 스프링 부트에 최적화 된 버전을 찾아 의존성 라이브러리를 생성 해줌. 
(dependency management 가 관리 해줌.)

빌드3. 애플리케이션 패키징

애플리케이션 실행
    - mvn spring-boot:run
    스프링 부트 메이븐 플러그인 사용.
    메이븐을 사용해서 실행한다.
    - main 클래스 실행
    - JAR 패키징 & java -jar
    스프링 부트 플러그인을 사용해 특수한 실행 가능한 형태의 JAR 파일 만들 수 있다. 패키지 수행 하면 target 폴더에 jar 파일 ( 또는 war 파일 ) 이 만들어 진다. (배포용도로 할때 주로 사용)
    java -jar 만들어진자르파일.jar
    우버자르, 팻자르라고 부름 ( 스프링 부트가 해줌. 스프링부트 메이브 플러그인 )

lsof -i:8080
------------------------------------
코딩1. 개발 툴 제공
Spring-Boot-Devtools ( 빌드하면, 최소범위를 재실행 하여 재기동 한다.)
    개발 중에 뷰 리소스 또는 템플릿에 적용되는 캐시는 오히려 불편하다.
    개발 중에 애플리케이션을 자주 재시작 한다.
    개발 중에 웹 브라우저를 자주 리로딩 한다.

애플리케이션 배포시 빼고 패키징 하고 싶다!! 


코딩2. 자동 설정 (스프링 부트의 꽃)
@ComponentScan
@Component, @service, @Contoller, @Repository
@Configuration
@Bean

그 어떠한 설정을 하지 않아도, 자동으로 설정 !! 
자동 설정으로 제공하는 빈 등록
META-INF/spring.factories
EnableAutoConfiguration
@Configuration && @ConditionalOnXxx

코딩3. 외부 설정
코드에서 값을 밖으로 꺼내는 방법 제공
application.properties 또는 application.yaml, 환경 변수, java 명령어
아규먼트 등 키/값의 형태로 정의되어 있는 다양한 외부 설정을 지원한다.
application.properties
가장 구체적이고 가까운 위치에 있는 설정의 우선 순위가 높다.
우선순위 1. config/
우선순위 2. / 실행위치
우선순위 3. jar내부 config/ 
우선순위 4. jar 내부 /
-----------------------------------------
배포 및 관리
배포 및 관리1. 도커 이미지 생성
    도커 이미지는 다른 이미지를 기반으로 새로운 이미지를 만들 수 있다.
    계층형 이미지를 만든다면 기존 계층은 캐시로 재사용할 수 있어 효율적이다. 

spring-boot > spring-boot-build-image (2.4 부터 지원)
docker dive로 도커 이미지 빌드 확인 할 수 있음.

배포 및 관리2. Actuator
애플리케이션 관련 데이터 및 모니터링 정보 제공
Spring-Boot-Starter-Actuator

웹(JSON)과 JMX 지원
여러 엔드포인트 제공
    /beans "빈" 정보 조회.
    /configprops "프로퍼티" 정보 조회.
    /logger "로거" 정보 조회 및 변경 가능.
    /heapdump 메모리의 현재 상태를 내려 받을 수 있다.
    /threaddump 쓰레드의 현재 상태를 내려 받을 수 있다.
    이밖에도 /metrics, /mappings 등 여러 엔드포인트를 제공한다.

배포 및 관리3. 스프링 부트 어드민
spring-boot-admin-starter-server
spring-boot-admin-starter-client
http://github.com/codecentric/spring-boot-admin

