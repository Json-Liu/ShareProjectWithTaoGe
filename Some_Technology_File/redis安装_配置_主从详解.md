##Redis ��װ ���� ���� ���
###1����װ Redis
****
>�л��� cd /usr/local/    ����������Ŀ¼�£�Ҳ�����Զ�������Ŀ¼��
>���أ� wget http://download.redis.io/releases/redis-3.2.0.tar.gz
>��ѹ�� tar xzf redis-3.2.0.tar.gz
>�л��� cd redis-3.2.0
>���룺 make �������Ȱ�װGCC ���û�а�װ  ��װGCC ��yum install gcc-c++��
****
###2�� ����Redis
>Redis�����ñȽϼ�  ֻ��һ�������ļ� redis.conf  ����redis�İ�װĿ¼�£���ѹ��Ŀ¼��

>����Ŀ¼��
>>mkdir /etc/redis            ������� redis.conf �����ļ�Ŀ¼
>>mkdir /var/redis/log    ������� redis ����־�ļ�Ŀ¼
>>mkdir /var/redis/run    ������� redis ��PID�ļ�Ŀ¼
>>mkdir /var/redis/dir    ������� redis �������ļ�Ŀ¼

>�޸����ã�
>>vim /etc/redis/redis.conf 
>>daemonize yes                                ���� redis ����ɺ�̨����
>>pidfile /var/redis/run/redis_6379.pid        ���� PID ���·��
>>logfilr /var/redis/log/redis_6379.log        ���� redis ��־���·��
>>dbfilename dump_6379.rdb
>>dir /var/redis/dir                            ���� redis �����ļ����·��
###3��������ر�
>cp redis-benchmark redis-cli redis-server /usr/bin/         �ѳ��õ�redis������� /usr/bin/ >Ŀ¼�� �����Ϳ���������·����ʹ�� redis �����Ϊ LINUX ���Զ��� /usr/bin/ Ŀ¼����������

>���� redis ����:
>>redis-server /etc/redis/redis.conf            ���� redis ���� ��ƷΪ�����ļ���Ĭ�ϵ� 6379
>>���� redis �����У�
>>>redis-cli ��Ĭ��ʹ�ö˿�Ϊ 6379 �� redis ���� �� �� redis-cli -p 6379
>>>127.0,0,1:6379> set name helloworld
>>>"OK"
>>>127.0,0,1:6379> get name 
>>>"helloworld"

>�ر� redis ����:
>>redis-cli shutdown  �� redis-cli -p 6379 shutdown �رն˿�Ϊ 6379 �� redis ����
>>�������ʵ����
>>>��װ�����úõ�ʵ���� redis ����ǰ��������
>>>�� /etc/redis Ŀ¼�¿��� redis.conf �����ļ�Ϊ redis_6380.conf ������������ redis_�˿ں� >>>������ʽ ����ʶ��
>>>�޸� redis_6380.conf �����ļ��е� �˿ں� PID�ļ� ��־���·�� �����ļ����·�� 
>>>������ʵ��: redis-server /etc/redis/redis_6380.conf

###4���������ӷ�����
>��һ�ַ���:�������ļ��м��� slave of IP �˿� EXP��slaveof 192.168.1.1 6379
>�ڶ��ַ��������� redis-cli ���е� redis ������ ����  slaveof 192.168.1.1 6379 ���� SLAVEOF ���� Ȼ��ͬ���ͻῪʼ
