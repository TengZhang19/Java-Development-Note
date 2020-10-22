# Spring MVC

## 一用IDEA建立项目


1. **创建MAVEN project**

2. **配置插件**
   - **cargo** 内置tomcat
   - **war**   自动打包war文件
3. **创建webapp/WEB-INF**
4. **配置Dispacher Servlet**
```xml
<properties>
  <!-- ... -->
  <servlet-api.version>~.~.~</servlet-api.version>
</properties>
<!-- ... -->
<dependencies>
<!-- ... -->
<dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>${servlet-api.version}</version>
      <!-- 指定依赖将由容器提供，缩减war文件大小  -->
      <scope>provided</scope>
</dependency>
</dependencies>
```
5. **创建WebAppInitializer实现WebApplicationInitializer接口**
6. **创建Controller 使用 @RequestMapping 的变体**
   - @GetMapping
   - @PostMapping
   - @PutMapping
   - @DeleteMapping
   - @PatchMapping
   - 使用@ResponseBody可以使返回值直接打印在页面上(不用view也可以)
7. **ViewResolver视图解析器与View视图**
   - JSP
   - Thymeleaf
8. **加入view前后缀自动处理**
```
@EnableWebMvc
@Configuration
@ComponentScan(basePackages="teng.springmvc")
public class WebConfig {

    // == constants ==
    public static final String RESOLVER_PREFIX="/WEB_INF/view/";
    public static final String RESOLVER_SUFFIX=".jsp";

    // == bean methods
    @Bean
    public ViewResolver viewResolver(){
        UrlBasedViewResolver viewResolver =
                new InternalResourceViewResolver();
        viewResolver.setPrefix(RESOLVER_PREFIX);
        viewResolver.setSuffix(RESOLVER_SUFFIX);
        return viewResolver;
    }
}
```
9. **Spring MVC 请求处理**

![SpringMVC_request_precessing](/images/SpringMVC_request_precessing.png)

10. **Model 与 ModelAttribute**

    Model由Dispacher Servlet创建,可以将其看做key-value map. 然后，就可以将ModelAttribute加入Model,这些ModelAttribute将对View可见

创建：

    //方法一
    //参数传入Model model

    model.addAttribute("user", "Tim");

    //log.info("modle= {}", model);

    //方法二

```java
//优先调用
    @ModelAttribute("welcomeMessage")
    public String welcomeMessage(){
        log.info("welcomeMessage() called");
        return "Welcome to this Demo application.";
    }
```

使用： ${user}

显示： Tim

spring IOP+Model使用逻辑：
![Model](/images/Model.png)
