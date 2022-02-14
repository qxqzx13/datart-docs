---
title: 数据图表
---

数据图表是 datart 可视化的基础单元；通过对数据视图中的字段做可视化属性配置，将查询结果进行可视化编码，最终以图表的形式展现

数据图表可以在可视化功能的目录树中创建，也可以在仪表板中直接创建。在目录树中创建的数据图表称作`公共数据图表`，可以独立展示、也可以被多个仪表板引用，与仪表板共同显示在目录树中；在仪表板中直接创建的数据图表称为`专有数据图表`，仅能与所属仪表板一起展示

在主导航栏点击`可视化`菜单，点击`目录`顶部的加号按钮创建公共数据图表

![概述-1](/datart-docs/images/datachart/0-1-1.png)

填写名称、描述、选择所属目录，点击保存之后，一个空数据图表已完成创建

![概述-2](/datart-docs/images/datachart/0-1-2.png)

点击目录上新建的数据图表，右侧区域会显示它的浏览界面，点击右上角的编辑按钮进入图表编辑器

![概述-3](/datart-docs/images/datachart/0-1-3.png)

## 1. 编辑图表

编辑器从布局上分为3部分：
- 左侧：关联数据视图的字段列表，用于拖拽到配置区`数据`栏中进行可视化属性配置
- 中部：配置区
- 右侧：预览区，用于选择图表类型和预览图表

![编辑图表](/datart-docs/images/datachart/1-1-1.png)

### 1.1 字段列表

在左上角的下拉菜单中关联数据视图，所选数据视图的字段列表会展示在左侧面板上，不同字段类型有不同的前缀图标，`字符`和`日期`型显示为蓝色，`数值`型显示为绿色

#### 1.1.1 计算字段

点击字段列表顶部的加号按钮，可以创建计算字段

![计算字段-1](/datart-docs/images/datachart/1-1-1-1.png)

创建一个计算字段需要填写名称、类型和表达式；在中部的编辑器内编写表达式，计算字段的表达式仅允许包含以下内容：
- 字段名称：表达式中所使用的字段名称格式为 `[字段名称]`，点击左侧字段列表中的字段，会自动添加字段名称到编辑器光标所在处
- 函数：datart 内置了55个通用函数，已分好类、在右侧以列表展示，点击函数名称会自动添加到编辑器光标所在处。在编辑器中光标移动到函数名称上时，下方会提示函数简介和语法。另外，datart 未支持的通用函数、但数据源的 SQL 语法可以支持的，开发者也可以写到表达式中
- 运算符：支持 `+` `-` `*` `/` 等常规 SQL 运算符
- 变量：*（开发中）*

未按标准书写的表达式在保存时会提示错误。保存成功后，计算字段显示为橙色，可以像使用常规字段一样拖拽计算字段到`数据`配置栏中

![计算字段-2](/datart-docs/images/datachart/1-1-1-2.png)

### 1.2 数据

将字段拖拽到数据配置栏中，来确定图表的数据来源。数据配置变化会触发重新查询

#### 1.2.1 维度和指标

datart 没有预定义维度和指标，而是通过图表提供的数据配置项类型来对字段进行处理，配置项详情可以参考[自定义图表插件](chart_plugin)章节。其中`维度`型配置项会对拖入的字段做分组处理，`指标`型配置项会对拖入的字段做聚合处理。

![维度和指标](/datart-docs/images/datachart/1-2-1-1.png)

指标配置项支持在下拉菜单中对拖入的字段设置：
- 聚合方式：
  - 数值型字段支持 `总计`、`平均值`、`计数`、`去重计数`、`最大值`、`最小值` 6种聚合方式
  - 字符和日期型字段支持 `计数`、`去重计数` 2种聚合方式
  - 如果拖入的计算字段为数值型、并且表达式里已经包含聚合函数的情况下，是无法在下拉菜单中选择聚合方式的
- 数值格式：
  - 默认格式
  - 数值：可以设置小数位数、单位和千分位分隔
  - 货币：可以设置小数位数、单位和千分位分隔
  - 百分比：可以设置小数位数
  - 科学型：可以设置小数位数
- 着色：部分图表支持设置指标数据在图表上显示的颜色，优先级低于着色配置项

