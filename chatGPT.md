## 꼭 모든 부분에 try catch 문을 써야 할까요?

모든 부분에 try catch 문을 사용하는 것은 항상 권장되는 것은 아닙니다. try catch 문은 예외 처리를 하기 위한 방법 중 하나로, 코드 실행 중 예외가 발생할 가능성이 있는 부분에 적용됩니다.

예를 들어, 파일을 열거나 데이터베이스에 연결하는 등의 작업은 예외가 발생할 가능성이 높은 작업이므로, 이러한 작업에 대한 예외 처리를 적용하는 것이 좋습니다.

하지만 모든 부분에 try catch 문을 사용하면 코드의 가독성이 떨어지고, 실행 속도도 느려질 수 있습니다. 또한 예외 처리를 너무 과도하게 사용하면, 예외 처리 자체가 예외를 발생시키는 원인이 될 수 있습니다.

따라서, 예외가 발생할 가능성이 있는 작업에 대해서만 try catch 문을 사용하고, 그 외의 작업에는 사용하지 않는 것이 좋습니다. 또한, 예외 처리는 예외를 적절하게 처리하기 위한 것이므로, 예외 처리를 너무 단순화하거나 무시하는 것은 좋지 않습니다.

## 자바에서 @Scheduled 예제를 알려주세요

