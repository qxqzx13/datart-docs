---
title: 权限
---

datart 使用[RBAC](https://en.wikipedia.org/wiki/Role-based_access_control)模型控制权限；在组织内，成员创建的数据源、数据视图、可视化、定时任务被视为资源，用户和角色为权限主体，管理者可以将资源的各类权限授予权限主体，通过这种方式来对完成对具体资源的权限控制

## 1. 权限类别

datart 中的权限共有2类，资源权限和数据权限

### 1.1 资源权限

资源权限在权限页面进行设置，使用上分3个维度进行控制

#### 1.1.1 功能

功能权限决定该模块入口是否在主导航栏中显示

![功能](/datart-docs/images/permission/1-1-1.png)

#### 1.1.2 新增

由于资源存储结构的区别，新增权限有两种不同情况

1. 列表结构的资源，新增权限独立启用和关闭

![新增](/datart-docs/images/permission/1-1-2.png)

2. 文件夹结构的资源，当赋予某文件夹`管理`权限时，即拥有了在该文件夹下创建、编辑和删除资源的权限。根目录为`所有资源`

#### 1.1.3 操作

操作权限即为对具体资源的管理权限；操作权限目前共有以下几种等级

1. 查看/使用：拥有对该资源的只读/使用权限
2. 管理：拥有对该资源的编辑和删除权限，如果对某文件夹拥有管理权限，即同时拥有了在该文件夹下创建、编辑和删除所有资源的权限；包含`查看/使用`权限
3. 下载：拥有对该资源的下载权限；可视化资源独有，包含`查看/使用`权限
4. 分享：拥有对该资源创建分享链接的权限；可视化资源独有，包含`查看/使用`权限

### 1.2 数据权限

数据权限通过对数据视图结果集的行、列进行控制来实现

#### 1.2.1 行权限

行权限通过变量来实现，具体使用方法请参考[变量章节](variable)

#### 1.2.2 列权限

列权限通设置具体数据视图中角色对结果集字段的访问权限来控制，具体使用方法请参考[列权限](view#列权限)章节

## 2. 资源权限设置

点击主导航栏中的`权限`菜单进入设置页面，目前仅组织拥有者可以进行设置

![设置](/datart-docs/images/permission/2-0-1.png)

### 2.1 常规视图

在常规视图下，左侧列表展示权限主体，共有`角色`和`成员`两个页签，方便管理者对具体角色或用户做整体权限规划

点击左侧列表中的权限主体，右侧区域会显示所有资源的权限细则

![常规视图](/datart-docs/images/permission/2-1-1.png)

### 2.2 资源视图

在资源视图下，左侧列表展示资源，共有`可视化`、`数据视图`、`数据源`和`定时任务`4个页签，方便管理者对具体资源进行权限设置

![资源视图-1](/datart-docs/images/permission/2-2-1.png)

点击左侧列表中的单条资源，右侧区域会显示所有权限主体的权限细则

![资源视图-2](/datart-docs/images/permission/2-2-2.png)

### 2.3 权限细则设置

点击单选按钮或复选框，对应的权限细则会立即生效

当勾选高等级权限时，其所包含的低等级权限会被级联选中；当取消低等级权限时，其已经勾选的高等级权限也会被级联取消

文件夹结构资源在勾选文件夹权限时，其子资源的权限会级联发生变化、与父级保持一致；如果需要子资源与父文件夹拥有不同权限，只需单独设置该子资源即可

## 3. 基础功能

### 3.1 搜索

可以在左侧列表对权限主体和资源进行检索

![搜索-1](/datart-docs/images/permission/3-1-1.png)

也可以在右侧区域对权限主体和资源进行检索

![搜索-2](/datart-docs/images/permission/3-1-2.png)