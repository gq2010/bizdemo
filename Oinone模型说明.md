# Oinone模型之元数据详解
## 一、模型元数据

### 安装与更新

使用@Model.model来配置模型的不可变更编码。模型一旦安装，无法在对该模型编码值进行修改，之后的模型配置更新会依据该编码进行查找并更新；如果仍然修改该注解的配置值，则系统会将该模型识别为新模型，存储模型会创建新的数据库表，而原表将会rename为废弃表。

如果模型配置了@Base注解，表明在studio中该模型配置不可变更；如果字段配置了@Base注解，表明在studio中该字段配置不可变更。

### 注解配置

模型类必需使用@Model注解来标识当前类为模型类。

可以使用@Model.model、@Fun注解模型的模型编码（也表示命名空间），先取@Model.model注解值，若为空则取@Fun注解值，若皆为空则取全限定类名。

### 模型元信息

模型的priority，当展示模型定义列表时，使用priority配置来对模型进行排序。

模型的ordering，使用ordering属性来配置该模型的数据列表的默认排序。

模型元信息继承形式：

*   不继承（N）
*   同编码以子模型为准（C）
*   同编码以父模型为准（P）
*   父子需保持一致，子模型可缺省（P=C）

注意：模型上配置的索引和唯一索引不会继承，所以需要在子模型重新定义。数据表的表名、表备注和表编码最终以父模型配置为准；扩展继承父子模型字段编码一致时，数据表字段定义以父模型配置为准。

| 名称                   | 描述          | 抽象继承 | 同表继承 | 代理继承 | 多表继承 |
| :------------------- | :---------- | :--- | :--- | :--- | :--- |
| 基本信息                 |             |      |      |      |      |
| displayName          | 显示名称        | N    | N    | N    | N    |
| summary              | 描述摘要        | N    | N    | N    | N    |
| label                | 数据标题        | N    | N    | N    | N    |
| check                | 模型校验方法      | N    | N    | N    | N    |
| rule                 | 模型校验表达式     | N    | N    | N    | N    |
| 模型编码                 |             |      |      |      |      |
| model                | 模型编码        | N    | N    | N    | N    |
| 高级特性                 |             |      |      |      |      |
| name                 | 技术名称        | N    | N    | N    | N    |
| table                | 逻辑数据表名      | N    | P=C  | P=C  | N    |
| type                 | 模型类型        | N    | N    | N    | N    |
| chain                | 是否是链式模型     | N    | N    | N    | N    |
| index                | 索引          | N    | N    | N    | N    |
| unique               | 唯一索引        | N    | N    | N    | N    |
| managed              | 需要数据管理器     | N    | N    | N    | N    |
| priority             | 优先级，默认100   | N    | N    | N    | N    |
| ordering             | 模型查询数据排序    | N    | N    | N    | N    |
| relationship         | 是否是多对多关系模型  | N    | N    | N    | N    |
| inherited            | 多重继承        | N    | N    | N    | N    |
| unInheritedFields    | 不从父类继承的字段   | N    | N    | N    | N    |
| unInheritedFunctions | 不从父类继承的函数   | N    | N    | N    | N    |
| 高级特性-数据源             |             |      |      |      |      |
| dsKey                | 数据源         | N    | P=C  | P=C  | N    |
| 高级特性-持久化             |             |      |      |      |      |
| logicDelete          | 是否逻辑删除      | P    | P    | P    | N    |
| logicDeleteColumn    | 逻辑删除字段      | P    | P    | P    | N    |
| logicDeleteValue     | 逻辑删除状态值     | P    | P    | P    | N    |
| logicNotDeleteValue  | 非逻辑删除状态值    | P    | P    | P    | N    |
| underCamel           | 字段是否驼峰下划线映射 | P    | P    | P    | N    |
| capitalMode          | 字段是否大小写映射   | P    | P    | P    | N    |
| 高级特性-序列生成配置          |             |      |      |      |      |
| sequence             | 配置编码        | C    | C    | C    | N    |
| prefix               | 前缀          | C    | C    | C    | N    |
| suffix               | 后缀          | C    | C    | C    | N    |
| separator            | 分隔符         | C    | C    | C    | N    |
| size                 | 序列长度        | C    | C    | C    | N    |
| step                 | 序列步长        | C    | C    | C    | N    |
| initial              | 初始值         | C    | C    | C    | N    |
| format               | 序列格式化       | C    | C    | C    | N    |
| 高级特性-关联关系（或逻辑外键）     |             |      |      |      |      |
| unique               | 外键值是否唯一     | C    | C    | C    | N    |
| foreignKey           | 外键名称        | C    | C    | C    | N    |
| relationFields       | 关系字段列表      | C    | C    | C    | N    |
| references           | 关联模型        | C    | C    | C    | N    |
| referenceFields      | 关联字段列表      | C    | C    | C    | N    |
| limit                | 关系数量限制      | C    | C    | C    | N    |
| pageSize             | 查询每页个数      | C    | C    | C    | N    |
| domainSize           | 模型筛选可选项每页个数 | C    | C    | C    | N    |
| domain               | 模型筛选，前端可选项  | C    | C    | C    | N    |
| onUpdate             | 更新关联操作      | C    | C    | C    | N    |
| onDelete             | 删除关联操作      | C    | C    | C    | N    |
| 静态配置                 |             |      |      |      |      |
| Static               | 静态元数据模型     | N    | N    | N    | N    |

表4-1-6-1 模型元信息

字段定义继承形式

| 名称   | 描述   | 抽象继承 | 同表继承 | 代理继承 | 多表继承 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 字段定义 | 字段定义 | C    | C    | C    | C    |

表4-1-6-2 字段定义继承形式

### 模型约束

#### 主键约束

每个模型都可以配置自身的主键列表，也可以不配置主键。主键值不可缺省，可以索引到模型所对应数据表中唯一的一条记录。

#### 外键约束

模型与模型之间的关联关系可以配置外键约束来约束关联关系之间数据的变更行为。

#### 校验约束

模型可以配置校验函数对该模型的数据进行校验，存储数据时，校验数据是否合法合规。

## 二、字段元数据

模型字段描述的是实体的特征属性。模型与字段之间的关联关系由Model的model与Field的model进行关联。ModelField继承关系抽象类Relation。

