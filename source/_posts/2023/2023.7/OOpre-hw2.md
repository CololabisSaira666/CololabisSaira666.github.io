---
title: Java-2-实现类后就要继承和重写
categories:
  - Java
abbrlink: e2b57d7f
date: 2023-07-10 17:52:58
tags:
  - 面向对象
cover: https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/202307151629zhai.jpg
---

# 继承

继承，即为定义子类继承父类的特征和行为。`A extends B`：`A` 继承了 `B` ，`A` 是 `B` 的子类， `A` 得到了 `B` 的属性和方法。

## 向上转型

建立了继承关系之后，可以使用父类型去引用通过子类型创建的对象。

## 向下转型

obj **instanceof** A：obj 为一个对象引用，A 为一个类型（类或接口），表达式的取值结果为布尔型，如果 obj 的创建类型为 A，则结果为 true，否则为 false。若结果为 true，使用向下转型，使用一个 A 类型的对象来引用obj： `A ao = (A)obj`。

# 对象方法的重写和复用

方法重写：让子类重新实现一个在父类中已经实现的方法。

通过使用关键词**super**，确保进行重写时调用父类中此定义方法。

# 异常处理



# 练习题

在上次题目的基础上进行增量开发，上次的题目在：https://cololabissaira666.github.io/post/9c53426d.html

需要做的工作有：

- 建立 Equipment 装备类。我们将 Task1 中的 Bottle 以及下面增加的所有药水类、武器类统称为 *“装备类”*，使所有装备类均继承自 Equipment 类（该类因而可称为基类， base class），请将所有装备都具有的属性定义在这个类里。同时，Task1 中每位冒险者拥有承载多个 Bottle 的容器，这里将承载 Bottle 的容器改为承载所有装备类的容器。
- 为冒险者新增一些属性如下：生命值 （`health`, 浮点数，默认值 100.0）、经验值（ `exp`, 浮点数，默认 0.0）、金钱数（ `money`, 浮点数，默认 0.0）。
- 增加药水 HealingPotion 和 ExpBottle 并继承 Bottle 的全部属性；添加“武器类” Sword 以及 RareSword 和 EpicSword，他们继承 Sword 全部属性。见下表：

| 药水类型      | 属性                                                         | 属性类型                                     |
| :------------ | :----------------------------------------------------------- | :------------------------------------------- |
| HealingPotion | 包括 Bottle 的全部属性，新增加属性 efficiency，代表药水的治疗效果 | Bottle 原有属性不变，efficiency 为浮点数类型 |
| ExpBottle     | 包括 Bottle 的全部属性，新增加属性 expRatio，代表水瓶对于经验值的增强效果 | Bottle 原有属性不变，expRatio为浮点数类型    |

| 武器类型  | 属性                                                         | 属性类型                                                     |
| :-------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Sword     | id, name, price, sharpness。其中 id, name, price 与 Task1 中 Bottle 类的定义相同，sharpness 表示武器的锋利程度 | id, name, price 与 Bottle 类中相应属性类型相同，sharpness 为浮点数类型 |
| RareSword | 包括 Sword 的全部属性，新增加属性 extraExpBonus，代表使用武器的附加效果 | Sword 原有属性不变，extraExpBonus 为浮点数类型               |
| EpicSword | 包括 Sword 的全部属性，新增加属性 evolveRatio，代表使用武器的附加效果 | Sword 原有属性不变，evolveRatio 为浮点数类型                 |

- 为每一种装备设置一个**使用**方法，定义如下，设冒险者A使用了装备B：

