---
title: 图数据库的基本使用
date: 2022-02-01 10:00:00
author: 陌上人如玉
---

# 简介

图数据与关系数据库对比

| **分类**   | 模型   | 优势                                   | 劣势                                     | 举例                   |
| ---------- | ------ | -------------------------------------- | ---------------------------------------- | ---------------------- |
| 关系数据库 | 表结构 | 数据高度结构化，一致性强，软件成熟度高 | 面向多跳的关联关系查询低效或不支持       | MySql Oracle SqlServer |
| 图数据库   | 图结构 | 针对关联关系的建模，操作非常高效       | 高度结构化的数据处理能力不及关系型数据库 | Neo4j TuGraph OrientDB |

> 面对海量数据的存储和处理问题，传统的关系数据库已经无法满足大部分的日常数据储存的需求。图数据库技术可以将关系信息储存为实体、灵活拓展数据模型。由于提供了对关联数据最直接的表达，以及图模型对异构数据天然的包容力。未来，图数据库技术必将成为最为热点的技术之一，为企业存储和分析大规模图数据提供强有力的支持。

# Orient DB

[官网org](https://orientdb.org/)

官方[DOC](http://orientdb.com/docs/3.0.x/)

 [English tutorial](https://www.tutorialspoint.com/orientdb/index.htm)

 [OrientDB 中文教程](https://www.yiibai.com/orientdb/orientdb_overview.html)

 [中文教程 2](https://www.w3cschool.cn/orientdb/orientdb_installation.html)

# gremlim

## 简介

什么是Gremlin？

Gremlin是一种图数据遍历的接口封装或者框架，类似于关系数据库中的Mybatis，将对于书库的访问操作封装到一套接口当中，使应用开发人员不用关心底层数据库的操作。

![](https://raw.githubusercontent.com/ConanSteve/images/master/blog/202204011535193.jpg)

## 连接

[doc](http://tinkerpop.apache.org/docs/current/reference/)

[gremlin中文文档](http://tinkerpop-gremlin.cn/)

 [gremlin安装](https://help.aliyun.com/knowledge_detail/92204.html)

[深入学习图数据库语言Gremlin 系列文章链接汇总](https://blog.csdn.net/javeme/article/details/82631834)

- 通过配置文件连接任意图数据库

```Shell
:remote connect tinkerpop.server conf/remote.yaml session
:remote console
connect remote:localhost/demodb admin admin
```

- 通过接口连接OrientDB

```Shell
g = org.apache.tinkerpop.gremlin.orientdb.OrientGraph.open("remote:localhost/mkg","admin","admin");
gt = g.traversal()
```

## 管理

[gremlin入门](https://blog.csdn.net/weixin_33895695/article/details/88678857?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-4.control) 

[gremlin语句详解](https://blog.csdn.net/weixin_42076409/article/details/80856911)

# 管理

OrientDB控制台模式：执行`sh console.sh` ，输入 

```
connect remote:localhost/test admin admin
```

然后执行SQL语句

## CRUD

- 创建实体类

```SQL
create class Entity extends V
create property Entity.name String
```

- 插入记录

```SQL
CREATE CLASS Customer 
CREATE PROPERTY Customer.id integer 
CREATE PROPERTY Customer.name String 
CREATE PROPERTY Customer.age integer
INSERT INTO Customer (id, name, age) VALUES (01,'satish', 25)
```

- 查询实体

```SQL
select from V limit 5 # select * from table_name limit 5
select from #34:823  # select * from table_name where id = 'xxx'
```

- 删除实体记录

```SQL
delete VERTEX from x_class_name
```

- 删除边

```JavaScript
delete edge where @class='belong_to'
```

# 实战

将关系数据库数据导入图数据库

# PythonGremlin

## Basic

如何修改pythongremlin连接指定的数据库？

修改 ‘config’ 目录下的demodb.properties文件中的 ‘orient-db-name’的值即可

> 注意：必须先将数据库关闭，再改文件，再重新启动数据库





## CRUD

[python 操作gremlin](https://www.it610.com/article/1280837636361043968.htm)

[gremlinpython包使用](https://pypi.org/project/gremlinpython/)

[gremlin_python使用及增删查改方法封装](https://blog.csdn.net/jackandsnow/article/details/100572659)

## Demo

```Python
# gremlinpython==3.5.0
from gremlin_python import statics
from gremlin_python.structure.graph import Graph
from gremlin_python.process.graph_traversal import __
from gremlin_python.driver.driver_remote_connection import DriverRemoteConnection

import xlrd


graph = Graph()
connection = DriverRemoteConnection('ws://localhost:8182/gremlin','g', username='root', password='admin')
g = graph.traversal().withRemote(connection)

def process():
    read_xlsx()
    return

def addV(vertexType, name):
    if 0 == len(g.V().hasLabel(vertexType).has("name",name).valueMap().toList()):
        vertHead = g.addV(vertexType).property("name",name).next()

def addE(edgeType, vheadId, vTailId, properties=None):
    '''
    add edge
    :param properties: property dict, like {'p1': 'value1', 'p2': 'value2'}
    '''
    index_key = vheadId+vTailId
    if 0 == len(g.E().hasLabel(edgeType).has("index_key",index_key).valueMap().toList()):
        edge = g.V(vTailId).as_("t").V(vheadId).addE(edgeType).to("t").property("index_key",index_key)
        
        if properties:
            for key in properties.keys():
                edge.property(key, properties.get(key))        
        edge.next()

def get_vertex_id(vertexType, name):
    return g.V().hasLabel(vertexType).has("name",name).id().next()["@value"]

def read_xlsx():
    data = xlrd.open_workbook("triple0707.xlsx")

    #handle first sheet
    table0 = data.sheets()[0]
    nrow0 = table0.nrows
    for row_index in range(1,nrow0-1):
        olympics = table0.cell_value(row_index,0)
        tech_name = table0.cell_value(row_index,2)

        addV("olympics", olympics)
        addV("technology",tech_name)
        vHeadId = get_vertex_id("olympics", olympics)
        vTailId = get_vertex_id("technology", tech_name)
        addE("apply", vHeadId, vTailId)

    #handle second sheet
    table1 = data.sheets()[1]
    nrow1 = table1.nrows
    for row_index in range(1,nrow0-1):
        tech_name = table1.cell_value(row_index,0)
        olympics_aspect_2 = table1.cell_value(row_index,2)
        olympics_aspect_1 = table1.cell_value(row_index,3)

        addV("technology",tech_name)
        addV("olympics_aspect_2", olympics_aspect_2)
        addV("olympics_aspect_1", olympics_aspect_1)
        vHeadId = get_vertex_id("technology", tech_name)
        vTailId = get_vertex_id("olympics_aspect_2", olympics_aspect_2)
        addE("support", vHeadId, vTailId)

        vHeadId = vTailId
        vTailId = get_vertex_id("olympics_aspect_1", olympics_aspect_1)
        addE("contain", vHeadId, vTailId)


    # handle third sheet
    table2 = data.sheets()[2]
    nrow2 = table2.nrows
    for row_index in range(1,nrow2-1):
        tech_name = table2.cell_value(row_index,0)
        domain_name = table2.cell_value(row_index,2)

        addV("technology", tech_name)
        addV("technology_domain",domain_name)
        vHeadId = get_vertex_id("technology", tech_name)
        vTailId = get_vertex_id("technology_domain", domain_name)
        addE("belong_to", vHeadId, vTailId)

    # handle fourth sheet
    table3 = data.sheets()[3]
    nrow3 = table3.nrows
    for row_index in range(1,nrow3-1):
        domain_name = table3.cell_value(row_index,0)
        olympics = table3.cell_value(row_index,2)
        weight = table3.cell_value(row_index,3)

        addV("technology_domain",domain_name)
        addV("olympics", olympics)
        vHeadId = get_vertex_id("technology_domain", domain_name)
        vTailId = get_vertex_id("olympics", olympics)
        addE("support", vHeadId, vTailId, properties={"weight":weight})
    
    return

try:
    process()
except Exception as e:
    print(e)
finally:
    connection.close()




```



```Python
# gremlinpython==3.5.0
from gremlin_python import statics
from gremlin_python.structure.graph import Graph
from gremlin_python.process.graph_traversal import __
from gremlin_python.driver.driver_remote_connection import DriverRemoteConnection

graph = Graph()
connection = DriverRemoteConnection('ws://localhost:8182/gremlin','g', username='root', password='admin')
g = graph.traversal().withRemote(connection)

def wiping_out_graph():
    print(g.V().count().next())
    print(g.E().count().next())
    g.V().drop().hasNext()
    g.E().drop().hasNext()
    print(g.V().count().next())
    print(g.E().count().next())
    print("graph cleared!")

def process():
    # test_addV()
    test_addE()
    # wiping_out_graph()
    print("count of vertex:"+str(g.V().count().next()))
    print("count of edge:"+str(g.E().count().next()))
    return

def add_vertex(label, filters = None, properties=None):
    """
    add vertex
    :param label: label, type: str
    :param filters: filters , type: dict
    :param properties: property dict, like {'p1': 'value1', 'p2': 'value2'}
    :return: vertex, Vertex(id, label)
    """
    travel = g.V().hasLabel(label)
    if filters:
        for key in filters.keys():
            travel = travel.has(key, filters.get(key))
    if 0 == travel.count().next():
        travel = g.addV(label)
        if properties:
            for key in properties.keys():
                travel.property(key, properties.get(key))
        return travel.next()



def add_edge(label, vheadId, vTailId, properties=None):
    '''
    add edge
    :param properties: property dict, like {'p1': 'value1', 'p2': 'value2'}
    '''
    index_key = vheadId+vTailId
    if 0 == g.E().hasLabel(label).has("index_key",index_key).count().next():
        edge = g.V(vTailId).as_("t").V(vheadId).addE(label).to("t").property("index_key",index_key)
        
        if properties:
            for key in properties.keys():
                edge.property(key, properties.get(key))        
        edge.next()

def drop_vertex(v_id=None, label=None, properties=None):
    """
    drop all vertex or specific vertex
    :param v_id: long vertex id or Vertex(id, label)
    :param label: label, type: str
    :param properties: property list, like ['p1', 'p2', {'p3': 'value'}]
    :return: None
    """
    travel = g.V()
    if v_id is not None:
        travel = travel.hasId(v_id).next()
    if label:
        travel = travel.hasLabel(label)
    if properties:
        for p in properties:
            if isinstance(p, dict):
                for key in p.keys():
                    travel = travel.has(key, p.get(key))
            else:
                travel = travel.has(p)
    travel.drop().hasNext()

def drop_edge(e_id=None, label=None, properties=None):
    """
    drop all edges or specific edge
    :param e_id: edge id, type str
    :param label: label, type: str
    :param properties: property list, like ['p1', 'p2', {'p3': 'value'}]
    :return: None
    """
    travel = g.E()
    if e_id is not None:
        travel = travel.hasId(e_id)
    if label:
        travel = travel.hasLabel(label)
    if properties:
        for p in properties:
            if isinstance(p, dict):
                for key in p.keys():
                    travel = travel.has(key, p.get(key))
            else:
                travel = travel.has(p)
    travel.drop().hasNext()


def get_vertex_id(label, properties=None):
    travel = g.V().hasLabel(label)
    if properties:
        for key in properties.keys():
            travel = travel.has(key, properties.get(key))
    return travel.id().next()["@value"]

def test_addV():
    add_vertex("person",filters={"name": "Bob"}, properties = {"name":"Bob", "age":15, "gender": "male"})
    add_vertex("person",filters={"name": "Tom"}, properties = {"name":"Tom", "age":15, "gender": "male"})
    # drop_vertex(label = "person",properties=[{"name": "Bob"}])

def test_addE():
    vHeadId = get_vertex_id("person", properties = {"name": "Bob"} )
    vTailId = get_vertex_id("person", properties = {"name": "Tom"} )
    add_edge("friend",vHeadId,vTailId)
    # drop_edge(e_id='#137:0')
    # drop_edge(label='friend',properties=[{"index_key":vHeadId+vTailId}])

# process()
# connection.close()

try:
    process()
except Exception as e:
    print(e)
finally:
    connection.close()

```

