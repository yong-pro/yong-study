### egov eGovFrame Boot Template Project 생성시 에러
	1. projct -> properties -> Deployment Assembly
	    1-1. add
		1-2. java build path entries
		1-3. maven 추가
 

### log4j error maven 설정
	스프링 부트 2.3.0.RELEASE버전은 기본적으로 Log4j2 를 지원하며 , 로깅 구성이 클래스 경로에 있는 경우. 이 경우 다른 log4j 의존성을 간단히 제거할 수 있습니다.

	다른 경우에 의존성을 어셈블하기 위해 스타터를 사용하는 경우 Logback을 제외하고 대신 log4j 2를 포함해야 합니다.

	Gradle 로 그렇게 할 수 있습니다 .

	dependencies {
		implementation 'org.springframework.boot:spring-boot-starter-web'
		implementation 'org.springframework.boot:spring-boot-starter-log4j2'
	}

	configurations {
		all {
			exclude group: 'org.springframework.boot', module: 'spring-boot-starter-logging'
		}
	}
	또는 Maven 으로 :

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
		<exclusions>
			<exclusion>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-starter-logging</artifactId>
			</exclusion>
		</exclusions>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-log4j2</artifactId>
	</dependency>