| 装备B的类型                                       | 使用效果                                                     | 输出文本                                                     |
| :------------------------------------------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Bottle（若 filled 为 true）                       | A的生命值增加[B的 capacity 属性]的十分之一，之后 B 的 filled 变为 false，price 变为原来的十分之一（向下取整）。 | {A 的 name} drank {B 的 name} and recovered {生命值增加量}.  |
| HealingPotion（若 filled为true）                  | A的生命值增加[B的 capacity 属性]的十分之一，之后 B 的 filled 变为 false，price 变为原来的十分之一（向下取整）。然后A的生命值再额外增加[B的capacity属性]乘以[B的efficiency属性]的量。 | {A 的 name} drank {B 的 name} and recovered {生命值增加量}. {A 的 name} recovered extra {生命值额外增加量}. |
| ExpBottle（若 filled 为 true）                    | A的生命值增加[B的 capacity 属性]的十分之一，之后 B 的 filled 变为 false，price 变为原来的十分之一（向下取整）。然后A的经验值变为原来的[B的expRatio属性]倍。 | {A 的 name} drank {B 的 name} and recovered {生命值增加量}. {A 的 name}’s exp became {A 变化后的经验}. |
| Bottle/HealingPotion/ExpBottle（若filled为false） | 无任何作用效果。                                             | Failed to use {B 的 name} because it is empty.               |
| Sword                                             | 使用后A的生命值减少 10.0、经验值增加 10.0，金钱数增加相当于[B 的 sharpness属性]一倍的量。 | {A 的 name} used {B 的 name} and earned {增加的金钱数}.      |
| RareSword                                         | 使用后A的生命值减少 10.0、经验值增加 10.0，金钱数增加相当于[B 的 sharpness属性]一倍的量。然后 A 的经验值额外增加[B 的 extraExpBonus 属性]。 | {A 的name} used {B 的name} and earned {增加的金钱数}. {A 的name} got extra exp {额外获得的经验}. |
| EpicSword                                         | 使用后A的生命值减少 10.0、经验值增加 10.0，金钱数增加相当于[B 的 sharpness属性]一倍的量。然后B的sharpness 属性变为原来的 evolveRatio倍。 | {A 的 name} used {B 的 name} and earned {增加的金钱数}. {B 的 name}’s sharpness became {B 变化后的sharpness}. |

- 实现各项装备的查询和增删指令，设置如下操作：
  1. 加入一个冒险者
  2. 给某个冒险者添加某件装备（装备包括药水和武器）
  3. 删除某个冒险者拥有的某个装备
  4. 查询某个冒险者所拥有装备的价格之和
  5. 查询某个冒险者所拥有装备的价格最大值
  6. 查询某个冒险者拥有的装备总数
  7. 打印一个装备的全部属性，属性的输出顺序与输入创建该装备时给定的各参数顺序一致，具体格式详见下方 *属性打印方式*
  8. 某个冒险者使用其拥有的某个装备
  9. 打印某个冒险者的所有状态

------

## 输入、输出格式

第一行一个整数 m，表示操作的个数。

接下来的 m行，每行一个形如 `{type} {attribute}` 的操作，`{type}` 和 `{attribute}` 间、若干个 `{attribute}` 间使用若干个空格分割，操作输入形式及其含义如下：

| type | attribute                                                    | 意义                                                         | 输出文本                                                     |
| :--- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1    | `{adv_id} {name}`                                            | 加入一个 ID 为 `{adv_id}`、名字为 `{name}` 的冒险者，且未持有任何装备 | 无                                                           |
| 2    | `{adv_id} {equipment_type} {vars}`（equipment_type和vars的含义见下表） | 给予某个人某件装备，装备类型由 `{equipment_type}` 定义，属性由 `{vars}` 定义，**所有的瓶子初始默认装满** | 无                                                           |
| 3    | `{adv_id} {equipment_id}`                                    | 删除 ID 为 `{adv_id}` 的冒险者的 ID 为 `{equipment_id}` 的装备 | 无                                                           |
| 4    | `{adv_id}`                                                   | 查询 ID 为 `{adv_id}` 的冒险者所持有装备的价格之和           | 一个整数，表示该冒险者所有装备的价格总和                     |
| 5    | `{adv_id}`                                                   | 查询 ID 为 `{adv_id}` 的冒险者所持有装备价格的最大值         | 一个整数，表示该冒险者所有装备价格的最大值                   |
| 6    | `{adv_id}`                                                   | 查询 ID 为 `{adv_id}` 的冒险者的装备总数                     | 一个整数，表示该冒险者所有装备的数量之和                     |
| 7    | `{adv_id} {equipment_id}`                                    | 打印 ID 为 `{equipment_id}` 的装备的全部属性                 | 该装备的全部属性，格式见下文“属性打印方式”                   |
| 8    | `{adv_id}{equipment_id}`                                     | ID为 `{adv_id}` 的冒险者使用其 ID 为 `{equipment_id}` 的装备 | 装备在使用时会产生输出，除此之外无额外输出。                 |
| 9    | `{adv_id}`                                                   | 打印ID为 `{adv_id}` 的冒险者的所有状态。                     | 一个字符串表示冒险者的状态： `The adventurer's id is {adv_id}, name is {name}, health is {health}, exp is {exp}, money is {money}.` |

