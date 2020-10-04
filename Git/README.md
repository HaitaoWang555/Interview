## Merge与Rebase

  - merge：直接将两个状态合并，并产⽣⼀个合并提交

  - rebase：将某个状态上的变更（commit）挨个重演

  - merge的优缺点

    - 优点
      - 简单，易于理解
      - 记录了完整的历史
      - 冲突解决简单
    - 缺点
      - 历史杂乱⽆章
      - 对bisect不友好

  - rebase的优缺点

    - 优点
      - 分⽀历史是⼀条直线，清楚直观
      - 对bisect友好
    - 缺点
      - 较为复杂，劝退新⼿
      - 如果冲突可能要重复解决（或者squash）
      - 会⼲扰别⼈？(和别⼈共享的分⽀永远不要force push)
    - 使⽤场景
      - 定时将你的分⽀和主⼲进⾏同步

  - git merge --squash
    - 优点
      - 把所有变更合在⼀起，更容易阅读，bisect友好
      - 想要回滚或者revert⾮常⽅便
    - 缺点
      - 丢失了所有的历史记录


## git checkout

- 将代码复原到任何⼀个状态上，但不修改仓库中的任何信息

  - git checkout v1.0.0
  - git checkout fd56bd
  - git checkout master
  - git checkout origin/master

- 新建分⽀

  - git checkout -b {任何可以代表分⽀状态的东⻄}

- 在⼯作⽬录和暂存区移动⽂件

  - git checkout --

## git reset

- 强⾏将当前分⽀HEAD指针移动到指定状态

  - git reset HEAD --hard (grhh)
  - git reset origin/master
  - git reset 3da2dfe
  - git reset HEAD~3

- --soft/--mixed/--hard

- 使⽤场景

  - 迅速将分⽀恢复到某个状态
  - squash commits，例如⽅便rebase

## git cherry-pick

- 将某个提交在另外的分⽀上重放

  - git cherry-pick 1a2b3c4d

- 使⽤场景

  - 希望把⼀个bug fix同步到较⽼的产品中
  - 在master上进⾏的变更希望进⼊release环节

## git revert

- 产⽣⼀个「反向提交」，撤销某个commit

  - git revert 1a2b3c4d

- 产⽣的「反向提交」可以再次进⾏revert

- 使⽤场景

  - 撤销历史中的某个更改，如bug或不恰当的功能
  - 回滚某次发布

## git bisect

- 在历史中查找某处引⼊的bug

  - git bisect start/reset
  - git bisect good/bad
  - git bisect run

- 使⽤场景

  - 在问题可以稳定重现的时候，迅速定位出问题的代码
  - 有的时候这⽐直接去debug更快捷

## git stash

- 临时性将⼯作⽬录的变更储存起来，然后清空⼯作⽬录

  ```bash
    git stash
    git stash list
    git stash pop # 恢复最近一次stash的文件
    git stash drop # 丢弃最近一次stash的文件
    git stash clear # 删除所有的stash
    it stash apply stash@{1} # 恢复某个暂时保存的工作
  ```


- 使⽤场景

  - 你正在开⼼的开发，突然来了⼀个线上bug
  - 你只好将⼿头的⼯作全部储存起来之后，开始别的⼯作
  - 结果⼜来了⼀件优先级更⾼的bug
  - 完成别的⼯作之后回来继续
  - 类⽐「存档/读档」

## Git工作流

- ⼀个或者两个共享的稳定分⽀

  - master
  - develop

- 好处：

  - 清楚直观
  - 每个提交代表⼀个单独的完整的功能点，⽅便回滚
  - 每个提交都是稳定的，⽅便进⾏bisect

- 临时性的功能分⽀

  - feature
  - bugfix
  - release

