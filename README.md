## 测试Java项目的GitHub持续集成功能
> 通过GitHub的Action功能测试

- 通过命令行创建mvn项目
```
mvn archetype:generate
choose: maven-archetype-quickstart
# com/org/cn + your company name 
groupId:cn.ghrf
artifactId:your project name
# 打包时用的名字可以不同于项目名字
packageName:same as your groupId
```
- 修改pom.xml,保证编译器适应java11
```
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <maven.compiler.release>11</maven.compiler.release>
</properties>
<build>
  <pluginManagement>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.10.1</version>
      </plugin>
    </plugins>
  </pluginManagement>
</build>
```
- 右键`pom.xml`,Update Project Configuration
```
vscode中的settings文件夹内容会自动更新
```

- 确保打包后，包内有MainClass
```
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-jar-plugin</artifactId>
  <version>3.2.2</version>
  <configuration>
    <archive>
      <manifest>
        <mainClass>yc.ga.App</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
```

- 下载依赖并构建项目
```
mvn isntall
```

- 失败过程记录
```
# 在yml文件中：windows-latest
找不到 D:\settings.xml文件
# 在yml文件中：ubuntu-latest
Could not transfer artifact   authorization failed for
```