#### 1.2.2 筛选

筛选配置项支持拖入任意字段，不同的字段类型配置面板有所差别，支持将筛选字段以控制器形式展示出来供用户操作

##### 1.2.2.1 字符型字段筛选

字符型字段默认情况下支持以下方式配置筛选：

- 常规：即时查询字段去重值作为筛选项
  - 支持在筛选项里选择一到多项作为默认值
  - 支持单选按钮、单/多选下拉菜单作为控制器，取决于默认值数量

  ![字符型字段筛选-1](/datart-docs/images/datachart/1-2-2-1-1.png)

- 自定义：手动添加筛选项
  - 支持快捷选择字段去重值添加到筛选项
  - 支持拖拽改变筛选项顺序
  - 支持在筛选项里选择一到多项作为默认值
  - 支持单选按钮、单/多选下拉菜单作为控制器，取决于默认值数量

  ![字符型字段筛选-2](/datart-docs/images/datachart/1-2-2-1-2.png)

- 条件：配置一个条件表达式作为筛选默认值
  - 仅支持文本输入框作为控制器

  ![字符型字段筛选-3](/datart-docs/images/datachart/1-2-2-1-3.png)

在选择了`聚合方式`的情况下，字符型字段将转换为数值型字段参与筛选

  ![字符型字段筛选-4](/datart-docs/images/datachart/1-2-2-1-4.png)

##### 1.2.2.2 数值型字段筛选

数值型字段支持以下方式配置筛选：

- 区间：填写一个范围作为筛选默认值
  - 支持数值范围和滑块作为控制器

  ![数值型字段筛选-1](/datart-docs/images/datachart/1-2-2-2-1.png)

- 条件：配置一个条件表达式作为筛选默认值
  - 仅支持数值输入框作为控制器

  ![数值型字段筛选-2](/datart-docs/images/datachart/1-2-2-2-2.png)

无论是否选择`聚合方式`，数值型字段始终作为数值参与筛选

##### 1.2.2.3 日期型字段筛选

日期型字段支持以下方式配置筛选：

- 推荐：快捷选项，选定一个常用的时间范围

  ![日期型字段筛选-1](/datart-docs/images/datachart/1-2-2-3-1.png)

- 手动：手动选择一个时间范围；可以选择精确或是相对时间

  ![日期型字段筛选-2](/datart-docs/images/datachart/1-2-2-3-2.png)

日期型字段仅支持日期范围作为控制器

##### 1.2.2.4 是否可见

隐藏：不使用控制器改变筛选值，仅默认值生效

显示：需要选择展示用的控制器，在图表预浏览面，查看用户可以通过操作控制器来改变筛选条件

条件：在图表里有1个及以上字符型字段参与筛选时，新建筛选时可以选择1个字符型筛选作为自身可见与否的依赖条件，当依赖的筛选值满足表达式时才会显示控制器

![是否可见](/datart-docs/images/datachart/1-2-2-4-1.png)

##### 1.2.2.5 控制器

控制器是筛选在图表浏览界面的可视化展示，通过预定义的控制器形式，用户可以自行更改筛选值来动态查询数据。数据图表的控制器集中展示在图表上方

datart 数据图表支持以下类型控制器：

- 字符：多选下拉菜单、单选下拉菜单、单选按钮、文本输入框

![控制器-1](/datart-docs/images/datachart/1-2-2-5-1.png)

- 数值：数值范围、滑块、数值输入框

![控制器-2](/datart-docs/images/datachart/1-2-2-5-2.png)

- 日期：日期范围

![控制器-3](/datart-docs/images/datachart/1-2-2-5-3.png)

可以在配置界面设置控制器宽度，默认情况下自适应展示

#### 1.2.3 着色

着色配置项支持放入一个字段来对图表做颜色可视化编码，目前仅支持拖入字符型字段。

当拖入字符型字段时，字段会被作为`维度`进行分组，图表会依据字段值和预设的颜色分成多系列进行展示，图例中会展示系列与颜色详情

![着色](/datart-docs/images/datachart/1-2-3-1.png)

#### 1.2.4 其他