| 装备类型      | equipment_type | vars                                  |
| :------------ | :------------- | :------------------------------------ |
| Bottle        | 1              | id name price capacity                |
| HealingPotion | 2              | id name price capacity efficiency     |
| ExpBottle     | 3              | id name price capacity expRatio       |
| Sword         | 4              | id name price sharpness               |
| RareSword     | 5              | id name price sharpness extraExpBonus |
| EpicSword     | 6              | id name price sharpness evolveRatio   |

| 装备类型      | 属性打印方式                                                 |
| :------------ | :----------------------------------------------------------- |
| Bottle        | `The bottle's id is {id}, name is {name}, capacity is {capacity}, filled is {filled}.` |
| HealingPotion | `The healingPotion's id is {id}, name is {name}, capacity is {capacity}, filled is {filled}, efficiency is {efficiency}.` |
| ExpBottle     | `The expBottle's id is {id}, name is {name}, capacity is {capacity}, filled is {filled}, expRatio is {expRatio}.` |
| Sword         | `The sword's id is {id}, name is {name}, sharpness is {sharpness}.` |
| RareSword     | `The rareSword's id is {id}, name is {name}, sharpness is {sharpness}, extraExpBonus is {extraExpBonus}.` |
| EpicSword     | `The epicSword's id is {id}, name is {name}, sharpness is {sharpness}, evolveRatio is {evolveRatio}.` |

## 数据范围与操作限制

### 变量约束

| 变量                                                         | 类型   | 说明                               |
| :----------------------------------------------------------- | :----- | :--------------------------------- |
| id                                                           | 整数   | 取值范围：0 - 2147483647           |
| name                                                         | 字符串 | 保证不会出现空白字符               |
| price                                                        | 长整数 | 在 long 精度范围内，且保证不小于 0 |
| capacity, efficiency, expRatio, sharpness, extraExpBonus, evolveRatio, health, exp, money | 浮点数 | 在 double 精度范围内               |

### 操作约束

- 操作数满足 1≤m≤2000。
- **保证所有冒险者与装备的 ID 两两不同。**
- 操作2-9：冒险者 ID 一定存在。
- 操作 3,7,8：冒险者一定持有该 ID 的装备。
- 操作 4：若冒险者不持有任何装备，则输出 0。
- 操作 5：冒险者一定持有至少一个装备。

## 测试样例

### 输入样例

```none
17
1 2 Co20ocvblT
1 30 Al8QnWnkS7
1 91 pqWY5UNcm4
2 91 1 26 6DlfOJGzfY 74 96.3964
2 2 6 35 yv58Ec49pK 2 65.161 68.6988
2 2 1 71 FEw7siBqbW 64 66.534
2 91 2 44 OLy4CqtmrO 45 60.135 13.2503
2 30 1 56 H2EvYaqUXD 0 64.7676
2 91 6 65 Wjsn3jVy6E 60 20.1061 23.1743
2 2 2 28 0WnMAYPzUH 37 27.0554 10.4833
3 30 56
4 30
5 91
6 91
7 91 65
8 2 35
9 91
```

### 输出样例

```none
0
74
3
The epicSword's id is 65, name is Wjsn3jVy6E, sharpness is 20.1061, evolveRatio is 23.1743.
Co20ocvblT used yv58Ec49pK and earned 65.161.
yv58Ec49pK's sharpness became 4476.4825068.
The adventurer's id is 91, name is pqWY5UNcm4, health is 100.0, exp is 0.0, money is 0.0.
```

## 注

- “装备类”包括 Bottle, HealingPotion 等 6 个不同的类，而冒险者需要拥有一个可以承载这 6 个装备类的容器。为了避免为 6 个装备类分别维护容器的麻烦，我们可以使用“向上转型”，在 Adventurer 类中统一维护一个承载 Equipment 的容器，并让 6 个装备类全部继承自 Equipment 类。由于“多态”的特性，在向上转型后对象仍然不会失去其原先的装备性质。

# 代码及思路

总的来说，只要根据题意实现各个类，再微调hw-1的代码即可。个人感觉比较重要的部分是类的继承和方法重写，同时也要考虑向上转型的问题。

这次代码量增加了，为了方便阅读不直接放在下文，访问此链接即可：https://github.com/CololabisSaira666/aboutOO