@Scheduled는 Spring Framework에서 제공하는 어노테이션으로, 주기적으로 작업을 실행할 수 있도록 도와줍니다. 자바에서 @Scheduled를 사용하는 예제 코드를 보여드리겠습니다.

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class ScheduledTasks {

    @Scheduled(fixedDelay = 5000)
    public void task1() {
        System.out.println("Task 1 executed at every 5 seconds.");
    }

    @Scheduled(cron = "0 0 12 * * ?")
    public void task2() {
        System.out.println("Task 2 executed at 12:00 pm every day.");
    }
}
```

위 코드에서는 Spring Framework의 @Scheduled 어노테이션을 사용하여 두 개의 작업을 주기적으로 실행합니다.

task1 메소드는 5초마다 실행됩니다. @Scheduled(fixedDelay = 5000)에서 5000은 밀리초 단위로 작성되어 있으므로, 5초를 의미합니다.
task2 메소드는 매일 오전 12시에 실행됩니다. @Scheduled(cron = "0 0 12 \* * ?")에서 cron 표현식을 사용하여 실행 시간을 지정합니다. 이 표현식은 "초 분 시 일 월 년" 형식으로 작성되며, *는 해당 필드의 모든 값, ?는 해당 필드가 지정되지 않음을 의미합니다. 위의 표현식은 매일 오전 12시를 의미합니다.
위 코드에서 @Component 어노테이션은 해당 클래스를 Spring Bean으로 등록합니다. 이렇게 등록한 후에는 @Scheduled 어노테이션을 사용하여 작업을 주기적으로 실행할 수 있습니다.

## 현재 애플리케이션이 REST 아키텍쳐를 따르며 스프링 부트는 model, controller를 맡으며 리액트가 맡은 view에서 api를 호출해 json 값을 받아오는데 json 값을 데이터베이스에 저장해 스프링 부트에서 받거나 리액트에서 지속적으로 api를 호출해 값을 받는 것 중 어떤게 성능 측면에서 더 나을까요?

이 질문에 대한 답은 정확한 상황과 요구 사항에 따라 다를 수 있습니다. 일반적으로 말하면, 데이터를 캐시할 수 없거나 사용자의 요청에 따라 값이 계속 변경되는 경우에는 리액트에서 지속적으로 API를 호출하여 값을 가져오는 것이 적절할 수 있습니다. 이 경우, 리액트에서 API를 호출하는 것은 사용자 경험 측면에서도 좋을 수 있습니다.

그러나 데이터를 캐시할 수 있고, 데이터의 변경이 상대적으로 적은 경우에는 스프링 부트에서 데이터를 저장하고, 필요한 경우에만 리액트에서 API를 호출하여 최신 데이터를 가져오는 것이 더 나을 수 있습니다. 이렇게 하면 데이터를 불필요하게 많이 조회하지 않아도 되므로 성능이 향상될 수 있습니다.

또한, 데이터의 크기와 처리 시간도 고려해야 합니다. 데이터가 매우 크고 처리 시간이 오래 걸리는 경우, 스프링 부트에서 데이터를 저장하고, 리액트에서는 적절한 요약 정보나 인덱스 정보만 가져오는 것이 좋습니다. 이렇게 하면 데이터 전체를 가져오는 것보다 효율적으로 데이터를 처리할 수 있습니다.

마지막으로, 데이터의 중요도와 보안성도 고려해야 합니다. 데이터가 중요하고 보안성이 높은 경우, 스프링 부트에서 데이터를 저장하고, 인증된 사용자만 접근할 수 있도록 보안을 강화하는 것이 좋습니다.

따라서, 성능 측면에서 어떤 방법이 더 나은지는 상황과 요구 사항에 따라 다르므로, 상황에 맞게 판단하고 선택하는 것이 중요합니다.

## 여기에서 정확한 상황과 요구 사항의 예시를 알려줄 수 있나요?

예를 들어, 다음과 같은 상황과 요구 사항이 있다고 가정해 봅시다.

상황: 온라인 상점에서 판매하는 상품 목록을 제공하는 웹 애플리케이션을 개발하고 있습니다. 상품 정보는 데이터베이스에 저장되어 있으며, RESTful API를 통해 브라우저에서 조회할 수 있습니다. 이 애플리케이션은 스프링 부트를 이용하여 개발되었으며, React를 이용하여 프론트엔드를 개발하고 있습니다.

요구 사항:

상품 정보는 데이터베이스에서 가져와 브라우저에 표시되어야 합니다.
상품 정보는 변경이 빈번하지 않으므로, 변경 사항이 있을 때만 데이터베이스에서 조회하도록 합니다.
상품 정보는 브라우저에서 자주 조회되므로, 성능을 최적화하여 빠르게 조회되어야 합니다.
상품 정보는 중요하고 보안성이 높으므로, 사용자 인증을 거쳐야만 조회할 수 있도록 합니다.
이러한 상황과 요구 사항에 따르면, 스프링 부트에서 상품 정보를 데이터베이스에 저장하고, 변경 사항이 있을 때만 데이터베이스에서 조회하도록 구현하는 것이 적절할 수 있습니다. 이렇게 하면 상품 정보를 자주 조회할 때마다 데이터베이스에서 값을 가져오는 것이 아니라, 캐시된 값으로 빠르게 조회할 수 있기 때문입니다. 또한, 상품 정보가 중요하고 보안성이 높으므로, 사용자 인증을 거친 후에만 조회할 수 있도록 보안을 강화해야 합니다.

그러나, 상황과 요구 사항에 따라서는 React에서 지속적으로 API를 호출하여 값을 가져오는 것이 더 적합한 경우도 있을 수 있습니다. 예를 들어, 상품 정보가 변경될 때마다 브라우저에서 실시간으로 반영되어야 하는 경우나, 데이터 크기가 작고 자주 조회될 때는 API를 호출하여 값을 가져오는 것이 더 효율적일 수 있습니다. 따라서, 상황과 요구 사항에 따라서 적절한 방법을 선택하는 것이 중요합니다.

## 주석을 잘 사용할 수 있는 예제를 알려주세요

다음은 주석을 잘 사용한 예제입니다.

```java
/**
 * This class represents a person with a name and age.
 * It provides methods to get and set the person's name and age.
 */
public class Person {

    private String name; // the person's name
    private int age; // the person's age

    /**
     * Constructs a person with a given name and age.
     * @param name the person's name
     * @param age the person's age
     */
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    /**
     * Gets the person's name.
     * @return the person's name
     */
    public String getName() {
        return name;
    }

    /**
     * Sets the person's name.
     * @param name the person's name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * Gets the person's age.
     * @return the person's age
     */
    public int getAge() {
        return age;
    }

