
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
		#exit	�˳����ݿ�

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
		 FLUSH PRIVILEGES;
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


python��װmysql
	pip install pymysql
	
		
		
		
