# Sqoop

> RDBMS와 하둡 사이터에서 데이터 이관을 지원하는 툴

```markdown
관계형 데이터베이스의 데이터를 HDFS, Hive, Hbase에 import하거나, 반대로 관계형 DB로 export할 수 있다.
```

## Sqoop 설치

* apache.org 홈페이지에서 1.4.6버전을 다운받는다.

  : 직접 다운받는 게 아닌 `wget`명령어를 이용해 다운

  > **`wget http://archive.apache.org/dist/sqoop/1.4.6/sqoop-1.4.6.bin__hadoop-1.0.0.tar.gz`**

* `tar`명령어를 이용해 압축파일을 푼다.

  > **`tar -zxvf sqoop-1.4.6bin__hadoop-1.0.0.tar.gz`**

* .bashrc 파일 수정

  > **`export HADOOP_COMMON_HOME=/home/hadoop/hadoop-1.2.1`**
  >
  > **`export HADOOP_MAPRED_HOME=/home/hadoop/hadoop-1.2.1`**
  >
  > **`export SQOOP_HOME=/home/hadoop/sqoop-1.4.6.bin__hadoop-1.0.0`**
  >
  > **`export PATH=$PATH:$SQOOP_HOME/bin`**

* 설정파일 실행

  > **`source .bashrc`**

* ojdbc6.jar을 sqoop의 lib으로 옮겨준다.

## import

> RDBMS의 데이터를 HDFS로

```markdown
sqoop
```

