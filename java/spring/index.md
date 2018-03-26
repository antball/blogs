[spring session 实现单用户多账号登录](https://blog.csdn.net/u011244202/article/details/60468922)



### applicationcontext获取方式
    FileSystemXmlApplicationContext
    ClassPathXmlApplicationContext
    WebApplicationContextUtils.getWebApplicationContext(ServletContext sc);
     (WebApplicationContext) servletContext.getAttribute(WebApplicationContext.ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE);