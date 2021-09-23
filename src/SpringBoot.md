# Spring Boot 2.x

1.关闭Spring Security认证

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        // 关闭spring security认证
        http.authorizeRequests()
                .anyRequest().permitAll()
                .and().logout().permitAll()
    }
}
```

2.Post请求报403错误，但Get请求正常

A：框架内部防止CSRF（Cross-site request forgery跨站请求伪造）的发生，限制了除了get以外的大多数方法，关闭CSRF即可

``` java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable();
    }
}
```

3.Postman测试文件上传（MultipartFile），后面MultipartFile一直为null

A：设置Postman的Body的form-data中的KEY的名称需和后台MultipartFile参数名称保持一致。如果api中的参数为 MultipartFile file，则postman中的key名称必须为file
