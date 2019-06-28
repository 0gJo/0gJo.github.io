STS 3.9 설치

Spring Legacy Project - Template : Spring MVC Project

topLevelPacakge ex.)org.sist.web ( 한글경로 들어가면 문제생길수 있음 (workspace도) )

기본 서버 삭제 후 아파치톰캣 서버 만들기

pom.xml 에서 자바버전(1.8) 변경

프로젝트 - properties - Project Facets 자바버전 변경

servlet-context.xml  == dispatcher-servlet.xml

root-context.xml == dispatcher-service.xml



http://maven.apache.org/download.cgi apache-maven 다운받은뒤 C드라이브로 이동

환경설정 :Path  / M2_HOME 등록 

<maven 날로 만들기>

artitectype에 따라서 탬플릿 .. 프로젝트 생성

cmd 창에

```
// 프로젝트 생성 
mvn archetype:generate -DgroupId=com.newlecture -DartifactId=javaprj -DarchetypeArtifactId=maven-archetype-quickstart

mvn test

//프로젝트 폴더로 이동
mvn compile // target 폴더 생성

// 패키지(jar) 생성
mvn package

// 
mvn install  ( 로컬저장소 m2.reipository 에 jar 이동)

mvn deploy
```

ojdbc6.jar은 중앙저장소에 없으므로 로컬저장소에 올려 놓고 pom.xml(모듈설정 lib) 설정해서 사용

C드라이브에 ojdbc.jar 옮겨 놓기 

cmd에 

```
mvn install:install-file  "-Dfile=ojdbc6.jar" "-DgroupId=com.oracle" "-DartifactId=ojdbc" "-Dversion=6.0" "-Dpackaging=jar"
```

artifactId -> 프로젝트명

Installing C:\ojdbc6.jar to C:\Users\sist\.m2\repository\com\oracle\ojdbc\6.0\ojdbc-6.0.jar

```xml

		<!-- ojdbc6.jar 로컬 저장소에 등록해서 사용  -->
	
		<dependency>
			<groupId>com.oracle</groupId>
			<artifactId>ojdbc</artifactId>
			<version>6.0</version>
		</dependency>


<!-- jdbc -->

		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-jdbc</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
		
```







tiles 관련 jar 파일 추가 - 서버로부터 다운받기

```xml
		<!-- 스프링 타일즈 -->
		<dependency>
			<groupId>org.apache.tiles</groupId>
			<artifactId>tiles-jsp</artifactId>
			<version>3.0.8</version>
		</dependency>

```

