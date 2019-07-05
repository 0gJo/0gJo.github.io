참고 사이트 :http://www.mybatis.org/mybatis-3/*** ( 레퍼런스 용도)

* 스프링 4 버전에는 MyBatis/iBatis 연동 기능이 포함되어 있지 않다 

  -> mybatis-spring 모듈 추가 

* myBatis 모듈 추가

* sqlSessionFactoryBean을 이용해서 [sqlSessionFactory 설정]

  ​	-->DB관련 설정을 하는xml인 service-context에 하자

* 트랜잭션 설정

* MyBatis를 이용한 DAO 구현 

  ​	--> 이제는 직접 자바코딩으로 dao를 구현할 필요가 없다.

  방법 1. sqlSession 이용 dao구현 (NLNoticeDao.xml)

  방법2. 매퍼 동적 생성 이용 dao 구현 

* Dao를 사용하는 곳에 sqlSession을 필드로 선언하고 주입받는 코딩 후,  

  Dao의 함수사용 

  CustomerController.java

  ``` java
  	NoticeDao m_noticeDao =  this.sqlSession.getMapper(NoticeDao.class);
  		List<Notice> list  = m_noticeDao.getNotices(page, field, query);
  ```

  

sqlSession == myBatis용 dao 라고  생각하면 된다.      

sqlSessionFactory에서query만 있는 xml파일을 읽어 자동으로 DAO를 만들어 주는 것이다.        

NLNoticeDao.xml

```xml
	<select id="getNotices" resultType="org.sist.web.newlecture.vo.Notice">
	
		SELECT *
		 FROM
		(
		SELECT ROWNUM NUM, N.* 
		FROM 
		(
		SELECT * 
		FROM NOTICES
		WHERE ${param2} LIKE '%${param3}%'
		ORDER BY REGDATE DESC
		) N
		)
		WHERE NUM BETWEEN (1 + (#{param1}-1)*15) AND (15 + (#{param1}-1)*15)
	
	</select>
```

${}: 전달된 값을 "그대로" 사용할떄      

#{} : 전달된 값을 원하는 데이터타입으로 사용할 때      

```xml
	<insert id="insert">
	
	<selectKey order="BEFORE" keyProperty="seq" resultType="String">
	SELECT MAX(TO_NUMBER(SEQ))+1 FROM NOTICES
	</selectKey>
	
		INSERT INTO NOTICES(SEQ, TITLE, CONTENT, WRITER, REGDATE, HIT, FILESRC) 
		VALUES(  #{seq} , #{title}, #{content},#{writer}, SYSDATE, 0
		, #{filesrc, javaType=String, jdbcType=VARCHAR})
	
	</insert>
```

selectkey는 먼저 수행해야할 쿼리를 나타낸다.    





Annotation방법으로 쿼리 등록 가능 

NoticeDao.java (인터페이스)      

```java
	@Select("SELECT COUNT(*) CNT FROM NOTICES WHERE ${field} LIKE '${param}'")
	public int getCount(
				@Param("field") String field
			, @Param("query") String query) throws ClassNotFoundException, SQLException;

@Delete("DELETE  FROM NOTICES  WHERE SEQ= #{seq}")
	public int delete(String seq) throws ClassNotFoundException, SQLException;

	@SelectKey(before=true, keyProperty="seq", resultType=String.class
			, statement=" SELECT MAX(TO_NUMBER(SEQ))+1 FROM NOTICES")
	@Insert(" INSERT INTO NOTICES(SEQ, TITLE, CONTENT, WRITER, REGDATE, HIT, FILESRC)     VALUES(  #{seq}   , #{title}, #{content}, #{writer} , SYSDATE, 0			   , #{filesrc, javaType=String,  jdbcType=VARCHAR} )")
	public int insert(Notice notice) throws ClassNotFoundException, SQLException;  
```



