


获取物理机列表
====================

.. toctree::
   :maxdepth: 2
   :numbered:



概要
--------------------

返回当前区域项目所有物理机列表, 需要先通过身份验证获取 Token, 再带上这个 Token 去获取物理机列表。


API规范
--------------------------

获取物理机API入口与API列表如下：


    * API入口: http://api.scloudm.com/
    * API列表:

+------------------+-------------------------------+------------+--------------------------------+
|  资源            |  操作                         |  HTTP方法  |  URI路径                       |
+==================+===============================+============+================================+
|  pm              |  获取所有物理机列表           |  GET       |  /mana_api/pm                  |
+------------------+-------------------------------+------------+--------------------------------+

先认证并获取新令牌(已可用), 使用该令牌执行获取动作
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------+-------------------+-----------------+
|  HTTP方法  |  URI路径          |  描述           |
+============+===================+=================+
|  GET       |  /mana_api/pm     |  获取物理机列表 |
+------------+-------------------+-----------------+

请求参数

+-----------------------+----------+-----------------------------+
|  字段名               |  类型    |  描述                       |
+=======================+==========+=============================+
|  Sp-Agent             |  header  |  厂商类型如, 必须为scloudm  |
+-----------------------+----------+-----------------------------+
|  tenant_id（可选）    |  string  |  租户id                     |
+-----------------------+----------+-----------------------------+
|  region（可选）       |  string  |  所属区域                   |
+-----------------------+----------+-----------------------------+
|  f（可选）            |  int     |  分页起始点                 |
+-----------------------+----------+-----------------------------+
|  t（可选）            |  int     |  分页结束点                 |
+-----------------------+----------+-----------------------------+

请求样例

::


    curl  -i \
          -H 'X-Auth-Token: {token_id}' \
          -H 'Sp-Agent: scloudm' \
          -X GET 'http://api.scloudm.com/mana_api/pm?tenant_id=123456789&region=dongjing&f=1&t=10'



返回参数

+-------------------+-------------+-------------------------------------------------------------------------+
|  字段名           |  类型       |  描述                                                                   |
+===================+=============+=========================================================================+
|  pm_servers       |  array      |  包含了所有物理机列表，每个物理的详细信息                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  asset_id         |  string     |  物理机资产编号                                                         |
+-------------------+-------------+-------------------------------------------------------------------------+
|  ilo_state        |  int        |  ilo 是否可用   0,1                                                     |
+-------------------+-------------+-------------------------------------------------------------------------+
|  cpu_num          |  int        |  cpu 核数                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  create_at        |  string     |  创建时间                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  update_at        |  string     |  更新时间                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  state            |  string     |  物理机物理状态 removed、repaired,deleted,active                        |
+-------------------+-------------+-------------------------------------------------------------------------+
|  disk_size        |  int        |  磁盘大小                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  host_name        |  string     |  主机名                                                                 |
+-------------------+-------------+-------------------------------------------------------------------------+
|  ip               |  string     |  物理机ip，逗号分割                                                     |
+-------------------+-------------+-------------------------------------------------------------------------+
|  wan_ip           |  string     |  物理机外网ip，逗号分割                                                 |
+-------------------+-------------+-------------------------------------------------------------------------+
|  lan_ip           |  string     |  物理机内网ip，逗号分割                                                 |
+-------------------+-------------+-------------------------------------------------------------------------+
|  manufacturer     |  string     |  物理机厂商                                                             |
+-------------------+-------------+-------------------------------------------------------------------------+
|  mem_size         |  int        |  物理机内存                                                             |
+-------------------+-------------+-------------------------------------------------------------------------+
|  region           |  string     |  所属区域                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+
|  status           |  string     |  物理机状态 ('starting','running','stopping','stop')                    |
+-------------------+-------------+-------------------------------------------------------------------------+
|  snid             |  string     |  系统序列号                                                             |
+-------------------+-------------+-------------------------------------------------------------------------+
|  os_type          |  string     |  物理机操作系统                                                         |
+-------------------+-------------+-------------------------------------------------------------------------+
|  tenant_id        |  string     |  项目ID                                                                 |
+-------------------+-------------+-------------------------------------------------------------------------+
|  tenant_name      |  string     |  项目名称                                                               |
+-------------------+-------------+-------------------------------------------------------------------------+


返回样例

::


        HTTP/1.0 200 OK
        Content-Type: application/json
        Content-Length: 537
        Server: Werkzeug/0.10.4 Python/2.7.5
        Date: Thu, 28 Jan 2016 05:53:28 GMT

        {
          "code": 200,
          "msg": "",
          "total_count": 1,
          "pm_servers": [
            {
              "asset_id": "233",
              "ilo_state": 1,
              "cpu_num": 1,
              "create_at": "2016-01-22 00:00:00",
              "state": "active",
              "disk_size": 213,
              "host_name": "qiuqiu.com",
              "ip": null,
              "wan_ip": "222.73.193.33",
              "lan_ip": "192.168.0.2",
              "manufacturer": null,
              "mem_size": 213,
              "region": "dongjing",
              "status": "running",
              "snid": "123",
              "os_type": "1",
              "tenant_id": "123456789",
              "update_at": "2016-01-22 00:00:00"
            }
          ]
        }


错误返回样例

::


   HTTP/1.1 400 Bad Request
   {
     "msg": "Malformed request URL: URL's project_id 'e58c78fe826f4f0b890767a3e078101' doesn't match Context's project_id 'e58c78fe826f4f0b890767a3e0781019'",
     "code": 400,
     "reason": "Unauthorized"
   }