- 信息：部分直角坐标系图表支持，只能放置数值型字段，拖入的字段会被当做`指标`做聚合处理
- 尺寸：用于散点图和气泡地图做节点大小编码，拖入的字段会被当做`指标`做聚合处理

#### 1.2.5 字段设置

可以点击拖入数据配置项的字段，在下拉菜单中对字段进行设置，目前支持以下通用设置：
- 别名：改变字段在图表上的显示名称
- 排序：对字段值进行排序，选项为：
  - 默认：即不排序
  - 升序
  - 降序

### 1.3 样式

样式配置栏与图表相关，用于改变图表的展示规则。样式配置变化不会触发查询

### 1.4 配置

配置栏中包含一些额外的配置选项

#### 1.4.1 参考线

可以给部分直角坐标系图表设置参考线和参考区间，目前仅支持折线图、面积图、柱状图、散点图和双Y轴图

参考线需要关联到1个指标，数值可以选择关联指标的最大值、最小值、平均值，也可以选择手动设置常量值

参考区间需要设置起始值和结束值，每个值分别需要关联1个指标，数值可以选择关联指标的最大值、最小值、平均值，也可以选择手动设置常量值

#### 1.4.2 分页

明细表可以进行分页设置

## 2. 预览图表

配置图表时可以在编辑器右侧即时预览图表，可以选择预览区域上方的小图标切换图表；鼠标悬停到图标上可以查看该图表正常展示所需的条件

![预览图表-1](/datart-docs/images/datachart/2-1-1.png)

在预览区的右上角，可以点击切换图表 -> 原始数据 -> SQL语句

![预览图表-2](/datart-docs/images/datachart/2-1-2.png)

![预览图表-3](/datart-docs/images/datachart/2-1-3.png)

## 3. 基础功能

### 3.1 新建数据图表和目录

点击目录树顶部的加号按钮，选择`新建数据图表`或`新建目录`会弹出新建表单，填写名称和所属目录即可完成创建

![新建](/datart-docs/images/datachart/3-1-1.png)

### 3.2 编辑基本信息

点击目录树右侧的扩展按钮按钮，选择`基本信息`，即可对数据图表/目录的基本信息进行编辑

![编辑](/datart-docs/images/datachart/3-1-2.png)

### 3.3 发布/取消发布数据图表

在数据图表浏览界面的工具栏上点击`发布`按钮来发布一个数据图表，未发布前数据图表处理制作中状态，此时对拥有查看权限的成员不可见；发布之后拥有查看权限的成员才能看到

![发布-1](/datart-docs/images/datachart/3-3-1.png)

数据图表发布之后，点击工具栏上的`取消发布`按钮，该图表会重新回到制作中状态

![发布-2](/datart-docs/images/datachart/3-3-2.png)

### 3.4 删除目录/移至回收站

点击目录树右侧的扩展按钮按钮，如果是目录，会显示`删除`按钮，点击并确认之后会永久删除该目录；如果是数据图表，会显示`移至回收站`按钮，点击并确认之后，该数据图表会被移动到回收站归档，无法再被使用

![回收站-1](/datart-docs/images/datachart/3-4-1.png)
![回收站-2](/datart-docs/images/datachart/3-4-2.png)

### 3.5 还原

点击目录树顶部的`扩展`按钮，进入回收站

![还原-1](/datart-docs/images/datachart/3-5-1.png)

系统会将移至回收站的数据图表重命名，规则为`原名称.时间戳`；点击回收站列表的任意数据图表，右侧区域会展示该数据图表的详细信息，为只读状态

![还原-2](/datart-docs/images/datachart/3-5-2.png)

点击列表右侧扩展按钮，选择`还原`，在弹窗表单中需要重新填写还原后的名称和目录，填写完成后，点击保存按钮完成还原

![还原-3](/datart-docs/images/datachart/3-5-3.png)

### 3.6 删除

查看回收站列表里的数据图表信息时，点击列表右侧扩展按钮，选择`删除`，确认对话框之后，将会永久删除该数据图表

![删除](/datart-docs/images/datachart/3-6-1.png)

### 3.7 搜索

点击目录树顶部的`搜索`按钮，会弹出关键字搜索框，可以按照名称检索数据图表、仪表板和目录

![搜索](/datart-docs/images/datachart/3-7-1.png)