    /**
     * Sets the person's age.
     * @param age the person's age
     */
    public void setAge(int age) {
        this.age = age;
    }
}
```

이 예제에서는 다음과 같은 주석이 사용되었습니다.

클래스 주석: 클래스의 역할과 사용 방법을 설명합니다.
필드 주석: 필드의 역할을 설명합니다.
생성자 주석: 생성자의 역할과 사용 방법을 설명합니다.
메소드 주석: 메소드의 역할과 사용 방법을 설명합니다.
주석은 코드를 읽는 사람이 이해하기 쉽도록 코드에 추가되는 설명입니다. 이 예제에서는 클래스, 필드, 생성자, 메소드에 대한 주석이 명확하고 자세하게 작성되어 있습니다. 이를 통해 코드를 이해하는 데 도움이 되며, 코드를 수정하거나 유지보수할 때도 유용합니다. 주석을 잘 사용하면 코드의 가독성과 유지보수성을 높일 수 있습니다.

## rowMapper 를 사용 안하는 방법이 있을까요?

```java
public List<Company> getAllCompanies() {
    String sql = "SELECT * FROM company";
    List<Company> companies = jdbcTemplate.query(sql, new CompanyRowMapper());
    return companies;
}

public class CompanyRowMapper implements RowMapper<Company> {
    @Override
    public Company mapRow(ResultSet rs, int rowNum) throws SQLException {
        Company company = new Company();
        company.setCompany(rs.getString("company"));
        company.setTitle(rs.getString("title"));
        company.setSalTpNm(rs.getString("salTpNm"));
        company.setSal(rs.getString("sal"));
        company.setMinSal(rs.getString("minSal"));
        company.setMaxSal(rs.getString("maxSal"));
        company.setRegion(rs.getString("region"));
        company.setHolidayTpNm(rs.getString("holidayTpNm"));
        company.setMinEdubg(rs.getString("minEdubg"));
        company.setCareer(rs.getString("career"));
        company.setRegDt(rs.getString("regDt"));
        company.setCloseDt(rs.getString("closeDt"));
        company.setZipCd(rs.getString("zipCd"));
        company.setStrtnmCd(rs.getString("strtnmCd"));
        company.setBasicAddr(rs.getString("basicAddr"));
        company.setDetailAddr(rs.getString("detailAddr"));
        company.setEmpTpCd(rs.getString("empTpCd"));
        company.setJobsCd(rs.getString("jobsCd"));
        company.setX(rs.getString("x"));
        company.setY(rs.getString("y"));
        return company;
    }
}

public List<Company> getAllCompanies() {
    String sql = "SELECT * FROM company";
    List<Map<String, Object>> rows = jdbcTemplate.queryForList(sql);
    List<Company> companies = new ArrayList<>();
    for (Map<String, Object> row : rows) {
        Company company = new Company();
        company.setCompany((String) row.get("company"));
        company.setTitle((String) row.get("title"));
        company.setSalTpNm((String) row.get("sal_tp_nm"));
        company.setSal((String) row.get("sal"));
        company.setMinSal((String) row.get("min_sal"));
        company.setMaxSal((String) row.get("max_sal"));
        company.setRegion((String) row.get("region"));
        company.setHolidayTpNm((String) row.get("holiday_tp_nm"));
        company.setMinEdubg((String) row.get("min_edubg"));
        company.setCareer((String) row.get("career"));
        company.setRegDt((String) row.get("reg_dt"));
        company.setCloseDt((String) row.get("close_dt"));
        company.setZipCd((String) row.get("zip_cd"));
        company.setStrtnmCd((String) row.get("strtnm_cd"));
        company.setBasicAddr((String) row.get("basic_addr"));
        company.setDetailAddr((String) row.get("detail_addr"));
        company.setEmpTpCd((String) row.get("emp_tp_cd"));
        company.setJobsCd((String) row.get("jobs_cd"));
        company.setX((String) row.get("x"));
        company.setY((String) row.get("y"));
        companies.add(company);
    }
    return companies;
}
```
