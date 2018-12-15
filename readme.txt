搭建项目的时候 我遇见的几个坑 
我主要就是卡在几个依赖上好久

1.博客里写了要下载编译一下elastic-job-lite-starter-master 一开始没当回事 跳过了 
        这个要注意一下把这个项目弄到本地  install到maven仓库

        同理把其他几个包也install到本地库 下面是命令 我试了一下直接复制jar到仓库好像不行
        mvn install:install-file -Dfile=‪F:\t\com\alipay\alipay-sdk-java\20170725114550\alipay-sdk-java-20170725114550.jar -DgroupId=com.alipay -DartifactId=alipay-sdk-java -Dversion=20170725114550 -Dpackaging=jar
		mvn install:install-file -Dfile=‪‪F:\t\com\alipay\alipay-trade-sdk\20161215\alipay-trade-sdk-20161215.jar -DgroupId=com.alipay -DartifactId=alipay-trade-sdk -Dversion=20161213173952 -Dpackaging=jar
		mvn install:install-file -Dfile=‪‪‪F:\t\com\alipay\sdk-java\20161213173952\sdk-java-20161213173952.jar -DgroupId=com.alipay -DartifactId=sdk-java -Dversion=20161213173952 -Dpackaging=jar

        这个搞完之后 基本就能启动了

2.还有一个 jackson 的依赖报错 也要手动指定  不知道是不是我自己的问题
         <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
            <exclusions>
                <exclusion>
                    <groupId>com.fasterxml.jackson.core</groupId>
                    <artifactId>jackson-databind</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.8.4</version>
        </dependency>
3. 还有就是 对着改过的host把要装的东西都装好 像是 zk redis mq mysql


4.配置hosts
127.0.0.1 paascloud-mq-rabbit
127.0.0.1 paascloud-db-redis
127.0.0.1 paascloud-gateway
127.0.0.1 paascloud-db-mysql
127.0.0.1 paascloud-provider-uac
127.0.0.1 paascloud-provider-zk

5.启动顺序
  1. paascloud-eureka
  2. paascloud-discovery
  3. paascloud-provider-uac
  4. paascloud-gateway
  5. 剩下微服务无启动数序要求

