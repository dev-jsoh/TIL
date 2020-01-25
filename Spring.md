# Spring

## 예제로 배우는 Spring Framework

### spring-petclinic

#### 프로젝트 실행

1. clone spring-petclinic project

2. Maven build

   > ./mvnw package

   project build 후 package 생성

   pom.xml에서 \<packaging>을 통해서 타입 지정 가능 기본은 jar

3. java package 실행

   * java -jar target/*.jar

   * java main method 실행을 통해서도 실행 가능(maven build를 먼저 해야함)

#### 프로젝트 살펴보기

* 로그 수준 설정

  src\main\resources\application.properties

  logging level 변경

* Find Owners 클릭했을 때

  * log를 통해 OwnerController의 initfindform 동작한 것을 알 수 있음
  * InitFindForm이 return 해 준 것은 view를 return
  * view는 resources 디렉토리의 templates 아래에 있음
  * Flow
    1. request 
    2. Spring dispatcher servlet이 @GetMapping을 보고 InitFindForm 메소드 호출
    3. return 값을 통해 template 생성

##### 과제

* LastName이 아니라 FirstName으로 검색해볼까?

  ```html
  findOwners.html
  <input class="form-control" th:field="*{firstName}" size="30"
              maxlength="80" />
  ```

  ```java
  // OwnerController.java
  
  if (owner.getFirstName() == null) {
              owner.setFirstName("");
          }
  
  		// find owners by last name
  //		Collection<Owner> results = this.owners.findByLastName(owner.getLastName());
          Collection<Owner> results = this.owners.findByFirstName(owner.getFirstName());
  		if (results.isEmpty()) {
  			// no owners found
  			result.rejectValue("firstName", "notFound", "not found");
  			return "owners/findOwners";
  		}
  ```

  ```java
  // Owner.java
  @Override
  	public String toString() {
  		return new ToStringCreator(this)
                  .append("id", this.getId()).append("new", this.isNew()).append("firstName", this.getFirstName())
  				.append("id", this.getId()).append("new", this.isNew()).append("lastName", this.getLastName())
  				.append("firstName", this.getFirstName()).append("address", this.address).append("city", this.city)
  				.append("telephone", this.telephone).toString();
  	}
  ```

* 정확히 일치하는게 아니라 해당 키워드가 들어있는 것을 찾아볼까?

  ```java
  // OwnerRepository.java
      @Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE %:firstName%")
      @Transactional(readOnly = true)
      Collection<Owner> findByFirstName(@Param("firstName") String firstName);
  ```

* Owner에 age 추가

  ```java
  // owner.java
  
  @Column(name = "age")
      @NotEmpty
      private String age;
  
  	public String getAge() { return this.age; }
  
  	public void setAge(String age) { this.age = age; }
  ```

  * data.sql, schema.sql 에 age 추가

##### 과제 강사 풀이

* 1번

  * findOwners.html

  > lastName 으로 돼있는 것 firstName으로 수정

  * OwnerController.java

  > getLastName 부분 firstName으로 수정
  >
  > findByFirstName으로 수정 그리고 method 추가

* 2번

  * OwnerRepository.java

    > %:firstName%
    >
    > 콜론 앞에 % 넣어줘야함

* 3번

  * Owner.java

    > age 추가 & getter, setter 추가

  * schema.sql

    > owners table에 age 추가
    >
    > data.sql 에 column 개수에 맞게 age 추가

  * 각종 html

    > age 추가

