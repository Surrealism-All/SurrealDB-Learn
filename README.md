# 第8章 新一代数据库SurrealDB

第八章将开启对于SurrealDB数据库的讲解，通过本章的学习将会了解到SurrealDB的概念，明确SurrealDB相比于其他数据库的优势。然后对其进行安装并通过一个个的例子系统地学习所有Cli命令操作，完成学习后读者将会完全掌握SurrealDB相关的操作。

## 8.1 什么是SurrealDB

SurrealDB 是一个分布式、高性能、可扩展的端到端云原生开源数据库。它专注于提供快速的存储和检索能力，并支持大规模数据处理和分析。SurrealDB的功能丰富，无论是简单的练手项目还是需要支持高性能的分布式应用程序都有很好的表现。它具有良好的可扩展性和灵活性，可以满足不同类型的应用程序需求。以下是 SurrealDB 的一些主要特点和功能：

1. 分布式架构：SurrealDB 使用分布式架构，可以在多个节点上存储和处理数据。这使得它能够处理大规模的数据集，并提供高可用性和容错能力。当前版本的SurrealDB已经支持通过Kubernetes进行分布式部署，将来将会增加更多部署方式。
2. 高性能：SurrealDB 采用了优化的数据存储和索引结构，以提供快速的数据访问速度。它支持基于内存和磁盘的存储引擎，并且针对不同类型的工作负载进行了优化。
3. 数据模型：SurrealDB 支持灵活的数据模型，包括键值对、文档和列族等。可以根据应用程序的需求选择适合的数据模型来存储和查询数据。
4. ACID 事务支持：SurrealDB 提供 ACID（原子性、一致性、隔离性和持久性）事务支持，确保数据的一致性和可靠性。可以使用事务来执行复杂的操作，同时保持数据的完整性。
5. 丰富的查询语言：SurrealDB 提供了强大的查询语言，可以使用类似 SQL 的语法进行数据查询和分析。它支持聚合操作、过滤条件、排序和连接等常见的查询操作，此外SurrealDB也支持使用如JSON Patch的方式对数据进行增删改查操作。
6. 优秀的扩展性：SurrealDB 具有良好的可扩展性，可以根据数据量和负载需求增加节点进行水平扩展。它可以自动分片和负载均衡数据，以提供高吞吐量和低延迟的访问性能。
7. 多语言支持：SurrealDB 提供了多种编程语言的客户端驱动程序和接口，可以方便地与各种应用程序集成。对于SurrealDB而言不仅可以使用热门的后端语言如Java、Rust、Golang也支持使用通过Node.js，JavaScript对数据库进行操作与管理。除此之外SurrealDB还支持直接使用发起网络请求的方式对数据库进行操作，这使得即使当前有些语言的 SDK并没有完全支持，也可以通过发起请求的方式进行集成。

## 8.2 与其他数据库相比新在哪里

SurrealDB 常常被称为新一代数据库或下一代数据库，所以在这节中我们需要讨论SurrealDB与传统数据库相比到底有哪些不同点或者说有哪些创新点使得它坐拥未来，下面就对其新颖之处进行盘点。

### 8.2.1 适应未来的架构与模型

SurrealDB采用分布式架构，它是一种分布式数据库系统，可以在多个节点上分布存储和处理数据。这使得它能够处理大规模的数据集，并提供高可用性和容错能力。而传统关系型数据库如 MySQL、Oracle、SQL Server 等通常都是针对单节点环境设计的，即将数据存储在单个服务器上，并通过单个实例进行访问和管理。因此，在这些传统数据库中，通常不包含分布式系统功能，也就无法进行分布式存储和处理。尽管传统数据库的存储和管理能力已经得到了极大的提升，但是在面对海量数据和高并发访问时，仍然存在性能瓶颈和可扩展性问题。

SurrealDB拥有丰富的数据模型以及大规模数据处理能力，支持灵活的数据模型，包括键值对、文档和列族等，可以根据应用程序的需求选择适合的数据模型来存储和查询数据并且SurrealDB 本身提供高性能的分布式数据处理和分析功能，支持海量数据的快速存储和检索。这使得它适用于处理需要进行复杂分析和处理的大型数据集的应用场景。对于如今这种数据大爆炸的时代有着天然的优势。

SurrealDB不是一个简单的数据库，而是一个可适应不同需求的集NOSQL与关系型数据库一体的超级数据库，开发者不仅可以将它当作传统关系型数据库，也可以将它当作像MongoDB那样的文档型数据库，还可以将它对标Neo4j，作为图形数据库使用，在多方面SurrealDB都提供了良好的支持。

#### 1.SurrealDB作为传统关系型数据库

作为传统关系型数据库，需要具备完整的数据的结构上的逻辑关系，拥有事务机制来保障数据的一致性，易于维护，有实体完整性、参照完整性以确保数据的安全和可靠。对于这些特性SurrealDB都能非常良好的实现。SurrealDB目前已经支持Rust、C、Java、Python等主流后端语言，后续还会增加更多语言的支持，对于前端而言目前SurrealDB支持直接使用JS进行操作，后续也会直接对多种主流前端框架进行支持，因此对于绝大多数程序而言都能进行快速的过渡和使用。接下来通过SurrealDB的系统模型与传统关系型数据库的系统模型进行对比来更好的理解，如图8-1所示。

![image-20231023201952914](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023201952914.png)

图8-1传统数据库与SurrealDB模型映射

图8-1展示了两者的模型映射关系，但对于没有接触过数据库中Records和Fields层一定会感到有些陌生，下面对SurrealDB的6层分别进行说明：

