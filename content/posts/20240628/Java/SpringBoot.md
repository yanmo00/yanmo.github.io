## 一、基础知识

### 1.Spring与SpringBoot

- Spring的缺点

  - 配置繁琐

  - 依赖繁琐

- SpringBoot的功能

  - 自动配置
  - 起步依赖：依赖传递
  - 辅助功能

总结：SpringBoot提供了一种快速开发Spring项目的方式，而不是对Spring功能上的增强

### 2.SpringBoot的实现步骤

1. 创建Maven项目
2. 导入SpringBoot起步依赖
3. 定义Controller
4. 编写引导类
5. 启动测试
6. 总结
   1. SpringBoot在创建项目时，使用jar打包方式
   2. SpringBoot的引导类，是项目入口，运行main方法就可以启动项目
   3. 使用SpringBoot和Spring构建的项目，业务代码编写方式一样

### 3.注解：

- `@RestController` **是一个组合注解**，
  - 结合了 `@Controller` 和 `@ResponseBody` 注解的功能（就相当于把两个注解组合在一起
  - 在使用 `@RestController` 注解标记的类中，每个方法的返回值都会以 JSON 或 XML 的形式直接写入 HTTP 响应体中，相当于在每个方法上都添加了 `@ResponseBody` 注解。
- @RequestMapping表示共享映射，
  - 如果没有指定请求方式，将接收GET、POST、HEAD、OPTIONS、PUT、PATCH、DELETE、TRACE、CONNECT所有的HTTP请求方式
  -  @RequestMapping("/user/register")会映射到方法上   ”localhost:8080/user/register“

- @SpringBootApplication用于标注一个 Java 类作为 Spring Boot 应用程序的主应用程序类。

### 4.![image-20240627192737988](https://minio-api.amjacks.cn:443/hjs/image-20240627192737988.png)

### 