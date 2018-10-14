# code_style

<!-- vim-markdown-toc GFM -->

* [1 软件工程](#1-软件工程)
* [2 需求设计及系统设计](#2-需求设计及系统设计)
    * [2.1 必须的文档](#21-必须的文档)
* [3 代码编写](#3-代码编写)
    * [3.1 代码规范](#31-代码规范)
    * [3.2 Code review 步骤](#32-code-review-步骤)

<!-- vim-markdown-toc -->

## 1 软件工程
> * 一流代码的特性
>   * 高效（Fast）
>   * 鲁棒（Solid and Robust）
>   * 简洁（Maintainable and Simple）
>   * 共享（Re-usable）
>   * 可测试（Testable）
>   * 可移植（Portable）
>   * 可监控（Monitorable）
>   * 可运维（Operational）
>     * 部署 Easy to deploy
>     * 变更 Easy to changes
>     * 维护 Easy to maintain
>     * 监控 Easy to observable
>   * 可扩展（Scalable & Extensible）
> * 需求分析 & 系统设计
>   * 需求分析：定义系统 / 软件黑盒的行为（external,what）
>   * 系统设计：设计系统 / 软件白盒的机制（internal，how&why）

## 2 需求设计及系统设计

文档是设计过程中使用的工具和设计过程的结果

### 2.1 必须的文档
凡是不那么“显而易见”的地方，最好都留下文档

> * 需求设计文档:需求，重点，取舍过程
> * 接口文档：函数，参数，返回值
> * 关键性的算法文档：思路，关键点
> * 系统总体框架：全局的思路

文档中不仅仅要留下来设计的结果（what），也要留下思考的过程（why）：留下决策的依据，便于后面的工作

## 3 代码编写

### 3.1 代码规范

* [python](./python/README.md)

### 3.2 Code review 步骤

> * Step 1：系统全貌
>   * 模块划分的逻辑，模块之间的关系
> * Step 2：模块级别
>   * 看清模块内的逻辑
>   * 关键数据，关键的类、函数
> * Step 3：类、函数内部的逻辑
> * Step 4：细节
>   * Layout，命名，...
