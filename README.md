# Install Kafka with Zookeeper on Linux
## 1) Install Java JDK version 11

      wget -O- https://apt.corretto.aws/corretto.key | sudo apt-key add - 
      sudo add-apt-repository 'deb https://apt.corretto.aws stable main'
      sudo apt-get update; sudo apt-get install -y java-11-amazon-corretto-jdk

Please follow the instructions  [here](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/generic-linux-install.html)  to verify your installation of Amazon Corretto 11 and set the JDK as your default Java in your Linux system.

Upon completion, you should get a similar output when doing  `java -version`:


    openjdk version "11.0.10" 2021-01-19 LTS
    OpenJDK Runtime Environment Corretto-11.0.10.9.1 (build 11.0.10+9-LTS)
    OpenJDK 64-Bit Server VM Corretto-11.0.10.9.1 (build 11.0.10+9-LTS, mixed mode)shell
