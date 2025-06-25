![cover_image](https://mmbiz.qpic.cn/mmbiz_jpg/tZhja1CIKficoMozV1sDLg2gBFichjdMrx4ARICctyGTCLVc1EGCbYN9xicVFnLdcIAibH4mGzqH57nqqSdQQzZgCQ/0?wx_fmt=jpeg)

#  Cursor + PlantUML：告别手写 SQL 的高效工作流

原创  梁波Eric  [ Eric技术圈 ](javascript:void\(0\);)

__ _ _ _ _

** 见字如面，与大家分享实践中的经验与思考。  **

数据库设计是软件开发中的关键环节，但传统方法往往耗时且容易出错。你是否曾经面对以下困境？

  * 手写 SQL DDL 语句繁琐且容易遗漏字段或约束 
  * 设计变更后需要手动同步修改多处 SQL 代码 
  * 团队成员对数据库结构理解不一致，导致沟通困难 
  * 不同数据库系统需要编写不同方言的 SQL 

本文介绍一种高效解决方案：将 PlantUML 类图与 Cursor 编辑器结合，实现从直观的图形化设计到  ** 标准化 SQL 代码  **
的无缝转换。这种方法不仅提高开发效率，还能确保数据结构的一致性和可维护性。

##  PlantUML概述

PlantUML 是一款强大的开源工具，通过简洁的文本语言创建各种 UML
图表。在数据库设计中，类图特别实用，它可以直观表示实体及其关系。与传统数据库设计工具相比，PlantUML 具有明显优势：

  * ** 版本控制友好  ** ：基于文本，可以轻松集成到 Git 等版本控制系统 

  * ** 语法简单  ** ：即使初学者也能快速上手 

  * ** 支持多种输出  ** ：PNG、SVG、PDF 等多种格式 

  * ** 跨平台兼容  ** ：不依赖特定操作系统或环境 

###  Cursor 编辑器的优势

Cursor 是一款现代化代码编辑器，集成了强大的代码生成和理解功能。它能根据 PlantUML 类图智能生成各种数据库方言的 SQL
代码，极大简化了开发流程。

如果在 macOS 系统中执行如下命令：

    
    
    $ brew install graphviz

也可以直接去官网 (  ` https://graphviz.org/download/  ` ) 进行下载安装。

然后在 Cursor 的插件市场中，搜索 "PlantUML"，安装后，即可编辑 PlantUML 类图以及进行预览。

###  类图基本语法

PlantUML 的类图语法简洁明了，如下是它的基本属性：

  * ** 结构  ** ：类名、属性（字段）、方法（操作）。 

  * ** 符号表示的作用域  ** ： 

    * ` +  ` ：公有（Public），对所有的类都可见。 

    * ` -  ` ：私有（Private），仅仅只对当前类可见。 

    * ` #  ` ：保护（Protected），受保护的属性或者方法，其子孙类可见。 

    * ` ~  ` ：包内可见（Package/Default）。 

    * ` _  ` : 下划线，表示当前的这个类的方法或者属性是静态的。 

    * ` =  ` ：表示默认值 

在简单了解其基本概念后，设计数据库模型时，可以使用面向对象的命名方式：

    
    
    @startuml  
    class User {  
      -id: Integer  
      -username: String  
      -email: String  
      -createdAt: Date  
    }  
      
    class Post {  
      -id: Integer  
      -title: String  
      -content: String  
      -userId: Integer  
      -publishedAt: Date  
    }  
      
    User "1" -- "n" Post : creates  
    @enduml

![image-20250406下午102057617](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxO3TQQg58I1CibdiaT2d1bvnpGcJDpKjgVmkAD0pFspdphv8HP5b29XqA/640?wx_fmt=png&from=appmsg)

这段代码描述了一个简单的博客系统，用户可以创建多篇文章。注意使用了直观的命名和类型：

  * 类名和属性名采用驼峰命名法 
  * 数据类型使用 Java 风格（如  ` String  ` 、  ` Integer  ` 、  ` Date  ` ） 

  * 关系表示简单明了：  ` "1" -- "n"  ` 表示一对多关系 

###  关系表示方法

PlantUML 提供了丰富的关系表示方式，让你能精确表达各种业务关系：

  * ` --  ` 基本关联关系 

  * ` <--  ` 或  ` --> ` 带方向的关联 

  * ` --o  ` 或  ` o--  ` 聚合关系（空心菱形） 

  * ` --*  ` 或  ` *--  ` 组合关系（实心菱形） 

  * ` --|> ` 继承关系 

  * ` ..|> ` 实现关系 

在关系两端可以添加基数表示，例如  ` "1" -- "n"  ` ，  ` "0..1" -- "*"  ` ，使关系更加明确。查看以下图例会更加清晰：

![image-20250404下午50029633](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrx2BSocJFBibjBYVe1fdXrDFvFT8ibFg2OyDQ4hG6p0ga77WRRVlYcgMEg/640?wx_fmt=png&from=appmsg)

###  自定义约束和标签

在设计数据库时，需要指定各种约束。PlantUML 允许使用特殊标记来精确控制生成的 SQL：

  * ` <<PK>> ` \- 标记主键 

  * ` <<FK>> ` \- 表示引用关系（注意：不一定转换为数据库外键） 

  * ` <<NN>> ` \- 标记非空约束 

  * ` <<unique>> ` \- 标记唯一约束 

  * ` <<default: value>> ` \- 设置默认值 

  * ` <<index>> ` \- 创建索引 

例如：

    
    
    class User {  
      -id: Integer <<PK>>  
      -email: String <<NN, unique, index>>  
      -username: String <<NN, index>>  
      -lastLogin: Date <<index>>  
    }

###  继承与审计字段

数据库设计中经常需要为表添加审计字段（如创建时间、更新时间等）。使用 PlantUML 的继承机制，可以优雅地表达这种模式：

    
    
    @startuml  
    class BaseEntity {  
      -id: Integer <<PK>>  
      -createdAt: Date  
      -createdBy: String  
      -updatedAt: Date  
      -updatedBy: String  
      -isDeleted: Boolean <<default: false>>  
    }  
      
    class Product {  
      -name: String <<NN>>  
      -description: String  
      -price: BigDecimal <<NN>>  
    }  
      
    Product --|> BaseEntity  
    @enduml

![image-20250406下午102229889](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxKlMfthACntHd1EGeUiczEDxNzQDzr7el9T0ScsFnicm8hKotTUnicnxgA/640?wx_fmt=png&from=appmsg)

这样设计的好处是减少重复代码，使模型更加清晰，同时在生成 SQL 时会自动将基类的字段应用到子类中。

虽然继承机制在概念上很清晰，但在实际复杂项目中需要注意：  ** 当项目中有大量实体时，如果每个类都继承自
BaseEntity，会导致图表中出现大量指向基类的继承线，可能使类图变得复杂难读  ** 。

对于复杂项目，可以考虑以下简化策略：

  * 在初始设计阶段，先不使用继承表示审计字段，专注于业务模型 
  * 在生成SQL时，统一添加这些标准字段 
  * 对于文档展示，可以创建不同详细程度的类图版本 

继承方式适合小型项目或教学演示，而大型企业应用可能需要采用其他更灵活的方案。

##  常见问题解答（FAQ）

###  为什么选择 PlantUML 而非专业数据库设计工具？

传统数据库设计工具虽然功能丰富，但 PlantUML 结合 Cursor 的方案具有独特优势：

  * ** 无缝集成版本控制  ** ：PlantUML 是纯文本格式，可以像代码一样管理，方便追踪每次修改 

  * ** 多数据库一键适配  ** ：一次设计可轻松转换为多种数据库方言，不必重复工作 

  * ** 开发流程一体化  ** ：设计即文档，与代码库共同演进，始终保持同步 

  * ** 降低学习成本  ** ：开发人员不需要切换思维模式，可以保持面向对象的思考方式 

###  PlantUML + Cursor 方法适用于哪些场景？

这套方法特别适合以下场景：

  * ** 新项目启动  ** ：从零开始设计数据模型时，可以快速构建并生成标准化 SQL 

  * ** 现有系统重构  ** ：通过反向工程工具（付费内容中提供）将现有数据库转为 PlantUML，再优化设计 

  * ** 多数据库支持  ** ：项目需要支持不同数据库系统，如 MySQL、PostgreSQL 等 

  * ** 团队协作  ** ：需要在团队间清晰沟通数据模型设计，并保持一致性 

对于特别复杂的遗留系统或高度专业化的数据库设计（如时序数据库、图数据库），可能需要结合专业工具使用。

##  从设计到实现的完整工作流

下面介绍使用 PlantUML 和 Cursor 从设计到实现的完整流程，让你快速上手这套高效工具。

![image-20250404下午53604615](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxrvuIXic2ZaBmOU6nibe3Aiawrgdiak5R6tHNEjmibSnTvLJarr6gH3MDHLA/640?wx_fmt=png&from=appmsg)

###  步骤一：编写 PlantUML 类图

首先，在 Cursor 编辑器中创建一个新文件，例如  ` database_schema.puml  ` ，下面是一个基础的样例。

    
    
    @startuml 简单电子商务数据模型  
    ' 定义实体  
    class Product {  
      -id: Integer <<PK>>  
      -name: String <<NN>>  
      -description: String  
      -price: BigDecimal <<NN>>  
      -stock: Integer <<default: 0>>  
      -categoryId: Integer <<FK>>  
    }  
      
    class Category {  
      -id: Integer <<PK>>  
      -name: String <<NN>>  
      -description: String  
    }  
      
    class Customer {  
      -id: Integer <<PK>>  
      -firstName: String <<NN>>  
      -lastName: String <<NN>>  
      -email: String <<NN, unique>>  
      -phone: String  
      -address: String  
    }  
      
    class Order {  
      -id: Integer <<PK>>  
      -customerId: Integer <<FK>>  
      -orderDate: Date <<NN>>  
      -status: String <<NN, default: 'pending'>>  
      -totalAmount: BigDecimal <<NN>>  
    }  
      
    class OrderItem {  
      -id: Integer <<PK>>  
      -orderId: Integer <<FK>>  
      -productId: Integer <<FK>>  
      -quantity: Integer <<NN, default: 1>>  
      -price: BigDecimal <<NN>>  
    }  
      
    ' 定义关系，使用精确的关系表示  
    Category "1" --o "n" Product : contains  
    Customer "1" --o "n" Order : places  
    Order "1" --* "n" OrderItem : includes  
    Product "1" --o "n" OrderItem : references  
    @enduml

![image-20250406下午102313136](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxKc3T20yXt0LKvUFy1lZ6rPQzBNy8YS9MYQwFCM4UN3M8ZXY2pAiabbw/640?wx_fmt=png&from=appmsg)

设计时注意：

  1. 类图模型中通常省略审计字段（如 createdAt、updatedAt 等），这些会在后续的 SQL 生成过程中自动添加 
  2. 使用精确的关系表示： 

     * ` --o  ` 表示聚合关系，如类别与产品的关系 

     * ` --*  ` 表示组合关系，如订单与订单项的关系（订单项不能独立于订单存在） 

  3. 清晰标记约束：  ` <<PK>> ` 、  ` <<FK>> ` 、  ` <<NN>> ` 等 

###  步骤二：使用 Cursor 转换为 SQL

在 Cursor 中，选择 PlantUML 代码后，可以使用提示命令让 AI 助手生成对应的 SQL DDL 语句。根据项目需求，可以选择不同的提示模板。

![image-20250404下午61236759](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxthIkicAiaeGRmtLoQ63b9l62FRiaE7KTLy6MoictqbW8JUKrwicZUxlafHw/640?wx_fmt=png&from=appmsg)

无论是采用 Ask 或者 Agent 模式（之前是 Chat/Composer 模式），模型采用 claude 3.7、cladue
3.5、gpt-4o、gemini-2.5-pro 都是可行的，生成的 SQL 的一致性很高。

支持 plantuml 附件的 ChatGPT 网页版本也可以很好的生成。

####  通用 SQL 生成模板

以下是一个通用模板，可根据实际需求调整参数：

    
    
    将以下 PlantUML 类图转换为 [MySQL/PostgreSQL/SQLite/SQL Server/Oracle/MongoDB] 的 SQL 建表语句，遵循以下规则：  
    1. 命名规范：将驼峰命名法转换为下划线命名法  
    2. 数据类型映射：将 Java/UML 类型映射到适当的 SQL 类型  
    3. 审计字段：为每个表添加标准审计字段（created_at, created_by, updated_at, updated_by, is_deleted）  
    4. 约束与索引：根据 UML 中的标记生成对应的约束（PK, NN, unique等）  
    5. 注释：为表和字段添加适当的注释  
    6. 默认值处理：将相应的字段转换为对应的 DEFAULT 语句  
    7. 存储引擎与字符集（可选）：  
        - [InnoDB/指定其他引擎]  
        - [utf8mb4/指定其他字符集]

> 💡  ** 使用技巧  ** ：直接复制此模板到 Cursor 中，根据项目需求修改方括号内的选项，然后选择 PlantUML 代码应用此转换指令。

####  生成结果示例

![image-20250404下午62203081](https://mmbiz.qpic.cn/mmbiz_png/tZhja1CIKficoMozV1sDLg2gBFichjdMrxfREj0OQMds9hfPSrzY8xUJ5tibSUicYpIY1NgO75WcPbnO6PPIeyLAkw/640?wx_fmt=png&from=appmsg)

至此，我们已经掌握了使用PlantUML设计数据库模型并通过Cursor转换为SQL的基础流程。这些方法可以有效提升数据库设计效率。

在实际企业项目中，我们还需要处理多数据库环境支持、复杂业务模型设计和团队协作等更高级需求。

** 完整版内容包含:  **

  * ✓ 全流程工作体系：从需求分析到数据库实现的完整流程指南 
  * ✓ 多数据库适配方案：支持MySQL、PostgreSQL、SQLite、SQL Server等 6 种专业映射方案 
  * ✓ 企业级业务模型：3套完整业务模型的PlantUML模板（用户权限、支付、B2B电商系统） 
  * ✓ 高效提示词库：6个针对不同场景和数据库的专业提示词模板 
  * ✓ 实用工具：包含SQL转PlantUML反向工程工具，实现遗留系统快速可视化 



个人观点，仅供参考









****



****





__









