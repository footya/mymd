>不适用eclipse调试方法

1. 当前工程目录 `mvn clean install`;
2. 生成的文件在**-web\output下**-1.0.0-SNAPSHOT.war;
3. copy **-1.0.0-SNAPSHOT.war 到 D:\apache-tomcat-7.0.41\webapps;
4. 执行D:\apache-tomcat-7.0.41\bin\startup.bat;
5. 打开http://localhost:8181/**-1.0.0-SNAPSHOT/;
6. 非java文件可以直接修改D:\apache-tomcat-7.0.41\webapps\hetu-1.0.0-SNAPSHOT下的文件测试
