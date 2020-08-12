# JDBC 설정

### dependency 추가

![image](https://user-images.githubusercontent.com/34564706/89361687-d74aca80-d706-11ea-8e1d-0e565fc169ce.png)

![image](https://user-images.githubusercontent.com/34564706/89361698-e29df600-d706-11ea-80a7-0e9c7be1e93f.png)

![image](https://user-images.githubusercontent.com/34564706/89361592-a36fa500-d706-11ea-961a-f84912b818b3.png)

![image](https://user-images.githubusercontent.com/34564706/89361640-c1d5a080-d706-11ea-90bd-eaf5097102c5.png)

```XML
		<!-- ORACLE 11g-->
		<dependency>
			<groupId>com.oracle</groupId>
			<artifactId>ojdbc6</artifactId>
			<version>11.2.0.3</version>
			<scope>system</scope>
			<systemPath>
			${project.basedir}\src\main\webapp\WEB-INF\classes\ojdbc6.jar
			</systemPath>
		</dependency>
```



### ojdbc6.jar 복붙

<img src="https://user-images.githubusercontent.com/34564706/89175832-7c5c8a80-d5c3-11ea-9621-7121ac02156d.png" width=500></img>

<img src="https://user-images.githubusercontent.com/34564706/89175884-926a4b00-d5c3-11ea-8816-1d5129ad5da9.png" width=500></img>

<img src="https://user-images.githubusercontent.com/34564706/89175924-a01fd080-d5c3-11ea-9e5a-472b8d81937d.png" width=300></img>

![image](https://user-images.githubusercontent.com/34564706/89365209-1a10a080-d70f-11ea-9882-947624855925.png)

![image](https://user-images.githubusercontent.com/34564706/89365272-37456f00-d70f-11ea-863d-cec91b875fde.png)

<img src="https://user-images.githubusercontent.com/34564706/89365319-50e6b680-d70f-11ea-90ab-127847210334.jpg" width=500></img>
