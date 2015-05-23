# 团队合作文档

### Git 工作流

#### 开发任务

**命名** 以 `issue` 加任务号为命名方式, 其他任务则以 `FooBar` 形式命名.

如：`issue_1`

如：`issue_foo_bar`

#### 版本修复

**命名** 以 `fix` 加任务号为命名方式, 其他任务则以 `FooBar` 形式命名.

如：`fix_1`

如：`fix_foo_bar`

#### 发布版本流程

当需要释放一个版本时，需要从 develop 分支拉出一个分支出来，然后这个版本所有修复的 bug 需要合并到版本分支和 develop 分支。

对于主分支(master)修复 bug 也是同样的思路。

##### 步骤

1. 从 develop 分支拉出一个分支 release-v0.1
2. 当需要修复一个 release-v0.1 分支，则从 release-v0.1 拉出一个 fix_foo_bar .
3. 合并时则需要提交到 release-v0.1 和 develop 分支.

这个主要参考 [git-flow](https://ihower.tw/blog/archives/5140) 工作流, 可以了解一下.
