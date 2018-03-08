# jenkins

https://www.devopslibrary.com/lessons/ccjpe-api
https://www.devopslibrary.com/
https://www.devopslibrary.com/lessons/jenkins-ha

http://container-solutions.com/running-docker-in-jenkins-in-docker/

https://support.cloudbees.com/hc/en-us/articles/217517477-Maven-jobs-and-Java-versions-compatibility

Tool chain solution for maven JDK6 builds 

  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.7.0</version>
       <configuration>
          <verbose>true</verbose>
          <fork>true</fork>
          <executable>${maven.compiler.executable}</executable>
          <compilerVersion>1.3</compilerVersion>
       </configuration>
  </plugin>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
      <execution>
        <goals>
          <goal>toolchain</goal>
        </goals>
      </execution>
    </executions>
    <configuration>
      <toolchains>
        <jdk>
          <version>1.6</version>
          <vendor>sun</vendor>
        </jdk>
      </toolchains>
    </configuration>
  </plugin>

  
Reference it on the chaild poms  
  
   <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
   </plugin>
   

<build>
  <plugins>   
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.7.0</version>
       <configuration>
          <verbose>true</verbose>
          <fork>true</fork>
          <executable>${maven.compiler.executable}</executable>
          <compilerVersion>1.3</compilerVersion>
       </configuration>
  </plugin>
</plugins>
</build>


 -Dmaven.compiler.source=1.6 
 -Dmaven.compiler.target=1.6 
 -Ddefault.java.version=1.6
 -Ddefault.java.home=/var/jenkins_home/workspace/maven/jdk1.6.0_45
 
 
 FROM jenkins/jenkins:2.89.4
USER root
RUN apt-get update && \
    apt-get install -y sudo awscli && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
#    echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
USER jenkins