使用@Field注解来描述模型的字段。如果未配置字段类型，系统会根据Java代码的字段声明类型来自动获取业务类型。建议配置displayName属性来描述字段在前端的显示名称。可以使用defaultValue配置字段的默认值。

### 元数据注解说明

# @Field（元数据配置）

## 基础配置

- **displayName**: 展示名
- **summary**: 摘要
- **defaultValue**: 默认值
- **serialize**: 序列化方式
- **multi**: 多值
- **Sequence** (暂不支持，2.1.9以后。编码相关可以看模型编码生成器一文)
  - **sequence**: 序列生成函数
    - 可选值:
      - SEQ——自增流水号（不连续）
      - ORDERLY——自增强有序流水号（连续）
      - DATE_SEQ——日期+自增流水号（不连续）
      - DATE_ORDERLY_SEQ——日期+强有序流水号（连续）
      - DATE——日期
      - UUID——随机32位字符串，包含数字和小写英文字母
  - **prefix**: 前缀
  - **suffix**: 后缀
  - **separator**: 分隔符
  - **size**: 长度
  - **step**: 步长（包含流水号有效）
  - **initial**: 起始值（包含流水号有效）
  - **format**: 格式化（包含日期有效）

- **field**: 字段编码，默认java名称
- **unique**: 唯一建
- **store**: 是否存储
- **index**: 索引
- **PrimaryKey**: 是否为主键
- **immutable**: 不可变更
- **priority**: 排序字段，默认规则
  - oione提供的父类中 ID 默认 5
  - oione提供的父类中其他从200起，步长10
  - 业务自定义字段：100起，步长1，按代码中字段顺序，先父子再子
- **required**: 是否必填（已有例子）
- **invisible**: 不可见（已有例子）

## Advanced

- **name**: 技术名称，默认java字段名
- **columnDefinition**: 数据库字段对应类型定义
- **copied**: 可拷贝
- **column**: 数据库字段
- **onlyColumn**: 不支持列格式化
- **sudo**: 免权限控制
- **insertStrategy**: 插入策略
- **batchStrategy**: 批量策略
- **updateStrategy**: 更新策略
- **whereStrategy**: 查询策略
- **whereCondition**: 默认查询条件
- **charset**: 字符集
- **collate**: 字符集规则

## 其他配置

- **compute**: 计算函数编码
- **Override**
- **requestSerialize**
- **translate**: 翻译
- **Version**: 乐观锁
- **track**: 字段追踪
- **Page**



# 字段类型

## 基础类型

### @Field.Binary, 对应类型 BINARY
- **min**: 最小值
- **max**: 最大值，默认值：65000
- **mime**: MIME类型，可选值见MimeTypeEnum
- **type**: 二进制类型，默认值BinaryTypeEnum.FILE

### @Field.Integer, 对应类型 INTEGER
- **M**: 默认值20
- **min**: 最小值，默认值：-Infinity
- **max**: 最大值，默认值：Infinity

### @Field.Float, 对应类型 FLOAT, decimal(M,D)
- **min**: 最小值，默认值：-Infinity
- **max**: 最大值，默认值：Infinity
- **M**: 默认值15
- **D**: 默认值6

### @Field.Boolean, 对应类型 BOOLEAN

### @Field.Enum, 对应类型 ENUM
- **dictionary**: 数据字段编码
- **size**: 长度限制，默认128
- **limit**: 数量限制

### @Field.String, 对应类型 STRING
- **min**: 最小值
- **max**: 最大值
- **size**: 长度限制，默认128

### @Field.Text, 对应类型 TEXT
- **min**: 最小值
- **max**: 最大值

### @Field.html, 对应类型 HTML
- **min**: 最小值
- **max**: 最大值

### @Field.Date
- **type**: 对应类型
  - DateTimeEnum.DATETIME（默认）
  - DateTimeEnum.YEAR
  - DateTimeEnum.DATE
  - DateTimeEnum.TIME
- **format**: 格式化方式，默认值DateFormatEnum.DATETIME
- **fraction**: 小数，默认值
- **min**: 最小值
- **max**: 最大值

## 复合类型

### @Field.Money, 对应类型 MONEY: decimal(M,D)
- **M**: 默认值65
- **D**: 默认值6
- **currency**: 货币
- **min**: 最小值，默认值：-Infinity
- **max**: 最大值，默认值：Infinity

## 引用类型

### @Field.Related
- **related**: @AliasFor("related")
- **value**: @AliasFor("value")

## 关系类型

### @Field.Relation
- **store**: 是否存储
- **relationFields**: 关系模型（自身模型）的关系字段（自身字段）
- **referenceFields**: 关联模型的关联字段
- **references**: 关联模型
- **referenceClass**: 关联模型类
- **domainSize**: 模型筛选结果数量限制
- **domain**: 模型筛选
- **filter**: 数据过滤
- **context**: 关联上下文
- **search**: 搜索函数编码

### @Field.many2one
- **limit**: 数量限制
- **pageSize**: 查询分页数量
- **ordering**: 排序
- **inverse**: 反转关联，关联关系存储在一对多关系的“一”这边

### @Field.one2many
- **onUpdate**
  - 默认值：OnCascadeEnum.SET_NULL，设置为空
  - 其他可选值：
    - SET_NULL，设置空值
    - CASCADE，级联操作
    - RESTRICT，限制操作
- **onDelete**
  - 默认值：OnCascadeEnum.SET_NULL，设置为空
  - 其他可选值：
    - SET_NULL，设置空值
    - CASCADE，级联操作
    - RESTRICT，限制操作

### @Field.many2many
- **through**: 中间模型
- **throughClass**: 中间模型类
- **relationFields**: 中间模型的关系模型的关系字段
- **referenceFields**: 中间模型的关联模型的关联字段
- **limit**: 数量限制
- **pageSize**: 查询分页数量
- **ordering**: 排序

### @Field.one2one



### 安装与更新

使用@Field.field来配置字段的不可变更编码。字段一旦安装，无法在对该字段编码值进行修改，之后的字段配置更新会依据该编码进行查找并更新；如果仍然修改该注解的配置值，则系统会将该字段识别为新字段，存储模型会创建新的数据库表字段，而原字段将会rename为废弃字段。

### 基础配置

#### 不可变更字段

使用immutable属性来描述该字段前后端都无法进行更新操作，系统会忽略不可变更字段的更新操作。

#### 自动生成编码的字段

