
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

