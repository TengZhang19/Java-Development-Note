# Lombok 笔记

Idea 插件 用于简化java代码，如getter(),setter(),toString() 等方法

```java
@Getter
@Slf4j //logger
public class Person{
  private String firstName;
  private String lastName;
  private String age;

  @Getter(AccessLevel.NONE) //Setter同理
  private final NumberGenerator numberGenerator;
  //自动生成6个getter方法

  @Setter
  private int guess; //只为guess生成setter()
}
```

Lombok 在编译时自动生成getter() setter() toString()等方法，源码更加简洁

使用spring initialier搭建项目时可以自动s加入

**lomBok基础使用方法**

@Data 自动生成getter setter hashCode equals canEqual 等方法, 参数可以由 @EqualsAndHashCode 指定

![lombokData](/images/lombokData.png)

@NonNull 检查传入参数是否为null，用在参数前
![lombokNonNull](/images/lombokNonNull.png)
