
�������ݿ⣺
Oracle      �׹���     �շ�
mysql       �׹���     ��ѡ���Դ
SQL server  ΢��
DB2         IBM
postgresql            ���
sqlite                �����������
access                ������

CentOS��װmysql

    ��ѯ��ж��
        #rpm -qa | grep mysql�����鿴����ϵͳ���Ƿ�װmysql���ݿ�
        #rpm -e mysql������ͨɾ��ģʽ
        ǿ��ɾ��ģʽ�����ʹ����������ɾ��ʱ����ʾ�������������ļ���
        ���ø�������Զ������ǿ��ɾ��
        #rpm -e --nodeps mysql��
		
    �鿴�밲װ
        #yum list | grep mysql �鿴�ṩ��mysql���ݿ⣬�����صİ汾
        #yum install -y mysql-server mysql mysql-devel ��װ
        #rpm -qi mysql-server �鿴�汾
		
    ��ʼ�����������
        #service mysqld start
        #chkconfig --list | grep mysqld �鿴�Ƿ񿪻�������
        #chkconfig mysqld on ���ÿ�������
		
	����˺ź͵�½
		#/usr/bin/mysqladmin -u root password root123��������mysql��root�˺�����
		#mysql -u root -p ��¼���ݿ�
		mysql> exit	�˳����ݿ�

	��Ҫ�����ļ�
		/etc/my.cnf �������ļ�
		/var/lib/mysql   ���ݿ��ļ����λ��
		/var/log ��־���λ��
		
	���ݿ�˿�
		#netstat -anp| grep 3306 
		
	��������
		mysql> show databases;
		mysql> create database [name];	�������ݿ�
		mysql> use [databasename];
		mysql> show tables;
		mysql> INSERT INTO user
				  (host, user, password,
				   select_priv, insert_priv, update_priv)
				   VALUES ('localhost', 'guest',
				   PASSWORD('guest123'), 'Y', 'Y', 'Y');
		mysql> FLUSH PRIVILEGES;
		mysql> SELECT host, user, password FROM user WHERE user = 'guest';

			ѡ��Ҫ������Mysql���ݿ⣬ʹ�ø����������Mysql���ֻ��Ը����ݿ⡣
		mysql>USE ���ݿ���;
			�г� MySQL ���ݿ����ϵͳ�����ݿ��б�
		mysql>SHOW DATABASES;
			��ʾָ�����ݿ�����б�ʹ�ø�����ǰ��Ҫʹ�� use������ѡ��Ҫ���������ݿ⡣
		mysql>SHOW TABLES;
			��ʾ���ݱ�����ԣ��������ͣ�������Ϣ ���Ƿ�Ϊ NULL��Ĭ��ֵ��������Ϣ��
		mysql>SHOW COLUMNS FROM ���ݱ�;
			����һ����testdb�����ݿ⣬������֧������
		mysql>create database testdb charset "utf8";
			ɾ�����ݿ�
		mysql>drop database testdb;
			��ʾ���ݱ����ϸ������Ϣ������PRIMARY KEY������)
		mysql>SHOW INDEX FROM ���ݱ�;
			ɾ����
		mysql> drop table student;
			�鿴��ṹ
		mysql> desc table_name;
			�鿴��ṹ�Ĵ�����¼
		mysql> show create table table_name;
		
		�������ݱ�
			�﷨
			CREATE TABLE table_name (column_name column_type);
			����
			mysql> create table student(
			   stu_id INT NOT NULL AUTO_INCREMENT,
			   name CHAR(32) NOT NULL,
			   age  INT NOT NULL,
			   register_date DATE,
			   PRIMARY KEY ( stu_id )
			);
			
		�﷨
		select column_name from table_name [where (column_name condition)] [order by column_name desc] [group by column_name]
		

		��ѯ
			��ʾȫ������Ϣ	
			mysql> select * from student;	*����ȫ��
			�ӵ�2��λ�ã���ʼ��ʾ3������Ϣ
			mysql> select * from student limit 3 offset 2;	
			ָ�����������ı���Ϣ��ʾ	
			mysql> select * from student where register_date > '2016-03-05';	
			ģ����ѯ		
			mysql> select * from student where name like "%Li";	 %���������ַ���%Li��ʾname��Li��β��ȫ����������

		����
			�������������ı���Ϣ
			mysql> update student set age=20, name='Tom' where stu_id > 4;	
			�޸��ֶ�����
			mysql> alter table student modify age int(2);
			�޸��ֶ���������
			mysql> alter table student change age new_age int;
			�޸ı���
			mysql> alter table student rename to student_new;

		���
			���һ�У�����Ԫ�أ�
			mysql> alter table student add age int(3) not null;
		
		
		ɾ��
			ɾ�����������ı���Ϣ
			mysql> delete from student where stu_id=6;	
			ɾ��һ�У�����Ԫ�أ�
			mysql> alter table student drop age;
		
		����
			�����������ı���Ϣ���н�������		
			mysql> select * from student where name like "%Li" order by stu_id desc;	

		����ͳ��
			����ָ���������б���Ϣͳ��
			mysql> select name, count(*) from student group by name;	
			����ָ���������б���Ϣͳ�ƣ�ͬʱͳ����������
			mysql> select coalesce(name,'total') as name, count(*)  as count from student group by name with rollup;		


		�������ʱ��֤��Ч��
				ʵ����������
			mysql> alter table student modify id int auto_increment;
				����student��
			mysql> 
				create table student(
				id int(11) not null auto_increment,
				name char(32) not null,
				age int not null,
				register_date date not null,
				primary key (id));
				����study_record��
			mysql> 
				create table `study_record` (
				`id` int(11) not null auto_increment,
				`day` int not null,
				`status` char(32) not null,
				`stu_id` int(11) not null,
				primary key (`id`),
				key `fk_student_key` (`stu_id`),
				constraint `fk_student_key` foreign key (`stu_id`) REFERENCES `student` (`id`)
				);
				��student���в�����Ϣ
			mysql> insert into student (name, age, register_date) values('Lucy', 19, '2017-04-02');
				��study_record���в�����Ϣ
			mysql> insert into study_record (day, status, stu_id) values (1, 'Yes', 2);
			
		����ѯ
			��������
				mysql> create table A (a int not null);
				mysql> create table B (b int not null);
			��������
				mysql> insert into A (a) values (1);
				mysql> insert into A (a) values (2);
				mysql> insert into A (a) values (3);
				mysql> insert into A (a) values (4);
				mysql> insert into B (b) values (3);
				mysql> insert into B (b) values (4);
				mysql> insert into B (b) values (5);
				mysql> insert into B (b) values (6);
			������������ȡ������ͬ�����ݣ�
				mysql> select * from A inner join B on A.a = B.b;
				mysql> select A.*, B.* from A, B where A.a = B.b;
			����Ƚ�A.a������ȫ����ӡ������B.b�����ݣ�����NULL�ı�ʾ���ֵĲ��A.a-B.b����
				mysql> select * from A left join B on A.a = B.b;
			����Ƚ�B.b������ȫ����ӡ������A.a�����ݣ�����NULL�ı�ʾ���ֵĲ��B.b-A.a����
				mysql> select * from A right join B on A.a = B.b;
			����
				mysql> select * from A right join B on A.a = B.b union select * from A left join B on A.a = B.b;
				mysql> select * from A full join B on A.a = B.b;��mysql��֧�֣�
				
		������ʱ��֤��Ч��
			һ����˵�������Ǳ�������4��������ACID���� Atomicity��ԭ���ԣ���Consistency���ȶ��ԣ���Isolation�������ԣ���Durability���ɿ��ԣ���
			1�������ԭ���ԣ�һ������Ҫô�ɹ���Ҫô���ء�
			2���ȶ��� �� �зǷ����ݣ����Լ��֮�ࣩ�����񳷻ء�
			3�������ԣ�����������С�һ���������Ľ����Ӱ��������������ô��������᳷�ء������100%���룬��Ҫ�����ٶȡ�
			4���ɿ��ԣ���Ӳ��������InnoDB���ݱ�������������־�ļ��ع��޸ġ��ɿ��Ժ͸��ٶȲ��ɼ�ã� innodb_flush_log_at_trx_commitѡ�� ����ʲôʱ������񱣴浽��־�
			mysql> begin;	��������
			mysql> insert into student (name, age, register_date) values ('David', 12, '2017-04-6');
			mysql> rollback;	����
			mysql> commit;	ȷ���ύ���޷��ٳ���
		
		����
			�鿴����
				mysql> show index from student;
			��������
				CREATE INDEX indexName ON mytable(username(length)); 
				mysql> create index index_name on student(name(32));
			ɾ������
				mysql> drop index index_name on student;
			
python��װmysql
	pip install pymysql
	
		
�μ�https://www.cnblogs.com/alex3714/articles/5950372.html
		
��ȨMysqlԶ�̷���
	mysql> grant all on *.* to admin@'localhost' identified by 'password';
	mysql> grant all on *.* to admin@'%' identified by 'password';
	mysql> flush privileges;

�鿴����ʹ�ö˿����
mysql> show global variables like 'port';

	
���⣺pymysql.err.OperationalError: (2003, "Can't connect to MySQL server on '192.168.***.***' (timed out)")	
���������
	��1���رշ���ǽ
	��2������3306�˿ڿ���ͨ������ǽ


CentOS�رշ���ǽ
	1����������������Ч��
	������chkconfig iptables on
	�رգ�chkconfig iptables off
	2����ʱ��Ч��������ʧЧ��
	������service iptables start
	�رգ�service iptables stop
	3 �鿴����ǽ״̬
	# service iptables status
		
Centos����3306ͨ������ǽ
	#vim /etc/sysconfig/iptables
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
	ע�������22������
	
�ο�http://www.centoscn.com/CentOS/help/2014/1030/4021.html
	

�鿴�û��嵥
	mysql> use mysql
	mysql> select user, password, host from user;

