
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


		���
			ʵ����������
			mysql> alter table student2 modify id int auto_increment;


python��װmysql
	pip install pymysql
	
		
		
		
