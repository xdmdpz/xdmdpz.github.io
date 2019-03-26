---

title: Springboot2.0记录些区别
date: 2018-09-10 16:22:44
tags: java,springboot
header-img: "/img/if/111111.jpg"
subtitle: "最近在搭架子，用了最新的Springboot2.0，发现好多方法都启用了"
---



1. 使用spring mvc解决跨域问题

   之前的解决方案

   ```Java
   @Configuration
   public class CORSConfig extends WebMvcConfigurerAdapter {
   
       @Override
       public void addCorsMappings(CorsRegistry registry) {
          registry.addMapping("/**")//设置允许跨域的路径
                   .allowedOrigins("*")//设置允许跨域请求的域名
                   .allowCredentials(true)//是否允许证书 不再默认开启
                   .allowedMethods("GET", "POST", "PUT","PATCH", "DELETE")//设置允许的方法
                   .maxAge(3600);//跨域允许时间
       }
   }
   ```

   由于`WebMvcConfigurerAdapter`类过时

   所以使用如下方法实现

   ```java
   @Configuration
   public class CORSConfig implements WebMvcConfigurer {
   
       @Override
       public void addCorsMappings(CorsRegistry registry) {
           registry.addMapping("/**")//设置允许跨域的路径
                   .allowedOrigins("*")//设置允许跨域请求的域名
                   .allowCredentials(true)//是否允许证书 不再默认开启
                   .allowedMethods("GET", "POST", "PUT","PATCH", "DELETE")//设置允许的方法
                   .maxAge(3600);//跨域允许时间
       }
   
   }
   ```

2. SpringDataJpa分页接口Pageable的实现类PageRequest构造方法弃用

   old

   ```java
   new PageRequest(firstResult, maxResults, new Sort(...))
   ```

   new

   ```
   PageRequest.of(firstResult, maxResults, new Sort(...))
   ```