可以使用@Field.Sequence注解在字段上配置编码生成规则，为编码为空的字段自动生成编码。
============
##### 一、编码生成器

可以在模型或者字段上配置编码自动生成规则。在进行数据存储时，如果配置了编码自动生成规则的字段值为空，则系统将根据规则自动生成编码。编码自动生成功能是通过序列生成器来支持的。可以在序列生成器生成的序列编码基础上再进行组合配置的功能编码生成最终的编码。序列生成器可以配置初始序列，步长，日期格式，长度。

1. 模型序列生成器（举例）

使用模型编码生成器，需要继承CodeModel或者有Code字段，那么使用Model.Code注解即可。

> Step1 为PetShop增加一个@Model.Code注解，并增加一个店铺编码(Code)字段

```java
package pro.shushi.pamirs.demo.api.model;

import pro.shushi.pamirs.meta.annotation.Field;
import pro.shushi.pamirs.meta.annotation.Model;

import java.sql.Time;

@Model.model(PetShop.MODEL_MODEL)
@Model(displayName = "宠物店铺",summary="宠物店铺",labelFields = {"shopName"})
@Model.Code(sequence = "DATE_ORDERLY_SEQ",prefix = "P",size=6,step=1,initial = 10000,format = "yyyyMMdd")
public class PetShop extends AbstractDemoIdModel {
    public static final String MODEL_MODEL="demo.PetShop";

    @Field(displayName = "店铺编码")
    private String code;

    @Field(displayName = "店铺名称",required = true)
    private String shopName;

    @Field(displayName = "开店时间",required = true)
    private Time openTime;

    @Field(displayName = "闭店时间",required = true)
    private Time closeTime;

}

```



2. 字段序列生成器

字段编码生成器，在对应的字段上增加，并使用Field.Sequence注解即可

> Step1 为PetShop增加一个字段codeTwo并增加@Field.Sequence注解

```java
package pro.shushi.pamirs.demo.api.model;

import pro.shushi.pamirs.meta.annotation.Field;
import pro.shushi.pamirs.meta.annotation.Model;

import java.sql.Time;

@Model.model(PetShop.MODEL_MODEL)
@Model(displayName = "宠物店铺",summary="宠物店铺",labelFields = {"shopName"})
@Model.Code(sequence = "DATE_ORDERLY_SEQ",prefix = "P",size=6,step=1,initial = 10000,format = "yyyyMMdd")
public class PetShop extends AbstractDemoIdModel {
    public static final String MODEL_MODEL="demo.PetShop";

    @Field(displayName = "店铺编码")
    private String code;

    @Field(displayName = "店铺编码2")
    @Field.Sequence(sequence = "DATE_ORDERLY_SEQ",prefix = "C",size=6,step=1,initial = 10000,format = "yyyyMMdd")
    private String codeTwo;

    @Field(displayName = "店铺名称",required = true)
    private String shopName;

    @Field(displayName = "开店时间",required = true)
    private Time openTime;

    @Field(displayName = "闭店时间",required = true)
    private Time closeTime;
}

```

##### 二、编码注解说明，模型更多其他注解详见4.1.6【模型之元数据详解】

- 模型编码注解说明

1.  模型编码生成器规定仅针对code属性生效
2.  Model.Code#sequence：序列生成函数

    *   SEQ——自增流水号（不连续）
    *   ORDERLY——自增强有序流水号（连续）
    *   DATE\_SEQ——日期+自增流水号（不连续）
    *   DATE\_ORDERLY\_SEQ——日期+强有序流水号（连续）
    *   DATE——日期
    *   UUID——随机32位字符串，包含数字和小写英文字母
3.  Model.Code#prefix：前缀
4.  Model.Code#suffix：后缀
5.  Model.Code#size：长度
6.  Model.Code#step：步长（包含流水号有效）
7.  Model.Code#initial：起始值（包含流水号有效）
8.  Model.Code#format：格式化（包含日期有效）
9.  Model.Code#separator：分隔符

- 字段编码注解说明

1.  字段编码生成器规定在字段上增加Field.Sequence注解即可
2.  Field.Sequence#sequence：序列生成函数

    *   SEQ——自增流水号（不连续）
    *   ORDERLY\_SEQ——自增强有序流水号（连续）
    *   DATE\_SEQ——日期+自增流水号（不连续）
    *   DATE\_ORDERLY\_SEQ——日期+强有序流水号（连续）
    *   DATE——日期
    *   UUID——随机32位字符串，包含数字和小写英文字母
3.  Field.Sequence#prefix：前缀
4.  Field.Sequence#suffix：后缀
5.  Field.Sequence#size：长度
6.  Field.Sequence#step：步长（包含流水号有效）
7.  Field.Sequence#initial：起始值（包含流水号有效）
8.  Field.Sequence#format：格式化（包含日期有效）
9.  Field.Sequence#separator：分隔符

========



#### 字段的序列化与反序列化

使用@Field注解的serialize属性来配置非字符串类型属性的序列化与反序列化方式，最终会以序列化后的字符串持久化到存储中。

> 
============
> 一、数据存储的序列化 (举例)

使用@Field注解的serialize属性来配置非字符串类型属性的序列化与反序列化方式，最终会以序列化后的字符串持久化到存储中。 ### Step1 新建PetItemDetail模型、并为PetItem添加两个字段

1.  PetItemDetail继承TransientModel，增加两个字段，分别为备注和备注人

```java
package pro.shushi.pamirs.demo.api.tmodel;

import pro.shushi.pamirs.meta.annotation.Field;
import pro.shushi.pamirs.meta.annotation.Model;
import pro.shushi.pamirs.meta.base.TransientModel;
import pro.shushi.pamirs.user.api.model.PamirsUser;

@Model.model(PetItemDetail.MODEL_MODEL)
@Model(displayName = "商品详情",summary = "商品详情",labelFields = {"remark"})
public class PetItemDetail extends TransientModel {
    public static final String MODEL_MODEL="demo.PetItemDetail";

    @Field.String(min = "2",max = "20")
    @Field(displayName = "备注",required = true)
    private String remark;

    @Field(displayName = "备注人",required = true)
    private PamirsUser user;

}
```


1.  修改PetItem，增加两个字段petItemDetails类型为List和tags类型为List，并设置为不同的序列化方式，petItemDetails为JSON（缺省就是JSON，可不配），tags为COMMA。同时设置 @Field.Advanced(columnDefinition = varchar(1024))，防止序列化后存储过长

