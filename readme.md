# SMARTPING #
## ���� ##
SmartPingΪһ��������(��)��以PING��⹤�ߣ�֧�ֻ�PING������PING���������˼���������

##���� ##

 - �����以PING������PING����ͼ
 - ���ƻ�PING����������˼���������

## ���˼�� ##
��ϵͳ���Ϊ�����Ļ�ԭ�����е����ݾ��洢������У�Ĭ������ѭ������1����ʱ�䣬�����������ݻ��� ��PING�� ��״̬���ɸ�����������ݻ��� ��PING�� ��״̬����API�ӿڻ�ȡ���������ݻ�������PING����ͼ������ͼ�д��ڱ������ܣ���������ΪThdchecksec�����ڷ��ִ��ڵ���Thdoccnum���ӳٳ���Thdavgdelay����򶪰��ʴ���Thdloss%�������������ñ����������ͬʱ��Alertsound�������ѡ�
    
## �����ļ� ##
    {
      "Name": "Localhost",
      "Ip": "127.0.0.1",
  
      "_comment_thd":"Thdchecksec,Thdoccnum,Thdloss,Thdavgdelay����Ϊ���ñ������򣬷ֱ��Ӧ������ڣ������ʣ�ƽ���ӳ٣���������",
      "Thdchecksec" : 900,"Thdloss" : 30,"Thdavgdelay" : 200,"Thdoccnum" : 1,
    
      "_comment_topo":"Alertsound,Tline,Tsymbolsize,Topotimeout����Ϊ�������˱���ʱʹ�ã��ֱ��Ӧ�������������߿�ȣ�ͼ�δ�С�����˼���ó�ʱʱ��",
      "Alertsound" : "http://mp3.13400.com:99/1917/001204170042283.mp3","Tline":"1","Tsymbolsize":"70","Topotimeout":"5",
    
      "Targets": [
        {
          "Name": "����","Addr": "127.0.0.1","Interval": "5","Type":"CS"
        },
        {
          "Name": "NOPING","Addr": "93.46.8.89","Interval": "5","Type":"CS"
        },
        
        {
          "Name": "IP_10_0_0_51","Addr": "10.0.0.51","Interval": "5","Type":"CS"
        },
        {
          "_comment":"��������Thdchecksec,Thdoccnum,Thdloss,Thdavgdelay�����Ե������ã��������õĹ�������",
          "Name": "IP_10_0_15_1","Addr": "10.0.15.1","Interval": "5","Type":"CS","Thdchecksec" : 30,"Thdoccnum" : 1,"Thdloss" : 50,"Thdavgdelay" : 200
        }
        {more...}
      ]
    }
    
**ע�⣺**

  - Ŀ������б�(Targets)��Ҳ��Ҫ������������Ϣ������������ͼ�н�����ʾ����
  - PING��������ҪС��60��Ŀǰ��ͼ��һ����һ���㣬������60�����ֶϵ�
  - Ŀ�����ģʽ,Client����ֻ����PING�������ᷢ��PING����CS���ȷ�PING��Ҳ��PING��������ͼ������Ϊ�������߻�˫������
  - ��������Targets�ڵı������ڣ��������������ʣ�ƽ���ӳٽ����û�������


## ���ݿ� ##
���ݿ��д洢PING����־���ݣ�Ĭ��ѭ������һ�������ݣ���ࣨ31*24*60*n=44640*N����

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

