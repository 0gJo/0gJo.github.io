* dispatcher-servlet.xml 설정파일을 용도별로 2개의 파일로 나누기
* DAO를 복사해서 인터페이스로 만들기(확장성)

게시글 등록시

포인트증가

게시글 insert

제약 조건 : point 3점 불가 / 게시글 title 중복불가



#### 02 스프링의 트랜잭션 지원

DataSource 설정

2.2 DataSourceTransactionManager 설정

방법 1. transactionManager + try~catch 이용 

Dao에 사용할 수 있도록 주입

트랜잭션으로 묶기

```java
	@Override
	public void insertAndPointUpOFmember(Notice notice, String id) {
		// 게시글 insert
		String sql = "INSERT INTO NOTICES(SEQ, TITLE, CONTENT, WRITER, REGDATE, HIT, FILESRC) VALUES("
				+ " (SELECT MAX(TO_NUMBER(SEQ))+1 FROM NOTICES)"
				+ ", :title, :content, 'newlec', SYSDATE, 0, :filesrc)";
		String sqlPoint = "update member set point = point + 1 where id = :id";

		TransactionDefinition def = new DefaultTransactionDefinition();
		TransactionStatus status = this.transactionManager.getTransaction(def );
		try {
			
			this.jdbcTemplate.update(	sql ,  new BeanPropertySqlParameterSource(notice));
			MapSqlParameterSource paramSource = new MapSqlParameterSource();
			paramSource.addValue("id", id);
			
			this.jdbcTemplate.update(sqlPoint, paramSource);
			
			//commit
			this.transactionManager.commit(status);
		} catch (DataAccessException e) {
			this.transactionManager.rollback(status);
			throw e;
		}

	}
```

2.6 트랜잭션 전파와 격리 레벨



#### 03 TransactionTemplate을 이용한 트랜잭션

3.1 TransactionTemplate과 TransactionCallback으로 트랜잭션 처리하기

```java
@Override
	public void insertAndPointUpOFmember(Notice notice, String id) {
		
		
		this.transactionTemplate.execute(new TransactionCallbackWithoutResult() { // void 일때 사용하는 
			
			String sql = "INSERT INTO NOTICES(SEQ, TITLE, CONTENT, WRITER, REGDATE, HIT, FILESRC) VALUES("
					+ " (SELECT MAX(TO_NUMBER(SEQ))+1 FROM NOTICES)"
					+ ", :title, :content, 'newlec', SYSDATE, 0, :filesrc)";
			String sqlPoint = "update member set point = point + 1 where id = :id";
						
			@Override
			protected void doInTransactionWithoutResult(TransactionStatus status) {
				jdbcTemplate.update(	sql ,  new BeanPropertySqlParameterSource(notice));
				MapSqlParameterSource paramSource = new MapSqlParameterSource();
				paramSource.addValue("id", id);
				
				jdbcTemplate.update(sqlPoint, paramSource);
				
			}
		});
		
		
		
	}
```



TransactionTemplate을 bean으로 등록한다. (내부적으로 transactionManager를 사용)

3.2 TransactionTemplate의 트랜잭션 설정

05 선언적 트랜잭션 처리

5.1 tx 네임스페이스를 이용한 트랜잭션 설정

5.2 애노테이션 기반 트랜잭션 설정

```java
@Transactional(propagation=Propagation.REQUIRED)
	public void insertAndPointUpOFmember(Notice notice, String id) {

			String sql = "INSERT INTO NOTICES(SEQ, TITLE, CONTENT, WRITER, REGDATE, HIT, FILESRC) VALUES("
					+ " (SELECT MAX(TO_NUMBER(SEQ))+1 FROM NOTICES)"
					+ ", :title, :content, 'newlec', SYSDATE, 0, :filesrc)";
			String sqlPoint = "update member set point = point + 1 where id = :id";
						

				jdbcTemplate.update(	sql ,  new 				BeanPropertySqlParameterSource(notice));
				MapSqlParameterSource paramSource = new MapSqlParameterSource();
				paramSource.addValue("id", id);
				
				jdbcTemplate.update(sqlPoint, paramSource);

	}
	
```

dispatcher-servlet.xml

```xml
<tx:annotation-driven transaction-manager="transactionManager"/>
```