```java
package pro.shushi.pamirs.demo.api.model;

import pro.shushi.pamirs.demo.api.tmodel.PetItemDetail;
import pro.shushi.pamirs.meta.annotation.Field;
import pro.shushi.pamirs.meta.annotation.Model;
import pro.shushi.pamirs.meta.enmu.NullableBoolEnum;

import java.math.BigDecimal;
import java.util.List;

@Model.model(PetItem.MODEL_MODEL)
@Model(displayName = "宠物商品",summary="宠物商品",labelFields = {"itemName"})
public class PetItem  extends AbstractDemoCodeModel{

    public static final String MODEL_MODEL="demo.PetItem";

    @Field(displayName = "商品名称",required = true)
    private String itemName;

    @Field(displayName = "商品价格",required = true)
    private BigDecimal price;

    @Field(displayName = "店铺",required = true)
    @Field.Relation(relationFields = {"shopId"},referenceFields = {"id"})
    private PetShop shop;

    @Field(displayName = "店铺Id",invisible = true)
    private Long shopId;

    @Field(displayName = "品种")
    @Field.many2one
    @Field.Relation(relationFields = {"typeId"},referenceFields = {"id"})
    private PetType type;

    @Field(displayName = "品种类型",invisible = true)
    private Long typeId;

    @Field(displayName = "详情", serialize = Field.serialize.JSON, store = NullableBoolEnum.TRUE)
    @Field.Advanced(columnDefinition = "varchar(1024)")
    private List<PetItemDetail> petItemDetails;

    @Field(displayName = "商品标签",serialize = Field.serialize.COMMA,store = NullableBoolEnum.TRUE,multi = true)
    @Field.Advanced(columnDefinition = "varchar(1024)")
    private List<String> tags;

}
```


> Step3 字段序列化注意点

1.  必须使用Field#store属性将字段存储设置为NullableBoolEnum.TRUE。
2.  使用Field#serialize属性指定序列化方式，默认为JSON。
3.  如把PetItemDetail设置为存储模型，须在PetItem的petItemDetails字段上使用Field.Relation#store属性将关联关系存储设置为false。不然会同时存储petItemDetails字段和对应的PetItemDetail表记录

> 字段序列化方式说明

