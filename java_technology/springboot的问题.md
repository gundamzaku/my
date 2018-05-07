##### 添加bootstrap.yml文件不成功  

在resource/里面添加bootstrap.yml文件不成功，不知道何解。只要在pom里面添加  
```
	<repositories>
		<repository>
			<id>repo</id>
			<url>https://repo.spring.io/libs-milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
	</repositories>
  ```
  仓库就可以了。  

##### Intellij AutoWired检测报错

在setting里面Editor-Inspections-Spring-Spring Core-Code-Autowiring for Bean Class设置成Warnning即可。