1. Namespace：命名空间是SurrealDB中最顶层的概念。它是数据库中的一个独立区域，用于组织和隔离不同的数据库和数据集。可以将命名空间看作是一个数据库容器，用于存储和管理多个子数据库。
2. Database：数据库是命名空间中的一个实体，用于组织和管理数据。在数据库中，可以创建多个表格以存储和组织数据。请不要将这个概念与“数据库”相混淆。
3. Tables：表是数据库中存储数据的主要结构。可以将其视为二维的数据表，类似于Excel表格或者说矩阵。每个表由列（字段Fields）和行（记录Records）组成。表中的每一列定义了特定类型的数据，而每一行则表示一个完整的数据记录。
4. Records：数据记录表示表的一行数据，它是字段的集合，对于记录而言它可以是独立的，也可以与其他记录之间建立关联关系。
5. Fields：字段是表中的一列数据，列的集合构成一条记录，字段的类型有很多，例如字符串、整型、浮点型、布尔型等，字段的类型一定程度上取决于数据库的设计。
6. Authentication Scopes：身份验证范围是SurrealDB中对于身份权限的一个概念，用于控制对数据库的访问权限。可以为每个数据库或表格配置特定的身份验证范围，以限制或允许不同用户、角色或组织的访问，以确保不同用户对数据库操作的安全性。SurrealDB被设计和开发为一个多租户数据库平台，具有高级[ namespace](https://surrealdb.com/docs/surrealql/statements/define/namespace) 层，用于分隔每个组织、部门或开发团队。 SurrealDB上的命名空间数量没有限制。

下面通过一张模型映射表来陈述传统型数据库和SurrealDB的概念映射，如表8-1所示。

表8-1 传统数据库与SurrealDB的概念映射

| 传统关系型数据库 | SurrealDB                                                    |
| ---------------- | ------------------------------------------------------------ |
| database         | database                                                     |
| table            | table                                                        |
| row              | record                                                       |
| column           | field                                                        |
| index            | index                                                        |
| primary  key     | record  id                                                   |
| transaction      | transaction                                                  |
| join             | [record links](https://surrealdb.com/docs/surrealql/datamodel/records), embedding and [graph relations](https://surrealdb.com/docs/surrealql/statements/relate) |

 

#### 2.SurrealDB作为文档型数据库

实际上SurrealDB的核心还是一个文档型数据库，通过其底层的键值存储引擎对记录进行存储，它可直接支持数组和集合类型的数据。具有灵活的数据模型，能够存储半结构化、非结构化和结构化数据，无需事先定义固定的表结构。这种无模式特性使开发人员能够以自由形式存储和查询数据，从而提高了应对需求变化和数据多样性的能力。NOSQL为现代数据需求提供了高效、可扩展的解决方案。各个模块都在其专业领域提供出色的功能，并与其他模块紧密合作，确保数据的快速存取、查询与分析。如图8-2所示。

 ![image-20231023202122227](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202122227.png)

图8-2 文档数据库与SurrealDB模型映射

同样也通过一张模型映射表来陈述文档型数据库和SurrealDB的概念映射，如表8-2所示。

表8-2 文档型数据库与SurrealDB概念映射

| 文档型数据库             | SurrealDB                                                    |
| ------------------------ | ------------------------------------------------------------ |
| database                 | database                                                     |
| collection               | table                                                        |
| document                 | record                                                       |
| field                    | field                                                        |
| index                    | index                                                        |
| ObjectId                 | record  id                                                   |
| transaction              | transaction                                                  |
| reference  and embedding | [record links](https://surrealdb.com/docs/surrealql/datamodel/records), embedding and [graph relations](https://surrealdb.com/docs/surrealql/statements/relate) |

 

#### 3.SurrealDB作为图形数据库

由于SurrealDB处理记录ID的方式以及从底层键值存储引擎获取单个记录的方式，它可以用于存储时间序列有序数据和高度连接的图形数据。使用图数据库可以更好地表达现实世界中的关系，非常直观且自然，便于建模。图数据库可以高效地插入大量数据。图数据库在知识图谱等领域有着广泛的应用。由于其高效的关联查询能力，知识图谱中可以应用图数据库来存储和查询信息。

最后也通过一张模型映射表来陈述图数据库和SurrealDB的概念映射，如表8-3所示。

表8-3 图数据库与SurrealDB概念映射

| 图数据库       | SurrealDB                                                    |
| -------------- | ------------------------------------------------------------ |
| database       | database                                                     |
| node  label    | table                                                        |
| node           | record                                                       |
| node  property | field                                                        |
| index          | index                                                        |
| Id             | record  id                                                   |
| transaction    | transaction                                                  |
| relationships  | [record links](https://surrealdb.com/docs/surrealql/datamodel/records), embedding and [graph relations](https://surrealdb.com/docs/surrealql/statements/relate) |

 

### 8.2.2 自我优化和强大的性能

SurrealDB 提供了自动化的配置和管理功能，包括自动分片、负载均衡、数据复制和故障恢复等，使得它更易于部署和管理。

强大的性能与可靠的自我优化，对于传统数据库而言常常需要开发者进行调优，实际上对于多数开发者而言这个过程是比较复杂的，而且需要一定的经验，对于基础类的优化例如：查询优化、数据库的设计优化以及并发控制，SurrealDB与传统数据库是相差不多的，但SurrealDB 针对大规模数据处理和分析等工作负载进行了优化，提供高效的查询和管理性能。它支持基于内存和磁盘的存储引擎，并且可以根据具体的工作负载进行自适应调整和优化。

### 8.2.3 多用户权限管理

SurrealDB拥有强大的用户权限控制，支持多角色多权限等级的数据库管理控制机制，SurrealDB 支持基于行级别的权限控制，可以对数据库中的每行数据进行细粒度的权限设置。这意味着可以根据具体需要，为不同的用户或用户组分配不同的权限，除了常见的读、写权限外，还可以对用户进行更细粒度的授权，如删除、更新、插入等操作权限。这使得权限管理更加灵活，可以满足不同应用场景的需求。此外SurrealDB 具备动态权限管理机制，可以在运行时根据需求灵活地调整和管理用户权限。管理员可以根据实际情况对用户权限进行动态授权、撤销或修改，而无需重启数据库或重置用户权限。

 

## 8.3 安装SurrealDB

SurrealDB支持Windows,Mac,Linux,Docker四种形式的安装，在本书中仅演示在Windows操作系统上安装SurrealDB数据库。对于其他安装方式可以参考SurrealDB官方文档[https://surrealdb.com/docs/installation](https://surrealdb.com/docs/installation，SurrealDB) 相较于一些传统数据库的安装而言SurrealDB的安装方式十分友好，只需要在终端下输入简单的一行命令便可以完成安装，安装成功后就可以在C盘的Program Files目录下的SurrealDB目录下找到SurrealDB的exe文件，并且以这种方式安装的SurrealDB会自动帮助用户配置环境变量，安装命令如下：

```shell
//windows操作系统下通过终端安装SurrealDB命令

iwr https://windows.surrealdb.com -useb | iex
```

 

完成安装后，再次打开终端输入surreal version或surreal help命令，若终端正常输出SurrealDB的版本或SurrealDB的LOGO标识和帮助命令信息就能够验证是否安装成功，安装成功如图8-3所示。

 ![image-20231023202242342](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202242342.png)

图8-3 SurrealDB检验安装成功

 

## 8.4 SurrealDB命令总览

SurrealDB命令行程序当前共有十个命令，下面就对这些命令进行梳理，本节结束后读者将大致掌握这些命令的用法以及子命令和相关参数。命令中有些知识点或许对读者来说并不了解，当遇到不了解的知识点时请查询8.5节中的SurrealDB基础知识说明进行学习。

完整的命令总览如表8-4所示。

表8-4 SurrealDB命令总览

| 命名     | 解释         | 例子                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| start    | 启动命令     | surreal  start -s --auth --user root --pass root memory      |
| sql      | 查询终端命令 | surreal  sql --conn http://127.0.0.1:10086 --user root --pass root --ns test --db test  –pretty |
| export   | 导出命令     | surreal  export --conn http://127.0.0.1:10086 --user root --pass root --ns test --db  test E://surreal_backup/ns_test_db_test.surql |
| import   | 导入命令     | surreal  import --conn http://127.0.0.1:10086 --user root --pass root --ns test2 --db  test2 E://surreal_backup/ns_test_db_test.surql |
| version  | 版本命令     | surreal  version                                             |
| upgrade  | 更新命令     | surreal  upgrade                                             |
| is-ready | 检查连接命令 | surreal  is-ready --conn http://127.0.0.1:10086              |
| backup   | 备份命令     | surreal  backup --user root --pass root http://127.0.0.1:10086 |
| validate | 验证命令     | surreal  validate E://surreal_backup/ns_test_db_test.surql   |

### 8.4.1 数据库启动命令（start）

通过使用surreal start相关命令便可以对数据库进行启动，由于启动命令的相关参数选项众多，接下来一点点进行解析，将启动命令融会贯通，首先在终端中使用surreal start –help得到启动命令的相关帮助信息，帮助信息以及解释如下：

```shell
// 终端中输入启动命令帮助命令获取帮助信息
> surreal start --help

// 启动数据库服务 ， 由于SurrealDB并不是开机自启动的，所以每次使用前需要使用启动命令开启SurrealDB服务。
// 后续可以使用bat脚本的方式使得SurrealDB在开机时进行自启动。
Start the database server

// 命令用法：surreal start [选项] [地址] 
// 方括号中的内容结合帮助信息中的对应Options和Arguments便可以推断得出。
Usage: surreal start [OPTIONS] [PATH]

// 变量
Arguments:
// [PATH] 地址变量用于设置存储数据的数据库路径
  [PATH]
          Database path used for storing data
	// env表示环境参数 ， 这里指出环境参数为可选值，默认为default。
	// default：表示默认的环境参数（用户不指定），使用memory，表示基于内存，使用该方式，SurrealDB在停机后会清除所有数据。
	// env：表示使用持久化的存储方案，即用户可以将数据存储到文件中，可选方式有很多：
	//	1. file:<path>
	// 	2. tikv:<addr>
	//	3.  file://<path>
	//	4. tikv://<addr>
	//	5. default：memory
          [env: SURREAL_PATH=]
          [default: memory]

// 选项
Options:
// -l , --log ： 表示使用的日志选项，SurrealDB会记录数据库操作日志以便在故障发生时更好的进行排错。
// SurrealDB的日志记录位置也取决于用户设置的数据存储位置，若使用memory模式则日志不会记录到规定的目录中。
// 例如设置了数据存储目录为E://surrealdb_datas，那么日志则会记录在该目录下的LOG文件中。
// SurrealDB默认使用的日志级别为info。
// SurrealDB的日志级别为： error > warn > info > debug > trace。
// 日志的可选值包括：
//	1.  none ： 不记录且不打印任何日志
//	2. full ：记录完整日志
//	3.  error：仅记录级别为错误（致命）级别的日志 
//	4. warn：仅记录日志级别为警告及以上级别的日志（ error + warn ）
// 	5.  info：仅记录日志级别为基础信息及以上级别的日志（ error + warn + info ）
// 	6.  debug：仅记录日志级别为调试及以上级别的日志（ error + warn + info + debug ）
// 	7.  trace：仅记录日志级别为跟踪及以上级别的日志（ error + warn + info + debug + trace ）
  -l, --log <LOG>
          The logging level for the database server

          [env: SURREAL_LOG=]
          [default: info]
          [possible values: none, full, error, warn, info, debug, trace]
// --no-banner ： 表示隐藏SurrealDB的LOGO，默认下开启
      --no-banner
          Whether to hide the startup banner

          [env: SURREAL_NO_BANNER=]
// -h --help ： 打印帮助信息，请使用`surreal start --help`
  -h, --help
          Print help (see a summary with '-h')

// 数据库相关参数
Database:
// --tick-interval：运行节点代理tick的间隔（包括垃圾收集），默认为10秒。
// 节点代理 tick的间隔时间应该根据具体业务场景和系统负载情况来设定。
      --tick-interval <TICK_INTERVAL>
          The interval at which to run node agent tick (including garbage collection)

          [env: SURREAL_TICK_INTERVAL=]
          [default: 10s]
// -s, --strict ： 表示启动数据库的严格模式，默认则使用普通模式，使用普通模式不需要指定该选项。
// SurrealDB的严格模式启动时系统会强制执行一些严格的内部规则和检查，以增强数据一致性和可靠性。
  -s, --strict
          Whether strict mode is enabled on this database instance

          [env: SURREAL_STRICT=]
// --query-timeout ： 设置一组语句可以运行的最长持续时间（ 超时时间 ），超出最长时间则会进行中断该语句并进行回滚，默认无需设置该参数。
      --query-timeout <QUERY_TIMEOUT>
          The maximum duration that a set of statements can run for

          [env: SURREAL_QUERY_TIMEOUT=]
// --transaction-timeout ： 设置执行一组事务的超时时间 ， 若事务超出该超时时间则表示事务失败那么就会取消该事务。
      --transaction-timeout <TRANSACTION_TIMEOUT>
          The maximum duration that any single transaction can run for

          [env: SURREAL_TRANSACTION_TIMEOUT=]
// 权限认证
Authentication:
// -u, --username ： SurrealDB启动时的用户名 ， 该选项可以简写为`--user`。
// 一般常使用root作为数据库的根用户名，当然也可以指定其他的用户名，这是任意的。
  -u, --username <USERNAME>
          The username for the initial database root user. Only if no other root user exists

          [env: SURREAL_USER=]
          [aliases: user]
// -p, --password ： 设置当前SurrealDB用户的密码，若数据库不存在其他用户则是根用户的密码。
// 同样该选项可以简写为`--pass`。
  -p, --password <PASSWORD>
          The password for the initial database root user. Only if no other root user exists

          [env: SURREAL_PASS=]
          [aliases: pass]
// --auth : 是否开启权限认证，默认不包含该选项，但当数据库涉及多用户和隐私数据时该选项就显得十分重要。
      --auth
          Whether to enable authentication

          [env: SURREAL_AUTH=]
// 数据库远程KV存储连接
Datastore connection:
// --kvs-ca ：指定用于与远程 KV 存储建立连接时的 CA（Certificate Authority）文件的路径。
// CA 文件包含了信任的根证书，用于验证远程 KV 存储的身份。
      --kvs-ca <KVS_CA>
          Path to the CA file used when connecting to the remote KV store

          [env: SURREAL_KVS_CA=]

// --kvs-crt : 指定用于与远程 KV 存储建立连接时使用的证书文件的路径。该证书用于验证 SurrealDB 的身份，以确保安全通信。
      --kvs-crt <KVS_CRT>
          Path to the certificate file used when connecting to the remote KV store

          [env: SURREAL_KVS_CRT=]

//--kvs-key ：指定用于与远程 KV 存储建立连接时使用的私钥文件的路径。私钥文件用于对连接进行加密和解密，确保数据传输的机密性。
      --kvs-key <KVS_KEY>
          Path to the private key file used when connecting to the remote KV store

          [env: SURREAL_KVS_KEY=]

// HTTP 服务器
HTTP server:
// --web-crt ：指定用于加密客户端连接的证书文件路径。该证书用于对客户端和服务器之间的通信进行加密，确保数据传输的安全性。
      --web-crt <WEB_CRT>
          Path to the certificate file for encrypted client connections

          [env: SURREAL_WEB_CRT=]
// --web-key ：指定用于加密客户端连接的私钥文件路径。私钥文件用于对加密通信的数据进行解密，确保只有合法的客户端能够访问服务器。
      --web-key <WEB_KEY>
          Path to the private key file for encrypted client connections

          [env: SURREAL_WEB_KEY=]

// --client-ip ： 指定用于检测客户端 IP 地址的方法。
// 该选项可以帮助SurrealDB连接客户端的 IP 地址，进行一些操作或记录日志等。
//  这个选项可以设置不同的值来指定不同的客户端 IP 检测方法（该选项可能会随着SurrealDB的更新增加更多的远程连接支持）：
//	1. none ： 不使用客户端 IP，即不获取客户端的 IP 地址
//	2. socket ： 使用原始套接字获取客户端的 IP 地址
//	3. CF-Connecting-IP ：使用云服务提供商 Cloudflare 的连接 IP 方法获取客户端 IP
//	4. Fly-Client-IP ： 使用 Fly.io 平台的客户端 IP 方法获取客户端 IP
//	5. True-Client-IP ： 使用 Akamai、Cloudflare 等服务商的真实客户端 IP 方法获取客户端 IP
//	6. X-Real-IP ：使用 Nginx 的真实 IP 方法获取客户端 IP
//	7. X-Forwarded-For ：使用来自其他代理的行业标准头部获取客户端 IP
      --client-ip <CLIENT_IP>
          The method of detecting the client's IP address

          [env: SURREAL_CLIENT_IP=]
          [default: socket]

          Possible values:
          - none:             Don't use client IP
          - socket:           Raw socket IP
          - CF-Connecting-IP: Cloudflare connecting IP
          - Fly-Client-IP:    Fly.io client IP
          - True-Client-IP:   Akamai, Cloudflare true client IP
          - X-Real-IP:        Nginx real IP
          - X-Forwarded-For:  Industry standard header used by many proxies

// -b, --bind ： 设置HTTP服务器连接地址，默认使用0.0.0.0:8000。
// 若个人使用建议使用127.0.0.1的本机地址，端口号设置[ 0 , 65535 ] , 建议端口号：[ 1024 , 49151 ]。
  -b, --bind <LISTEN_ADDRESSES>
          The hostname or ip address to listen for connections on

          [env: SURREAL_BIND=]
          [default: 0.0.0.0:8000]

// 功能
Capabilities:
// -A, --allow-all ： 表示允许所有的功能，包括：嵌入式脚本、游客用户执行查询、执行方法、出站访问。
// 请注意开启此选项可能会导致一些安全性问题，所以需要慎重考虑。
  -A, --allow-all
          Allow all capabilities

          [env: SURREAL_CAPS_ALLOW_ALL=]
// --allow-scripting ： 允许执行嵌入式脚本函数。启用此选项后，服务器允许执行嵌入在查询中的脚本函数，以扩展服务器的功能。
      --allow-scripting
          Allow execution of embedded scripting functions

          [env: SURREAL_CAPS_ALLOW_SCRIPT=]

//--allow-guests ：允许游客用户执行查询。当启用此选项时，服务器允许未经身份验证的用户执行查询操作，而无需登录或提供凭据。
      --allow-guests
          Allow guest users to execute queries

          [env: SURREAL_CAPS_ALLOW_GUESTS=]
// --allow-funcs ：允许执行特定的函数。你可以通过提供逗号分隔的函数名称列表来指定要允许执行的函数。
// 例如可以开启http::get则说明可以使用Http协议的get方法进行操作
      --allow-funcs [<ALLOW_FUNCS>...]
          Allow execution of functions. Optionally, you can provide a comma-separated list of function
          names to allow.
          Function names must be in the form <family>[::<name>]. For example:
           - 'http' or 'http::*' -> Include all functions in the 'http' family
           - 'http::get' -> Include only the 'get' function in the 'http' family


          [env: SURREAL_CAPS_ALLOW_FUNC=]
          [default: ]

// --allow-net ： 允许出站网络访问，允许所有出站网络访问意味着服务器可以与任何外部主机、服务或网络进行通信，不受限制。
      --allow-net [<ALLOW_NET>...]
          Allow all outbound network access. Optionally, you can provide a comma-separated list of targets
          to allow.
          Targets must be in the form of <host>[:<port>], <ipv4|ipv6>[/<mask>]. For example:
           - 'surrealdb.com', '127.0.0.1' or 'fd00::1' -> Match outbound connections to these hosts on any
           port
           - 'surrealdb.com:80', '127.0.0.1:80' or 'fd00::1:80' -> Match outbound connections to these
           hosts on port 80
           - '10.0.0.0/8' or 'fd00::/8' -> Match outbound connections to any host in these networks


          [env: SURREAL_CAPS_ALLOW_NET=]
// 拒绝所有功能，与-A相对
  -D, --deny-all
          Deny all capabilities

          [env: SURREAL_CAPS_DENY_ALL=]

      --deny-scripting
          Deny execution of embedded scripting functions

          [env: SURREAL_CAPS_DENY_SCRIPT=]

      --deny-guests
          Deny guest users to execute queries

          [env: SURREAL_CAPS_DENY_GUESTS=]

      --deny-funcs [<DENY_FUNCS>...]
          Deny execution of functions. Optionally, you can provide a comma-separated list of function
          names to deny.
          Function names must be in the form <family>[::<name>]. For example:
           - 'http' or 'http::*' -> Include all functions in the 'http' family
           - 'http::get' -> Include only the 'get' function in the 'http' family


          [env: SURREAL_CAPS_DENY_FUNC=]

      --deny-net [<DENY_NET>...]
          Deny all outbound network access. Optionally, you can provide a comma-separated list of targets
          to deny.
          Targets must be in the form of <host>[:<port>], <ipv4|ipv6>[/<mask>]. For example:
           - 'surrealdb.com', '127.0.0.1' or 'fd00::1' -> Match outbound connections to these hosts on any
           port
           - 'surrealdb.com:80', '127.0.0.1:80' or 'fd00::1:80' -> Match outbound connections to these
           hosts on port 80
           - '10.0.0.0/8' or 'fd00::/8' -> Match outbound connections to any host in these networks


          [env: SURREAL_CAPS_DENY_NET=]

```

接下来通过使用一张简单的表格来快速归纳启动命令的常用选项，以及给出相关例子进行快速记忆，见表8-5。

表8-5 常用启动参数解释表

| 选项                        | 说明                                                         | 例子                     |
| --------------------------- | ------------------------------------------------------------ | ------------------------ |
| --user  \| --username \| -u | -u,  --username ： SurrealDB启动时的用户名 ， 该选项可以简写为`--user`。用户名可用是任意的。 | --user  root             |
| --pass  \| --password \| -p | -p,  --password ： 设置当前SurrealDB用户的密码，若数据库不存在其他用户则是根用户的密码。该选项可简写为`--pass` | --pass  root             |
| --bind                      | -b,  --bind ： 设置HTTP服务器连接地址，默认使用0.0.0.0:8000。 | --bind  127.0.0.1:6787   |
| --strict  \| -s             | -s,  --strict ： 表示启动数据库的严格模式，默认则使用普通模式，使用普通模式不需要指定该选项。严格模式启动时系统会强制执行一些严格的内部规则和检查，以增强数据一致性和可靠性。 | --strict                 |
| --log  \| -l                | 表示使用的日志选项，SurrealDB会记录数据库操作日志以便在故障发生时更好的进行排错，默认info。  SurrealDB的日志级别为： error > warn > info > debug > trace。   日志的等级：  1. none ： 不记录且不打印任何日志  2.  full ：记录完整日志  3. error：仅记录级别为错误（致命）级别的日志   4.  warn：仅记录日志级别为警告及以上级别的日志（ error + warn ）  5. info：仅记录日志级别为基础信息及以上级别的日志（ error + warn + info ）  6. debug：仅记录日志级别为调试及以上级别的日志（ error + warn + info + debug ）  7. trace：仅记录日志级别为跟踪及以上级别的日志（ error + warn + info + debug + trace ） | --log  warn              |
| --auth                      | 是否开启权限认证，默认不包含该选项，但当数据库涉及多用户和隐私数据时该选项就显得十分重要。 | --auth                   |
| [path]                      | [PATH]  地址变量用于设置存储数据的数据库路径，默认为memory，表示基于内存，使用该方式，SurrealDB在停机后会清除所有数据。表示使用持久化的存储方案，即用户可以将数据存储到文件中，可选方式有很多：   1. `file:<path>`   2. `tikv:<addr> `  3. `file://<path>`   4. `tikv://<addr>`   5.`memory` | file://E://surreldb_data |

#### 1.基于Memory模式启动SurrealDB

SurrealDB默认使用内存模式进行启动，当然也可以直接进行指定，下面通过指定用户名为root，密码为root，绑定连接地址为127.0.0.1:10086进行启动，启动命令如下所示：

```shell
//指定memory

surreal start –-user root –-pass root –-bind 127.0.0.1:10086 memory

//默认无需指定memory，默认为memory模式

surreal start –-user root –-pass root –-bind 127.0.0.1:10086
```

启动后可以清晰的看到如下三块区域：

1. 启动的SurrealDB存储方式是基于内存进行存储的。
2. SurrealDB目前没有用户名为root的用户，所以该root用户将会被创建出来。
3. 目前SurrealDB绑定的连接服务地址为127.0.0.1:10086。

启动执行结果如图8-4所示。

 ![image-20231023202434993](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202434993.png)

图8-4 基于memory模式启动SurrealDB执行结果

#### 2.将数据持久化到文件中

基于内存启动的SurrealDB在停机后数据将会被清除，无法做到数据的持久化存储，在进行测试的时候无疑是很好的选择。若需要持久化数据则需要指定存储数据的地址，存储地址的指定方式有很多，以下是基于本地的存储方式，启动命令如下所示：

```shell
//指定本机地址，地址为E盘的surreal_datas目录

surreal start --user root --pass root --bind 127.0.0.1:10086 file:E://surreal_datas
```

启动后如内存模式一样，同样也关注这三块区域，第一块区域清楚地显式了SurrealDB的存储地址为E盘的surreal_datas目录，启动执行结果如图8-5所示。

 ![image-20231023202453693](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202453693.png)

图8-5 将数据持久化到文件中启动SurrealDB执行结果

使用持久化存储方式启动SurrealDB后会在指定的存储目录中创建7个文件：

1. 000004.log：这是一个日志文件，用于记录SurrealDB的操作日志。它包含了对数据库的增删改操作的详细记录，用于实现持久化和数据恢复。
2. CURRENT：用于记录当前使用的SurrealDB数据文件的编号。它存储一个数字，表示当前正在使用的数据文件的编号。当SurrealDB启动时，会读取CURRENT文件来确定要加载的数据文件。
3. IDENTITY：包含了SurrealDB实例的唯一标识符。它的内容可以用于识别不同的SurrealDB实例，以及与其他实例进行通信和同步数据。
4. LOCK：用于实现互斥锁。在SurrealDB中，只允许一个进程或线程访问数据库文件，以避免并发访问导致的数据损坏。LOCK文件用于确保只有一个实例可以同时访问数据库。
5. LOG：这是一个日志文件，记录了SurrealDB的运行日志和错误信息。它包含了诊断信息、调试信息等，用于帮助开发者跟踪和解决问题。
6. MANIFEST-000005： SurrealDB的元数据文件，记录了数据库中存在的数据文件列表和其对应的索引信息。它用于管理和维护数据库文件，以便实现数据的持久化和恢复。
7. OPTIONS-000007：包含了SurrealDB的配置选项。它记录了启动SurrealDB时使用的配置参数，如存储路径、数据文件大小、后台作业数等。这些配置选项可以影响SurrealDB的行为和性能。

文件存储目录如图8-6所示。

 ![image-20231023202501537](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202501537.png)

图8-6 持久化存储模式下的文件目录

#### 3.基于严格模式以及权限认证启动SurrealDB

SurrealDB默认来说是不启动严格模式的，严格模式启动时系统会强制执行一些严格的内部规则和检查，对于需要强可靠性的场景十分必要。而权限认证是当数据库涉及多用户和隐私数据时的必要需求。启动命令如下所示：

```
//使用严格模式启动SurrealDB且不指定登录用户

surreal start --strict --auth --bind 127.0.0.1:10086 file:E://surreal_datas

//使用严格模式启动SurrealDB且指定登录的用户名密码

surreal start --strict --user root --pass root --auth --bind 127.0.0.1:10086 memory
```

在这里主要关注到的是①号标志位的行，对比无认证方式这种方式实际上是更加推荐的，数据库启动的执行结果如图8-7所示。

 ![image-20231023202856803](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202856803.png)

图8-7 基于严格模式和权限认证启动SurrealDB执行结果

### 8.4.2数据库操作命令（sql）

通过使用surreal sql命令可以启动SurrealDB的命令行执行终端，该命令行终端是一种子终端，可以使用websocket协议或者http协议对SurrealDB进行连接，通常被使用在直接与数据库进行交互的场景中。它是一种自含式语言，允许用户在终端键盘上直接输入SQL命令来操作数据库。通过这种方式，可以进行各种数据的基本操作，包括增加数据、删除数据、修改数据以及查询数据。对于没有图形化界面的用户这种方式是十分有效的。需要注意的是，使用该命令的基础是已经开启了SurrealDB数据库服务，该命令的帮助解释信息如下：

```shell
//sql命令用于启动Surreal的命令行查询终端
Start an SQL REPL in your terminal with pipe support

// 命令用法：surreal sql [选项]
Usage: surreal sql [OPTIONS]

//选项
Options:
//表示指定数据库连接URL的方式和连接地址，默认使用websocket协议连接localhost:8000，当然也可以使用http协议进行连接，可以指定该选项别名为conn
  -e, --endpoint <ENDPOINT>    Remote database server url to connect to [default: ws://localhost:8000]
                               [aliases: conn]
//指定连接数据库的用户名，不同用户有不同的操作权限，连接别名user
  -u, --username <USERNAME>    Database authentication username to use when connecting [env:
                               SURREAL_USER=] [aliases: user]
//指定连接用户的密码，连接别名为pass
  -p, --password <PASSWORD>    Database authentication password to use when connecting [env:
                               SURREAL_PASS=] [aliases: pass]
//指定连接SurrealDB数据库的命名空间，该选项别名为ns
      --namespace <NAMESPACE>  The namespace selected for the operation [env: SURREAL_NAMESPACE=]
                               [aliases: ns]
//指定连接SurrealDB数据库的数据库名称，该选项别名为db
      --database <DATABASE>    The database selected for the operation [env: SURREAL_DATABASE=]
                               [aliases: db]
//设置数据库响应的打印方式为pretty，也就是更加优美的打印方式（格式化输出）
      --pretty                 Whether database responses should be pretty printed
//设置是否使用JSON方式进行发出结果
      --json                   Whether to emit results in JSON
//设置省略分号是否会导致换行，即可以多行进行数据库语句的编写方式
      --multi                  Whether omitting semicolon causes a newline
  -h, --help                   Print help

```



#### 1.使用Http协议连接SurrealDB

下面使用Http协议连接了SurrealDB服务，指定连接地址为127.0.0.1:10086，并设定连接时使用的用户名和密码，连接的命名空间和数据库，虽然这里的命名空间和数据库实际上都没有定义但可以在后续进行定义，连接命令和执行系列命令如下：

```shell
//使用http协议连接

surreal sql --conn http://127.0.0.1:10086 --user root --pass root --ns test --db test –pretty

//定义命名空间

define namespace test

//定义数据库

define database test

//定义表

define table user

//创建表中的数据

create user set userId = '1001', name = 'Matt';

//查询表

select * from user;
```

数据库连接并执行查询命令的执行如图8-8所示。

 ![image-20231023202948471](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023202948471.png)

图8-8基于Http协议连接数据库查询

#### 2.使用WebSocket协议连接SurrealDB

WebSocket协议允许与SurrealDB进行简单的双向通信，对比Http协议，它使得实时查询成为可能。而连接方式仅需将http改为ws即可，连接命令如下。

```shell
//使用websocket协议连接

surreal sql --conn ws://127.0.0.1:10086 --user root --pass root --ns test --db test --pretty
```



### 8.4.3 数据库脚本导出命令（export）

数据库导出命令用于将数据库中的数据和结构导出到一个文件或其他存储介质中，以便在需要时进行备份、迁移或与他人共享数据。对于通过内存模式启动的SurrealDB来说该命令显得更加重要，由于内存模式不会记录持久化数据，所以在进行一系列操作之后通过导出命令将数据进行持久化存储到文件中有利于下次重复利用，在使用导出命令时需要指定需要导出的命名空间和数据库以及导出的文件名，对于保存的文件后缀实际上SurrealDB没有加以限制，但建议是使用.surql作为后缀名来进行区分。导出命令的详细解释如下：

```
//导出当前数据的脚本
Export an existing database as a SurrealQL script

//用法：surreal export [选项] --namespace 命名空间 --database 数据库 导出文件
Usage: surreal export [OPTIONS] --namespace <NAMESPACE> --database <DATABASE> [FILE]

// 参数
Arguments:
//设置导出文件，默认为-，表示写在终端进行输出
  [FILE]  Path to the sql file to export. Use dash - to write into stdout. [default: -]

//选项
Options:
//表示指定数据库连接URL的方式和连接地址，默认使用websocket协议连接localhost:8000，当然也可以使用http协议进行连接，可以指定该选项别名为conn
  -e, --endpoint <ENDPOINT>    Remote database server url to connect to [default:
                               ws://localhost:8000] [aliases: conn]
//指定连接数据库的用户名，不同用户有不同的操作权限，连接别名user
  -u, --username <USERNAME>    Database authentication username to use when connecting [env:
                               SURREAL_USER=] [aliases: user]
//指定连接用户的密码，连接别名为pass
  -p, --password <PASSWORD>    Database authentication password to use when connecting [env:
                               SURREAL_PASS=] [aliases: pass]
//指定连接SurrealDB数据库的命名空间，该选项别名为ns
      --namespace <NAMESPACE>  The namespace selected for the operation [env: SURREAL_NAMESPACE=]
                               [aliases: ns]
//指定连接SurrealDB数据库的数据库名称，该选项别名为db
      --database <DATABASE>    The database selected for the operation [env: SURREAL_DATABASE=]
                               [aliases: db]
  -h, --help                   Print help

```

接下来使用导出命令对连接地址为127.0.0.1:10086的SurrealDB上的test命名空间下的test数据库进行导出，将导出脚本存储到E盘下的surreal_backup目录，存储文件名称为ns_test_db_test.surql，导出的完整命令如下：

```
//导出http://127.0.0.1:10086，用户名为root，密码为root，命名空间test，数据库test，存储脚本地址E://surreal_backup/ns_test_db_test.surql

surreal export --conn http://127.0.0.1:10086 --user root --pass root --ns test --db test E://surreal_backup/ns_test_db_test.surql
```

导出成功终端不会有任何输出结果，最终结果如图8-9所示。

 ![image-20231023204624144](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204624144.png)

图8-9数据库脚本导出结果

### 8.4.4 数据库脚本导入命令（import）

用于将 SQL 脚本文件中的数据导入到指定的数据库中，这些数据包括表结构和数据。可以通过该手段实现故障恢复，数据迁移或与他人共享已有数据。并且可以通过一些工具实现不同数据库之间的脚本互转以达到无痕切换功能。例如将MySQL数据库的脚本转为SurrealDB的脚本进行导入，以便于用户在切换数据库使用时保证数据不丢失。对于导入脚本命令的详细解释如下：

```
//导入数据库脚本到已经存在的数据库中
Import a SurrealQL script into an existing database

//用法：surreal import [选项] --namespace 命名空间 --database 数据库 导入文件
Usage: surreal import [OPTIONS] --namespace <NAMESPACE> --database <DATABASE> <FILE>

//参数
Arguments:
//导入的sql文件的地址
  <FILE>  Path to the sql file to import

//选项
Options:

//表示指定数据库连接URL的方式和连接地址，默认使用websocket协议连接localhost:8000，当然也可以使用http协议进行连接，可以指定该选项别名为conn
  -e, --endpoint <ENDPOINT>    Remote database server url to connect to [default:
                               ws://localhost:8000] [aliases: conn]
//指定连接数据库的用户名，不同用户有不同的操作权限，连接别名user
  -u, --username <USERNAME>    Database authentication username to use when connecting [env:
                               SURREAL_USER=] [aliases: user]
//指定连接用户的密码，连接别名为pass
  -p, --password <PASSWORD>    Database authentication password to use when connecting [env:
                               SURREAL_PASS=] [aliases: pass]
//指定连接SurrealDB数据库的命名空间，该选项别名为ns
      --namespace <NAMESPACE>  The namespace selected for the operation [env: SURREAL_NAMESPACE=]
                               [aliases: ns]
//指定连接SurrealDB数据库的数据库名称，该选项别名为db
      --database <DATABASE>    The database selected for the operation [env: SURREAL_DATABASE=]
                               [aliases: db]
  -h, --help                   Print help

```

接下来需要将原来的数据库停机然后重新启动，这里需要启动基于内存模式的SurrealDB来完成接下来的操作。启动完成后数据应该已经被清空，再次使用sql命令连接到当前数据库的查询子终端，然后创建好需要的命名空间和数据库后使用导入命令将之前导出的SQL脚本文件进行导入，完整示例命令如下：

```shell
//步骤1：重新启动基于内存的数据库，用户名root，密码root，绑定地址127.0.0.1:10086

surreal start --strict --auth --user root --pass root --bind 127.0.0.1:10086 memory

//步骤2-1：通过http协议连接

surreal sql --conn http://127.0.0.1:10086 --user root --pass root --ns test2 --db test2 --pretty

//步骤2-2：查看命名空间

info for namespace;

//步骤2-3：查看数据库

info for db;

//步骤2-4：定义test2命名空间

define namespace test2;

//步骤2-5：定义test2数据库

define database test2;

//步骤3：导入SQL脚本，设置导入的命名空间为test2，数据库为test2，导入文件地址为E://surreal_backup/ns_test_db_test.surql
 surreal import --conn http://127.0.0.1:10086 --user root --pass root --ns test2 --db test2 E://surreal_backup/ns_test_db_test.surql

//步骤4：查看导入的user表数据

select * from user;

info for table user;
```

步骤2中通过Http协议连接到SurrealDB，指明用户名和密码为root，并指定命名空间为test2，使用的数据库为test2进行连接。由于SurrealDB重新启动的关系，所以需要手动使用define命令创建命名空间和数据库，当然在创建前可以使用info语句对命名空间和数据库进行查看，避免重复创建，整体流程如图8-10所示。

 ![image-20231023204706465](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204706465.png)

图8-10步骤2完整操作

接下来执行步骤3，将之前导出的数据库SQL脚本导入新的数据库中，指定使用Http协议进行连接并同样指定正确的用户名密码，最后跟上SQL脚本的地址，若终端打印了INFO日志surreal::cli::import: The SQL file was imported successfully则说明脚本已经导入成功。成功结果如图8-11所示。

 ![image-20231023204712325](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204712325.png)

图8-11数据库SQL脚本导入结果

最后回到查询终端中使用select语句查询user表查看打印结果，若执行成功则会输出之前导出的user数据，结果如图8-12所示。

 ![image-20231023204716891](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204716891.png)

图8-12 验证SQL脚本导入的数据

### 8.4.5 数据库版本信息命令（version）

使用surreal version相关命令可以获取到SurrealDB的数据库版本信息，该命令有一个选项参数-e（--endpoint），使用该参数可以获取到指定远程服务器的数据库版本信息，而不使用该参数则获取本地安装的SurrealDB数据库版本以及对应安装的操作信息信息。命令使用如图8-11所示。

 ![image-20231023204724616](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204724616.png)

图8-11 查询数据库版本信息

由该命令得到当前操作系统使用的是windows x86_64，安装的SurrealDB的版本是1.0.0+20230913。实际上以下三个命令在本机上毫无任何区别，命令如下：

```shell
//通过http协议连接获取版本信息

surreal version -e http://127.0.0.1:10086

//通过websocket协议获取版本信息

surreal version -e ws://127.0.0.1:10086

//直接获取本机上的版本信息

surreal version 
```



### 8.4.6 数据库更新命令（upgrade）

SurrealDB的更新方式十分简单，更新和安装一样只需要一行命令即可，这无疑降低了使用者的操作复杂度，详细的命令解释如下。

```shell
//普通更新，更新到最新的稳定版本
surreal upgrade
//更新到非稳定版本
surreal upgrade –-nightly
//更新且不覆盖老版本
surreal upgrade –dry-run

//更新最新的稳定版本
Upgrade to the latest stable version
//用法：surreal upgrade [选项]
Usage: surreal upgrade [OPTIONS]

//选项
Options:
//nightly表示使用预发布版本，即非稳定的最新版本，包含很多稳定版中没有正式发布的功能
      --nightly            Install the latest nightly version
//指定版本进行安装
      --version <VERSION>  Install a specific version
//表示不要替换可执行文件，意思是下载更新后保留老版本，可以说这是一种追加更新而不是覆盖更新
      --dry-run            Don't actually replace the executable
  -h, --help               Print help

```



### 8.4.7数据库检查连接命令（is-ready）

数据库连接命令主要用于确认当前数据库是否连接成功，实际上对于任何操作前先确保连接是十分重要的。检查连接命令可以帮助使用者了解当前数据库的连接情况。这对于维护数据库的安全性和稳定性非常重要。检查连接的详细说明如下：

```shell
//检查http://127.0.0.1:10086是否连接成功
surreal is-ready --conn http://127.0.0.1:10086

//检查是否当前SurrealDB的连接已经准备好了
Check if the SurrealDB server is ready to accept connections
//用法：surreal is-ready [选项]
Usage: surreal is-ready [OPTIONS]
//选项
Options:
//表示指定数据库连接URL的方式和连接地址，默认使用websocket协议连接localhost:8000，当然也可以使用http协议进行连接，可以指定该选项别名为conn
  -e, --endpoint <ENDPOINT>  Remote database server url to connect to [default: ws://localhost:8000]
                             [aliases: conn]
  -h, --help                 Print help

```



### 8.4.8 数据库备份命令（backup）

可以通过surreal backup命令将数据备份到现有数据库中或从现有数据库中备份数据。数据库备份命令的重要性主要体现在提高系统的高可用性和灾难可恢复性。在数据库系统崩溃时，如果没有数据库备份，就无法找回数据。使用数据库备份来还原数据库是在数据库崩溃时提供最小代价的数据恢复最优方案。此外，根据不同的需求和场景，可以选择不同的备份策略，如完整备份和增量备份。数据库备份命令的详细解释如下所示：

```shell
//将本机的数据备份到其他的SurrealDB数据库中
surreal backup --user root --pass root http://127.0.0.1:10086 http://198.121.31.147:10086

//将数据备份到现有数据库或从现有数据库备份数据
Backup data to or from an existing database

//使用方法：surreal backup [选项] <FROM>（表示可加可不加）[INTO]
Usage: surreal backup [OPTIONS] <FROM> [INTO]

//参数
Arguments:
//导出的远程数据库或文件的路径
  <FROM>  Path to the remote database or file from which to export
//要导入的远程数据库或文件的路径，默认为-
  [INTO]  Path to the remote database or file into which to import [default: -]

//选项
Options:
//数据库连接时的用户名
  -u, --username <USERNAME>  Database authentication username to use when connecting [env:
                             SURREAL_USER=] [aliases: user]
//数据库连接时的密码
  -p, --password <PASSWORD>  Database authentication password to use when connecting [env:
                             SURREAL_PASS=] [aliases: pass]
  -h, --help                 Print help

```



### 8.4.9 数据库查询文件验证命令（validate）

要对SurrealQL本地文件执行验证需要使用surreal validate命令并指定验证文件的地址。数据库查询文件的验证命令详细解释如下：

```shell
//验证E://surreal_backup/ns_test_db_test.surql文件
surreal validate E://surreal_backup/ns_test_db_test.surql

//验证SurralQL查询文件
Validate SurrealQL query files
//用法：surreal validate [模式]
Usage: surreal validate [PATTERN]

//参数
Arguments:
//需要验证的文件的Glob模式，默认验证所有的后缀名为.surql文件
  [PATTERN]  Glob pattern for the files to validate [default: **/*.surql]

Options:
  -h, --help  Print help

```



### 8.4.10 数据库帮助命令（help）

若要查看命令行工具的常规帮助信息需要使用surreal help命令，该命令会打印出所需命令的帮助信息，所有命令行程序都应该包含该命令以提供良好的支持，对于子命令可以使用--help或-h的方式获取帮助。帮助命令的打印结果如图8-12所示。

 ![image-20231023204902118](E:\Rust\try\SurrealDB-Learn\README\imgs\image-20231023204902118.png)

图8-12 帮助信息的打印结果

## 8.5 SurrealDB命令基础知识说明

### 8.5.1 SurrealDB数据存储地址

在SurrealDB的start命令中，需要指定数据库的启动方式，分为基于内存的模式和持久化存储到文件目录中，这里来讨论一下持久化存储的文件目录写法。实际上主要分为file和tikv两种类型。其中file类型就是指的文件目录地址，而tikv类型实际上指的是TIKV集群的地址。

使用`tikv:<addr>`或`tikv://<addr>`来设置存储路径是指将数据存储到一个TIKV集群中。TIKV 是一个分布式事务键值存储引擎，可以提供高性能和可扩展的分布式存储服务。具体来说，`tikv:<addr>`中的`<addr>`是TIKV集群的地址。TIKV支持多种部署方式，如单机、本地虚拟机、Docker容器、Kubernetes部署等，因此`<addr>`的格式会有所不同。一般而言，`<addr>`应该包含至少一个IP地址和端口号（例如1.2.3.4:10086），以指定TIKV集群的入口地址。需要注意的是，在使用TIKV作为SurrealDB的存储引擎时，你需要先搭建好TIKV集群，并确保TIKV的稳定性和可靠性。另外，TIKV的部署和配置非常复杂，需要对TIKV有一定的了解和经验。所以不建议刚入门使用这种方式。

### 8.5.2 SurrealDB严格模式

SurrealDB 中的 --strict 参数可以设置系统的运行模式，分为严格模式和普通模式。严格模式下，系统会强制执行一些严格的内部规则和检查，以增强数据一致性和可靠性。与之相对，普通模式下，则不会进行这些额外的检查和限制。具体来说，SurrealDB 的严格模式包括以下几个方面的限制：

1. 强制使用顺序一致性协议：在严格模式下，系统只能使用顺序一致性协议，禁止使用其它类型的一致性协议（如最终一致性或弱一致性），以确保数据的一致性和可靠性。
2. 强制执行分区一致性：在严格模式下，系统会强制执行分区一致性，即每个分区中的数据必须保持一致性，不能出现数据冲突或数据不一致的情况。
3. 限制节点间消息延迟：在严格模式下，系统要求节点间消息传输的延迟不能太大，否则可能导致数据不一致或出现流量控制问题。
4. 额外的数据验证和恢复机制：在严格模式下，系统会增加一些额外的数据验证和恢复机制，以保障数据的完整性和正确性。

相比之下，普通模式则没有这些严格的限制和检查，系统运行更加灵活和容错。但是，在一些敏感性场合或需要高可靠性保障的应用中，建议采用严格模式，以确保数据的安全和稳定性。需要注意的是，切换系统运行模式可能会影响系统性能和效率，请在实践中选取适当的模式，并进行实验验证和性能评估。

### 8.5.3 节点代理间隔

SurrealDB 中运行节点代理 tick 的间隔默认为 10 秒，这个时间间隔是可以配置的。一般来说，节点代理 tick 的间隔时间应该根据具体业务场景和系统负载情况来设定。如果间隔时间太短，会导致过多的节点代理 tick 发送和处理，增加系统负载和网络流量，降低系统性能和效率。同时，频繁的数据同步和传输也可能引起网络拥塞和数据冲突等问题。但如果间隔时间太长，会导致节点状态同步不及时，可能会出现数据不一致等问题，从而降低系统可靠性和稳定性。因此，建议根据具体业务需求和系统特点，选择合适的节点代理 tick 时间间隔，并进行实验验证和性能调优。需要注意的是，在调整节点代理 tick 间隔之前，应该了解系统架构和流程，分析瓶颈和热点，通过优化算法、协议和网络拓扑等方式，尽量减少节点代理 tick 的数量和频率，提高系统可靠性和效率。

### 8.5.4 语句超时时间的作用

在 SurrealDB 中，--query-timeout 选项用于设置一组语句运行的最长时间。该参数并非必需设置，但在特定场景下可以提供一些好处。简单来说设置 --query-timeout 可以帮助限制长时间运行、无响应或需要实时响应的查询，以提高系统的资源利用率、可用性和性能。具体的超时时间应该根据业务需求和系统特点进行调整，并进行实验测试以确保合适性。需要设置 --query-timeout 的具体原因包括：

1. 避免长时间运行的查询占用资源：某些查询可能因为复杂性或数据量大而需要较长时间才能完成。如果不设置查询超时时间，这些长时间运行的查询可能会占用大量系统资源，导致其他查询或操作的响应时间延迟，甚至影响整个系统的正常运行。设置查询超时时间可以限制查询的执行时间，确保资源被合理分配和利用。这就是常说的慢SQL。
2.  防止长时间无响应的查询：有时候，查询可能由于各种原因导致无法正常响应。例如，查询语句可能会因为死锁、网络故障等问题而陷入无限循环或阻塞状态。如果没有查询超时时间的限制，这些无响应的查询可能会一直持续，并且无法自动取消，导致系统处于不可用状态。通过设置查询超时时间，可以在超过预设时间后中断无响应的查询，保证系统的可用性和稳定性。
3. 控制查询的响应时间：在某些情况下，对查询的实时性要求较高，不能容忍过长的查询响应时间。通过设置查询超时时间，可以控制查询的最长执行时间，确保查询能够在预期的时间范围内给出响应。这对于需要及时反馈结果的应用场景非常重要，可以提升用户体验和系统的交互性。试想对于用户来说，若一个查询功能等待了超过30s，用户一定认为该功能一定有什么问题或者网络环境有问题，无疑带给用户极差的体验。

如果一组语句超出了设置的最长时间，SurrealDB 会自动中断这个查询，并回滚已经执行的部分操作。具体来说，SurrealDB 会发送一个中断信号给当前正在执行查询的进程，通知其结束当前操作，并释放相应的锁和资源。同时，SurrealDB 会将当前事务标记为失败，回滚所有已经执行的语句，使其不产生影响。需要注意的是，在查询超时的情况下，SurrealDB 并不会主动释放所有已获取的资源。因此，开发者需要在代码中捕获查询超时的异常，并显式地释放相关的资源，以避免资源泄露和其它问题。当然，SurrealDB 的查询超时机制并非是百分之百可靠的。如果查询中涉及到大量数据和复杂操作，可能会存在一些延迟和误差。因此，在实际应用中，需要谨慎设置查询超时时间，并进行测试和优化，以确保系统的稳定性和正确性。

### 8.5.5 事务超时时间作用

在SurrealDB中设置--transaction-timeout用于约束执行一组事务的超时时间 ， 若事务超出该超时时间则表示事务失败那么就会取消该事务。简单来说设置事务的超时时间可以有效控制事务的执行时间，避免资源滥用、死锁等问题，提高系统的并发性能和用户体验。但需要根据具体的业务需求和系统特点来设置事务的超时时间，并进行测试和优化。设置事务的超时时间有以下几个好处：

1. 避免长时间事务占用资源：长时间运行的事务可能会占用数据库的资源，导致其他事务无法及时执行或受到影响。通过设置事务的超时时间，可以限制事务的执行时间，确保资源被合理分配和利用。当超过设定的时间后，系统可以自动中断长时间运行的事务，释放相关资源，防止资源的滥用和浪费。
2.  防止事务锁超时：在并发环境下，事务可能会因为等待资源而进入阻塞状态，例如等待其他事务释放的锁。如果等待时间过长，可能会造成事务锁超时，导致事务失败或出现死锁。通过设置事务的超时时间，可以避免潜在的死锁问题，当等待时间超过设定的超时时间时，系统会主动中断事务，避免出现死锁情况。
3.  提高系统的并发性能：长时间运行的事务会占用数据库的资源，并阻塞其他事务的执行，从而影响系统的并发性能。通过设置事务的超时时间，可以限制事务的执行时间，使得数据库资源可以更好地分配给其他事务，提高系统的并发处理能力和吞吐量。
4. 改善用户体验：一些应用场景对事务的响应时间有较高的要求，不能容忍过长的等待时间。通过设置事务的超时时间，可以确保事务在预期的时间范围内给出响应，提升用户体验和交互性。

### 8.5.6 什么是允许所有出站网络访问

SurrealDB可以允许所有出站网络访问，这是指在SurrealDB服务器中设置了--allow-net选项后，服务器将允许与服务器进行通信的数据包从服务器发出到外部网络。出站网络访问是指服务器主动发起的网络连接，可以用来与其他服务器、服务或资源进行通信。具体而言，当使用该选项并提供了目标列表时，服务器将允许与目标列表中指定的主机或网络进行通信。目标可以是主机名（如"[surrealdb.com](http://surrealdb.com)"）或IP地址（如"127.0.0.1"），还可以指定端口号（如":80"表示80端口）。如果目标是一个IP地址，还可以指定一个可选的子网掩码（如"/8"表示只允许与该IPV4网络中的任何主机通信）。允许所有出站网络访问意味着服务器可以与任何外部主机、服务或网络进行通信，不受限制。这对于需要与外部系统进行数据交换或获取外部资源的应用程序非常有用。然而，需要注意网络安全性，并确保只允许必要的出站连接，以防止潜在的安全风险。