| 序列化方式 | 说明         | 备注                                                                                          |
| :---- | :--------- | :------------------------------------------------------------------------------------------ |
| JSON  | JSON序列化    | 主要用于模型相关类型字段的序列化，是@Field.serialize默认选项                                                      |
| DOT   | 点拼接集合元素    |                                                                                             |
| COMMA | 逗号拼接集合元素   |                                                                                             |
| BIT   | 按位与，2次幂数求和 | 非@Field.serialize可选项列表，用于[二进制枚举](https://doc.oinone.top/oio4/9237.html)序列化不需要配置，由oinone自动推断 |

表3-3-7-1 字段序列化方式说明

> 二、注册自己的序列化器（举例）

注册自己的序列化器（实现pro.shushi.pamirs.meta.api.core.orm.serialize.Serializer接口）， 如oinone的DOT的序列化方式，用type()方法返回值做匹配，serialize和deserialize分别对应序列化和反序列化方法。

    package pro.shushi.pamirs.framework.compute.serialize;

    import org.apache.commons.lang3.StringUtils;
    import org.springframework.stereotype.Component;
    import pro.shushi.pamirs.meta.annotation.fun.extern.Slf4j;
    import pro.shushi.pamirs.meta.api.core.orm.serialize.Serializer;
    import pro.shushi.pamirs.meta.common.constants.CharacterConstants;
    import pro.shushi.pamirs.meta.enmu.SerializeEnum;
    import pro.shushi.pamirs.meta.util.TypeUtils;

    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.List;

    /**
     * 点表达式序列生成处理器实现
     *
     * @author d@shushi.pro
     * @version 1.0.0
     * date 2020/3/4 2:48 上午
     */
    @SuppressWarnings("rawtypes")
    @Slf4j
    @Component
    public class DotSerializeProcessor implements Serializer<Object, String> {

        @Override
        public String serialize(String ltype, Object value) {
            if (null == value) {
                return null;
            }
            if (List.class.isAssignableFrom(value.getClass())) {
                return StringUtils.join((List) value, CharacterConstants.SEPARATOR_DOT);
            } else {
                return StringUtils.join(Collections.singletonList(value), CharacterConstants.SEPARATOR_DOT);
            }
        }

        @SuppressWarnings("unchecked")
        @Override
        public Object deserialize(String ltype, String ltypeT, String value, String format) {
            if (null == value) {
                return null;
            }
            String[] dots = value.split(CharacterConstants.SEPARATOR_ESCAPE_DOT);
            List list = new ArrayList();
            for (String dot : dots) {
                Object object = TypeUtils.valueOfPrimary(ltypeT, dot, null);
                list.add(object);
            }
            return list;
        }

        @Override
        public String type() {
            return SerializeEnum.DOT.value();
        }
    }



> 字段默认值的反序列化

用@Field.defaultValue注解在字段上配置defaultValue属性时，将根据字段的Ttype类型及字段的Ltype等类型属性，自动进行反序列化。包括但不限于以下几种情况：

*   OBJ、STRING、TEXT、HTML——保持不变
*   BINARY、INTEGER——转换为整数
*   FLOAT、MONEY——转换为浮点数
*   DATETIME、DATE、TIME、YEAR——根据Field.Date#format属性决定反序列化日期格式
*   BOOLEAN——仅允许null、true、false
*   ENUM——使用value进行匹配


============

#### 前端默认配置

可以使用@Field注解中的以下属性来配置前端的默认视觉与交互规则，也可以在前端设置覆盖以下配置。

*   required，是否必填
*   invisible，是否不可见
*   priority，字段优先级，列表的列使用该属性进行排序

### 字段类型

类型系统由基本类型、复合（组件）类型、引用类型和关系类型四种类型系统构成。通过类型系统来决定应用程序、数据库和前端视觉视图是如何进行交互，数据及数据间关系如何处理的。

#### 基本类型

表4-1-6-3 基本类型

#### 复合类型

| 业务类型     | Java类型                                | 数据库类型                                  | 规则说明                                                                                                                                                                                                                                                          |             |
| :------- | :------------------------------------ | :------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------- |
| BINARY   | Byte Byte\[]                          | TINYINT BLOB                           | 二进制类型，不推荐使用                                                                                                                                                                                                                                                   |             |
| INTEGER  | INTEGER Short Integer Long BigInteger | smallint int bigint decimal(size,0)    | 整数, 包括整数（10-11位有效数字）、长整数（19-20位有效数字）和大整数（超过19位）。 【数据库规则】：默认使用int；如果size小于6则使用smallint；如果size超过6则使用int；如果size超过10位数字，即大于11（包含符号位），则使用长整数bigint；如果size超过19位数字，即大于20（包含符号位），则使用大数decimal。若未配置size，则按Java类型推测。 【前端交互规则】：整数使用Number类型，长整数和大整数前后端协议使用字符串类型。         | 二进制类型，不推荐使用 |
| FLOAT    | Float Double BigDecimal               | float(M,D) double(M,D) decimal(M,D)    | 浮点数, 包括单精度浮点数（7-8位有效数字）、双精度浮点数（15-16位有效数字）和大数（超过15位）。 【数据库规则】：默认使用单精度浮点数float； 如果size超过7位数字，即大于等于8，则使用双精度浮点数double；如果size超过15位数字，即大于等于16，则使用大数decimal。若未配置size，则按Java类型推测。 【前端交互规则】：单精度浮点数float和双精度浮点数double使用Number类型（因为都使用IEEE754协议64位进行存储），大数前后端协议使用字符串类型。 |             |
| BOOLEAN  | Boolean                               | tinyint(1)                             | 布尔类型，值为1,true(真)或0,false(假)                                                                                                                                                                                                                                   |             |
| ENUM     | Enum                                  | varchar(size)                          | 【前端交互规则】：可选项从ModelField的options字段获取，options字段值为字段指定数据字典子集的JSON序列化字符串。前后端传递的是可选项的name，数据库存储使用可选项的value。multi属性为true，则使用多选控件；multi属性为false，则使用单元控件                                                                                                              |             |
| STRING   | String                                | varchar(size)                          | 字符串，size为长度限制默认值参考，前端可以view中覆盖该配置                                                                                                                                                                                                                             |             |
| TEXT     | String                                | text                                   | 多行文本，编辑态组件为多行文本框，长度限制为配置项size值                                                                                                                                                                                                                                |             |
| HTML     | String                                | text                                   | 富文本编辑器                                                                                                                                                                                                                                                        |             |
| DATETIME | java.util.Date java.sql.Timestamp     | datetime(fraction) timestamp(fraction) | 日期时间类型 【数据库规则】：日期和时间的组合， 时间格式为 YYYY-MM-DD HH\:MM\:SS\[.fraction]，默认精确到秒，在默认的秒精确度上，可以带小数，最多带6位小数，即可以精确到 microseconds (6 digits) precision。可以通过设置fraction来设置精确小数位数，最终存储在字段的decimal属性上。 【前端交互规则】：前端默认使用日期时间控件，根据日期时间类型格式化格式format格式化日期时间                         |             |
| YEAR     | java.util.Date                        | year                                   | 日期时间类型 年份类型 日期类型 【数据库规则】：默认“YYYY”格式表示的日期值 【前端交互规则】：前端默认使用年份控件，根据日期类型格式化格式format格式化日期                                                                                                                                                                          |             |
| DATE     | java.util.Date java.sql.Date          | date date                              | date date 日期类型 【数据库规则】：默认“YYYY-MM-DD”格式表示的日期值 【前端交互规则】：前端默认使用日期控件，根据日期类型格式化格式format格式化日期                                                                                                                                                                      |             |
| TIME     | java.util.Date java.sql.Time          | time(fraction) time(fraction)          | time(fraction) time(fraction) 时间类型 【数据库规则】：默认“HH\:MM\:SS”格式表示的时间值 【前端交互规则】：前端默认使用时间控件，根据日期类型格式化格式format格式化日期                                                                                                                                                  |             |

| 业务类型     | Java类型                           | 数据库类型                                 | 规则说明                                                                                                                                                                                                                                                       |
| :------- | :------------------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BINARY   | ByteByte\[]                      | TINYINTBLOB                           | 二进制类型，不推荐使用                                                                                                                                                                                                                                                |
| INTEGER  | ShortIntegerLongBigInteger       | smallintintbigintdecimal(size,0)      | 整数, 包括整数（10-11位有效数字）、长整数（19-20位有效数字）和大整数（超过19位）。【数据库规则】：默认使用int；如果size小于6则使用smallint；如果size超过6则使用int；如果size超过10位数字，即大于11（包含符号位），则使用长整数bigint；如果size超过19位数字，即大于20（包含符号位），则使用大数decimal。若未配置size，则按Java类型推测。【前端交互规则】：整数使用Number类型，长整数和大整数前后端协议使用字符串类型。        |
| FLOAT    | FloatDoubleBigDecimal            | float(M,D)double(M,D)decimal(M,D)     | 浮点数,?包括单精度浮点数（7-8位有效数字）、双精度浮点数（15-16位有效数字）和大数（超过15位）。【数据库规则】：默认使用单精度浮点数float；如果size超过7位数字，即大于等于8，则使用双精度浮点数double；如果size超过15位数字，即大于等于16，则使用大数decimal。若未配置size，则按Java类型推测。【前端交互规则】：单精度浮点数float和双精度浮点数double使用Number类型（因为都使用IEEE754协议64位进行存储），大数前后端协议使用字符串类型。 |
| BOOLEAN  | Boolean                          | tinyint(1)                            | 布尔类型，值为1,true(真)或0,false(假)                                                                                                                                                                                                                                |
| ENUM     | Enum                             | 与数据字典指定基本类型一致                         | 【前端交互规则】：可选项从ModelField的options字段获取，options字段值为字段指定数据字典子集的JSON序列化字符串。前后端传递的是可选项的name，数据库存储使用可选项的value。multi属性为true，则使用多选控件；multi属性为false，则使用单元控件                                                                                                           |
| STRING   | String                           | varchar(size)                         | 字符串，size为长度限制默认值参考，前端可以view中覆盖该配置                                                                                                                                                                                                                          |
| TEXT     | String                           | text                                  | 多行文本，编辑态组件为多行文本框，长度限制为配置项size值                                                                                                                                                                                                                             |
| HTML     | String                           | text                                  | 富文本编辑器                                                                                                                                                                                                                                                     |
| DATETIME | java.util.Datejava.sql.Timestamp | datetime(fraction)timestamp(fraction) | 日期时间类型【数据库规则】：日期和时间的组合，时间格式为?YYYY-MM-DD HH\:MM\:SS\[.fraction]，默认精确到秒，在默认的秒精确度上，可以带小数，最多带6位小数，即可以精确到?microseconds (6 digits) precision。可以通过设置fraction来设置精确小数位数，最终存储在字段的decimal属性上。【前端交互规则】：前端默认使用日期时间控件，根据日期时间类型格式化格式format格式化日期时间                         |
| YEAR     | java.util.Date                   | year                                  | 年份类型日期类型【数据库规则】：默认“YYYY”格式表示的日期值【前端交互规则】：前端默认使用年份控件，根据日期类型格式化格式format格式化日期                                                                                                                                                                                 |
| DATE     | java.util.Datejava.sql.Date      | datedate                              | 日期类型【数据库规则】：默认“YYYY-MM-DD”格式表示的日期值【前端交互规则】：前端默认使用日期控件，根据日期类型格式化格式format格式化日期                                                                                                                                                                               |
| TIME     | java.util.Datejava.sql.Time      | time(fraction)time(fraction)          | 时间类型【数据库规则】：默认“HH\:MM\:SS”格式表示的时间值【前端交互规则】：前端默认使用时间控件，根据日期类型格式化格式format格式化日期                                                                                                                                                                               |

表4-1-6-3 基本类型

#### 复合类型

| 业务类型  | Java类型     | 数据库类型        | 规则说明                           |
| :---- | :--------- | :----------- | :----------------------------- |
| MONEY | BigDecimal | decimal(M,D) | 金额，前端使用金额控件，可以使用currency设置币种字段 |

表4-1-6-4 复合类型

#### 引用类型

| 业务类型    | Java类型    | 数据库类型            | 规则说明                                                                                   |
| :------ | :-------- | :--------------- | :------------------------------------------------------------------------------------- |
| RELATED | 基本类型或关系类型 | 不存储或varchar、text | 引用字段【数据库规则】：点表达式最后一级对应的字段类型；数据库字段值默认为Java字段的序列化值，默认使用JSON序列化【前端交互规则】：点表达式最后一级对应的字段控件类型 |

表4-1-6-5 引用类型

#### 关系类型

| 业务类型 | Java类型           | 数据库类型            | 规则说明  |
| :--- | :--------------- | :--------------- | :---- |
| O2O  | 模型/DataMap       | 不存储或varchar、text | 一对一关系 |
| M2O  | 模型/DataMap       | 不存储或varchar、text | 多对一关系 |
| O2M  | List<模型/DataMap> | 不存储或varchar、text | 一对多关系 |
| M2M  | List<模型/DataMap> | 不存储或varchar、text | 多对多关系 |

表4-1-6-6 关系类型

多值字段或者关系字段需要存储，默认使用JSON格式序列化。多值字段数据库字段类型默认为varchar(1024)；关系字段数据库字段类型默认为text。

#### 类型默认推断

M代表精度，即有效长度（总位数）， D代表标度，即小数点后的位数，fraction为时间秒以下精度。multi表示该字段为多值字段。

| Java类型               | Field注解                             | 推断ttype  | 推断配置                 | 推断数据库配置       |
| :------------------- | :---------------------------------- | :------- | :------------------- | :------------ |
| Byte                 | @Field                              | BINARY   | 无                    | blob          |
| String               | @Field                              | STRING   | size=128             | varchar(128)  |
| List                 | @Field                              | STRING   | size=1024,multi=true | varchar(1024) |
| Map                  | @Field                              | STRING   | size=1024            | varchar(1024) |
| Short                | @Field                              | INTEGER  | M=5                  | smallint(6)   |
| Integer              | @Field                              | INTEGER  | M=10                 | integer(11)   |
| Long                 | @Field                              | INTEGER  | M=19                 | bigint(20)    |
| BigInteger           | @Field                              | INTEGER  | M=64                 | decimal(64,0) |
| Float                | @Field                              | FLOAT    | M=7,D=2              | float(7,2)    |
| Double               | @Field                              | FLOAT    | M=15,D=4             | double(15, 4) |
| BigDecimal           | @Field                              | FLOAT    | M=64,D=6             | decimal(64,6) |
| Boolean              | @Field                              | BOOLEAN  | 无                    | tinyint(1)    |
| java.util.Date       | @Field                              | DATETIME | fraction=0           | datetime      |
| java.util.Date       | @Field.Date(type=DateTypeEnum.YEAR) | YEAR     | 无                    | year          |
| java.util.Date       | @Field.Date(type=DateTypeEnum.DATE) | DATE     | 无                    | date          |
| java.util.Date       | @Field.Date(type=DateTypeEnum.TIME) | TIME     | fraction=0           | time          |
| java.sql.Timestamp   | @Field                              | DATETIME | fraction=0           | timestamp     |
| java.sql.Date        | @Field                              | DATE     | 无                    | date          |
| java.sql.Time        | @Field                              | TIME     | fraction=0           | time          |
| Long                 | @Field.Date                         | DATETIME | fraction=0           | datetime      |
| enum implementsIEnum | @Field                              | ENUM     | 无                    | 根据枚举value类型   |
| primitive type       | @Field.Enum(dictionary=数据字典编码)      | ENUM     | 无                    | 根据枚举value类型   |
| List                 | @Field.Enum(dictionary=数据字典编码)      | ENUM     | multi=true           | varchar(512)  |
| 模型类                  | @Field.Relation                     | M2O      | 无                    | text          |
| DataMap              | @Field.Relation                     | M2O      | 无                    | text          |
| List<模型类>            | @Field.Relation                     | O2M      | multi=true           | text          |
| List                 | @Field.Relation                     | O2M      | multi=true           | text          |

表4-1-6-7 类型默认推断

### 字段约束

#### 主键

可以使用Yaml或者@Model.Advanced的keyGenerator属性来配置模型主键的自动生成规则，AUTO\_INCREMENT或者分布式ID。如果不配置，将不会自动生成主键值。

#### 逻辑外键约束

在创建关联关系字段的时候，可以使用@Field.Relation注解的onUpdate和onDelete属性指定在删除模型或更新模型关系字段值时，对关联模型进行的相应操作。操作包括RESTRICT、NO ACTION、SET NULL和CASCADE，默认值为RESTRICT。

- RESTRICT是指模型与关联模型有关联记录的情况下，引擎会阻止模型关系字段的更新或删除模型记录；\
- NO ACTION是指不作约束（这里与数据库约束的定义不相同）；\
- CASCADE表示在更新模型关系字段或者删除模型时，级联更新关联模型对应记录的关联字段值或者级联删除关联模型对应记录；\
- SET NULL则是表示在更新模型关系字段或者删除模型的时候，关联模型的对应关联字段将被SET NULL（该字段值允许为null的情况下，若不允许为null，则引擎阻止对模型的操作）。

#### 通用校验约束

| 字段业务类型  | size  | limit  | decimal | mime | min | max |
| :------ | :---- | :----- | :------ | :--- | :-- | :-- |
| BINARY  | 文件类型  | 最小比特位  | 最大比特位   |      |     |     |
| INTEGER | 有效数字  | 最小值    | 最大值     |      |     |     |
| FLOAT   | 有效数字  | 小数位数   | 最小值     | 最大值  |     |     |
| BOOLEAN |       |        |         |      |     |     |
| ENUM    | 存储字符数 | 多选最多数量 |         |      |     |     |
| STRING  | 存储字符数 | 字符数    | 字符数     |      |     |     |
| TEXT    | 字符数   | 字符数    |         |      |     |     |
| HTML    | 字符数   | 字符数    |         |      |     |     |
| MONEY   | 有效数字  | 小数位数   | 最小值     | 最大值  |     |     |
| RELATED |       |        |         |      |     |     |

表4-1-6-8 通用校验约束（表一）

| 字段业务类型   | fraction | format | min    | max    |
| :------- | :------- | :----- | :----- | :----- |
| DATETIME | 时间精度     | 时间格式   | 最早日期时间 | 最晚日期时间 |
| YEAR     | 时间格式     | 最早年份   | 最晚年份   |        |
| DATE     | 时间格式     | 最早日期   | 最晚日期   |        |
| TIME     | 时间精度     | 时间格式   | 最早时间   | 最晚时间   |

表4-1-6-9 通用校验约束（表二）

| 字段业务类型  | size          | domainSize | limit  | pageSize |
| :------ | :------------ | :--------- | :----- | :------- |
| RELATED | 存储字符数(若序列化存储) |            |        |          |
| O2O     | 存储字符数(若序列化存储) | 可选项每页个数    |        |          |
| M2O     | 存储字符数(若序列化存储) | 可选项每页个数    |        |          |
| O2M     | 存储字符数(若序列化存储) | 可选项每页个数    | 关系数量限制 | 查询每页个数   |
| M2M     | 存储字符数(若序列化存储) | 可选项每页个数    | 关系数量限制 | 查询每页个数   |

表4-1-6-10 通用校验约束（表三）

在模型或字段上配置check函数，则处理前端请求时会进行校验约束。也可以调用模型上的check函数进行编程式校验。

#### 默认值约束

字段默认值defaultValue可以是基本类型或者关系类型的序列化值。时间类型可以使用format来格式化时间表达式或者使用长整数来设置默认值。枚举类型使用枚举项值value来设置默认值。如果需要进行复杂的计算请使用模型的construct构造函数来配置解决。

#### 唯一约束

将字段或者模型上配置unique唯一索引，可以为模型或字段添加唯一约束。

#### 可选项约束

使用枚举定义字段的可选项值，可以为字段提供可选项约束功能。

### 关系字段

关联关系用于描述模型间的关联方式：

- 多对一关系，主要用于明确从属关系\
- 一对多关系，主要用于明确从属关系\
- 多对多关系，主要用于弱依赖关系的处理，提供中间模型进行关联关系的操作\
- 一对一关系，主要用于多表继承和行内合并数据

---

#### 一、图例说明（左上角）
- **紫色箭头（←→）**：表示“多对多”（M2M）关系。
- **黄色箭头（→）**：表示“一对一”（O2O）关系。
- **蓝色箭头（→）**：表示“多对一”（M2O）关系。
- **红色箭头（→）**：表示“一对多”（O2M）关系。

---

#### 二、中心结构解析

图的中心是一个名为“**存储模型**”的节点，它与其他多个“存储模型”通过不同的关系连接，体现了数据库中模型间的复杂关联。

##### 1. 多对多关系（M2M）
- 中心“存储模型”与右侧另一个“存储模型”之间是**多对多**关系（紫色线）。
- 该关系通过一个**中间表（中间模型）** 实现。
- 中间表有两个字段：
  - 红色 `rel fields`：指向其中一个模型的字段，对应 `throughRelationFields`。
  - 蓝色 `rel fields`：指向另一个模型的字段，对应 `throughReferenceFields`。
- 这表示在多对多关系中，通常需要一个中间表来存储两个实体之间的映射，而 `rel fields` 指明了哪个字段用于关联。

##### 2. 一对一关系（O2O）
- 中心“存储模型”向上连接到另一个“存储模型”，用**黄色箭头**表示“一对一”关系。
- 连接线上标注为 O2O，表示从中心模型到上方模型是一对一。
- 在中心模型中有一个 `rel fields` 字段，用于建立此关系。

##### 3. 多对一关系（M2O）
- 中心“存储模型”向左下连接到一个“存储模型”，用**蓝色箭头**表示“多对一”。
- 标注为 M2O，意味着多个中心模型可以对应一个目标模型。
- 中心模型中存在 `rel fields` 字段，用于指向目标模型。

##### 4. 一对多关系（O2M）
- 中心“存储模型”向右下连接到一个“存储模型”，用**红色箭头**表示“一对多”。
- 标注为 O2M，表示一个中心模型可以对应多个目标模型。
- 目标模型中包含 `rel fields` 字段，用于反向引用中心模型。

---

#### 三、底部文字说明
> **rel fields 表示的是存储关联关系的字段所在模型**
>
> **多对多关系的红字 rel fields 为 throughRelationFields，蓝字 rel fields 为 throughReferenceFields**

- 解释了 `rel fields` 的含义：它是用来定义模型之间关系的字段。
- 在多对多关系中：
  - **红色 `rel fields`**：表示在中间表中，用于指向某个主模型的字段，即 `throughRelationFields`。
  - **蓝色 `rel fields`**：表示在中间表中，用于指向另一个主模型的字段，即 `throughReferenceFields`。

---

#### 四、总结

这张图清晰地展示了：

1. **四种基本数据库关系类型**（一对一、一对多、多对一、多对多）。
2. **每种关系的连接方向和符号表示**。
3. **多对多关系需要中间表**，并通过两个字段（`throughRelationFields` 和 `throughReferenceFields`）分别关联两个实体。
4. **`rel fields` 是关键字段**，用于在模型中建立关系，其位置和颜色区分了不同类型的关联字段。



#### 名词解释

关联关系比较重要的名词解释如下：

- 关联关系：使用relation表示，模型间的关联方式的一种描述，包括关联关系类型、关联关系双边的模型和关联关系的读写\
- 关联关系字段：业务类型ttype为O2O、O2M、M2O或M2M的字段\
- 关联模型：使用references表示，自身模型关联的模型\
- 关联字段：使用referenceFields表示，关联模型的字段，表示关联模型的哪些字段与自身模型的哪些字段建立关系\
- 关系模型：自身模型\
- 关系字段：使用relationFields表示，自身模型的字段，表示自身模型的哪些字段与关联模型的哪些字段建立关系\
- 中间模型，使用through表示，只有多对多存在中间模型，模型的relationship=true

#### 关联关系的默认视图

- 一对多默认视图，编辑态在行内是下拉多选，在详情是选项卡表格；展示态在行内是折叠面板表格，在详情是选项卡表格\
- 多对一默认视图，编辑态在行内是下拉单选，在详情是下拉单选；展示态在行内是文字，在详情是文字\
- 多对多默认视图，编辑态在行内是下拉多选，在详情是选项卡表格；展示态在行内是折叠面板表格，在详情是选项卡表格\
- 一对一默认视图，编辑态在行内是平铺，在详情是分组；展示态在行内是平铺，在详情是分组

在后端研发的使用上所有关联关系和引用的处理都限制在本模型，即平台至多处理到当前模型的字段，不再继续依据关联关系和引用处理关联模型。但是可以手动调用模型上的链式方法fieldQuery、fieldCreate和fieldUpdate来完成关联关系的查询与更新操作。

使用O2M或者M2M关联关系关联的临时模型没有分页查询操作。

#### 关联关系的配置

可以使用@Field.Relation注解的relationFields、referenceFields、references和through来配置关联关系。

relationFields与referenceFields为存储关联关系的一一映射字段列表。

如果relationFields缺省，一对多或者多对多关系的relationFields默认为模型主键；一对一或者多对一关系的relationFields默认为关联关系字段名加上首字母大写的主键名拼接而成的字符串。如果有多个主键，则relationFields和referenceFields也对应有多个字段。

如果配置了relationFields，但referenceFields缺省，则referenceFields与relationFields字段名一致。

一对多关系的referenceFields必填。如果referenceFields缺省，多对多，多对一或者一对一关系的referenceFields默认为主键。

| 关系类型 | 缺省关系字段默认值          | 缺省关联字段默认值                                                    |
| :--- | :----------------- | :----------------------------------------------------------- |
| 一对多  | 默认为关系模型的pk         | 默认为关系模型名+关系模型的pk；如果关系另一端的多对一字段名不是关系模型名，则需明确指定，使两端关系字段与关联字段对应 |
| 一对一  | 默认为关联关系字段名+关系模型的pk | 默认为关联模型的pk                                                   |
| 多对一  | 默认为关联关系字段名+关系模型的pk | 默认为关联模型的pk                                                   |
| 多对多  | 默认为关系模型的pk         | 默认为关联模型的pk                                                   |

表4-1-6-11 关联关系的配置

多对多使用through来指定中间模型的模型编码，如果指定模型编码的中间模型不存在，系统会根据through自动生成中间模型，中间模型的默认字段为与两端模型关联的关系字段。与关系模型关联的关系字段名称为关系模型名称加上关系模型的主键拼接而成的字符串；与关联模型关联的多对一字段名称为关联模型名称加上关联模型主键拼接而成的字段串。如果与关系模型关联的关系字段名称和与关联模型关联的多对一字段名称冲突，需要使用throughRelationFields和throughReferenceFields明确配置指定字段名称解决冲突。

系统根据模块的依赖关系，自动生成的中间模型将生成在先加载的建立多对多关系的关系模型所在模块。

#### 读写关联关系字段

默认关联关系字段的store属性为false，relationStore为true。若设置关联关系字段relationStore属性为true，则会为关联关系字段生成关系字段用于存储关联关系。若设置关联关系字段store属性为true，则存储时序列化字段值存储到数据库中，查询时从数据库中反序列化得到字段值。字段类型为varchar且长度为128，如果需要改变字段长度，可以使用@Field.Advanced的columnDefinition设置。当store属性为false时，则字段值为关联关系查询得到的结果。如果store为false且relationStore为false，则只能对字段进行赋值来设置字段值。

#### 关联操作

调用数据管理器的API不会触发关联操作，需要调用fieldQuery和fieldSave方法进行关联模型的关联操作。

前端的查询接口会根据GraphQL协议进行关联查询。

前端的新增和更新接口默认会存储当前模型的关联关系字段和递归新增和更新一对多关系的关联关系字段。更新接口会检查当前模型的逻辑外键约束。可以调用模型的ignore方法或设置模型数据的ignore属性来改变递归深度，避免循环操作。

前端的删除接口会默认删除当前模型数据和根据级联配置进行当前模型的关联关系字段的关联操作。删除接口会检查当前模型的逻辑外键约束。可以调用模型的ignore方法或设置模型数据的ignore属性来改变递归深度，避免循环操作。

#### 关联数据分页

可以使用关系字段配置中分页数量pageSize来限定关联查询的返回结果数量。可选项可以使用domainSize来限定可选项返回结果数量，由前端从字段元数据中获取并设置为可选项查询分页数量限制。

#### 反转关系

一对多关联关系可以设置inverse为true反转关系，反转关系后关联关系存储在一对多关系中“一”这一端。

#### 引用字段

引用字段可以通过与其他字段建立引用关系来获取数据。

当引用字段的store属性为true时，则字段值为存储的字段值，数据存储时将被引用字段值存储到数据存储中（unset掉被引用字段，则直接存储引用字段值）；当store属性为false时，则数据为被引用字段的字段值且不会存储。
