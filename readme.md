# SMARTPING #
## ���� ##
SmartPingΪһ��������(��)��以PING��⹤�ߣ�֧�ֻ�PING������PING���������˼���������

##���� ##

 - �����以PING������PING����ͼ
 - ���ƻ�PING����������˼���������

## ���˼�� ##
��ϵͳ���Ϊ�����Ļ�ԭ�����е����ݾ��洢������У�Ĭ������ѭ������1����ʱ�䣬�����������ݻ��� ��PING�� ��״̬���ɸ�����������ݻ��� ��PING�� ��״̬����API�ӿڻ�ȡ���������ݻ�������PING����ͼ������ͼ�д��ڱ������ܣ���������ΪThresholchecksec�����ڷ��ִ��ڵ���Thdoccnum���ӳٳ���Thresholdavgdelay����򶪰��ʴ���Thresholdloss%�������������ñ����������ͬʱ��Alertsound�������ѡ�
    
## �����ļ� ##
    {
      "Name": "����",                    <-�����ı�ʶ��֧������,Ӣ��,[�иܣ�����]���ܿ�ͷ��
      "Ip": "127.0.0.1",                <-������IP
      "Db": "./database.db",            <-�洢��¼�����ݿ�
      "Thdchecksec" : "900",                                                <-[����]��������
      "Thdoccnum" : "1",                                                    <-[����]����������
      "Thdloss" : "30",                                                     <-[����]��������-������
      "Thdavgdelay" : "200",                                                <-[����]��������-ƽ���ӳ�
      "Alertsound" : "http://mp3.13400.com:99/1917/001204170042283.mp3",    <-��������
      "Tline":"1",                                                          <-����ͼ�߿��
      "Tsymbolsize":"70",                                                   <-����ͼ���С
      "Targets": [              <-Ŀ������б�
        {
          "Name": "����",            <-Ŀ���������
          "Addr": "127.0.0.1",       <-Ŀ�����IP
          "Interval": "20",          <-ping������
          "Type":"CS"                <-Ŀ�����ģʽ(C:Client,CS,Client/Server),
          "Thdchecksec" : "900",     <-��������
          "Thdoccnum" : "1",         <-����������
          "Thdloss" : "30",          <-��������-������
          "Thdavgdelay" : "200"      <-��������-ƽ���ӳ�
        },
        {
          "Name": "����",
          "Addr": "10.10.12.2",
          "Interval": "20",
          "Type":"CS",
          "Thdchecksec" : "900",
          "Thdoccnum" : "1",
          "Thdloss" : "30",
          "Thdavgdelay" : "200"
        },
        ...
      ]
    }
    
**ע�⣺**

  - Ŀ������б�(Targets)��Ҳ��Ҫ������������Ϣ������������ͼ�н�����ʾ����
  - PING��������ҪС��60��Ŀǰ��ͼ��һ����һ���㣬������60�����ֶϵ�
  - Ŀ�����ģʽ,Client����ֻ����PING�������ᷢ��PING����CS���ȷ�PING��Ҳ��PING��������ͼ������Ϊ�������߻�˫������
  - ��������Targets�ڵı������ڣ��������������ʣ�ƽ���ӳٽ����û�������


## ���ݿ� ##
���ݿ��д洢PING����־���ݣ�Ĭ��ѭ������һ�������ݣ���ࣨ31*24*60=44640����

    CREATE TABLE pinglog (
        logtime   VARCHAR (8),
        ip        VARCHAR (15),
        name      VARCHAR (15),
        maxdelay  VARCHAR (3),
        mindelay  VARCHAR (3),
        avgdelay  VARCHAR (3),
        sendpk    VARCHAR (2),
        revcpk    VARCHAR (2),
        losspk    VARCHAR (3),
        lastcheck VARCHAR (16),
        PRIMARY KEY (
            logtime,
            ip
        )
    );
    CREATE INDEX pk_n_t ON pinglog (
        name,
        lastcheck
    );
    CREATE INDEX pk_i_t ON pinglog (
        ip,
        lastcheck
    );


## ʹ�� ##

**����**

nohup ./idcping >/dev/null 2>&1 &

**����**

http://ip:8899

**��ҳʾ����**

![index.jpg](_screen/index.jpg "")

��ɫ���ʹ��������������ƽ���ӳ٣���ɫ���ʹ���Ҳ��������������

**����ʾ����**

![topology.jpg](_screen/topology.jpg "")

Բ�δ���һ���㣬��ɫ��ʾ��������ɫ��ʾ��ǰ�鿴����ͼ���ڵĵ㵽�˵㲻ͨ����������ɫ������������ɫ�����쳣����ɫ����δ֪(�޷�ȡ������)

