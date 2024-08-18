---
title: Java-1-爪洼-实现类
tags:
  - Java
  - 面向对象
categories:
  - Java
abbrlink: 9c53426d
date: 2023-07-02 00:05:20
cover: https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/lofter_1679044503548.jpg
---

# 前言

学习Java，首先关于基础知识部分，在菜鸟教程：https://www.runoob.com/java/java-tutorial.html 中已经介绍地很清楚了，不再赘述，需要时查阅即可。

# 类的构造

Java作为一门面向对象语言，应该重点关注一下类和对象的概念，下面实践一下，构建一个类：

```java
class Bottle {
    private int id;
    private String name;
    private long price;
    private double capacity;
    private boolean filled;

    public int getId(){
        return this.id;
    }
    
    public void setId(int id){
        this.id=id;
    }
}
```

可以发现，通常来说，我们不将属性定义为 public 的，而是私有化保护内部数据，只暴露数据的操作接口。

当我们拥有一个类之后，就可以在 MainClass 中引用了。首先我们需要 new 一个对象，然后将他实例化。以下为示例：

```java
public class MainClass {
    public static void main(String[] argv) {
        Bottle bottle = new Bottle();  //new Bottle() 即构造函数
        bottle.setName("Cola");
        bottle.setPrice(3);
        bottle.setId(1);
        bottle.setCapacity(100.0);
        bottle.setFilled(true);
    }
}
```

实例化的过程中我们会用到构造函数，所以在类中需要以 **public 类名**的方式定义构造函数。所以在这里，我们给之前构造的类定义以下构造函数：

```java
class Bottle {
    private int id;
    private String name;
    private long price;
    private double capacity;
    private boolean filled;

    public int getId(){
        return this.id;
    }
    
    public Bottle (int id, String name, long price, double capacity, boolean filled){
        this.id = id;
        this.name = name;
        this.price = price;
        this.capacity = capacity;
        this.filled = filled;
    }
}
```

# 容器

Java 容器分为 Collection 和 Map 两大类，用于存储数据和对象。以下为基础的容器知识入门：[ java容器超详细_CoderWriter的博客-CSDN博客](https://blog.csdn.net/qq_43969123/article/details/105804956)。

# 练习题

## 题面

想象你是一个冒险者，现在正在一个新的星球上进行探险，这个过程中你需要努力收集各种物品来不断增强自身能力值。在第一个 task 中你需要完成两个任务：

- 对基本物品 Bottle 和冒险者 Adventurer 进行建模
- 利用容器的知识，管理多个冒险者

首先，你需要构造一个 **Bottle** 类，来表示冒险者需要用到的瓶子类，要求 **Bottle** 类包含属性：ID，名字，价格，容量，和表达瓶子是否装满的标志量。

接着，再构造一个**Adventurer**类，用来表示冒险者类，要求**Adventurer**类包含属性：ID，名字，承载多个Bottle的容器。

在这个问题中，你需要管理多个冒险者。初始时，你没有需要管理的冒险者。接下来会有 12个操作：

1. 加入一个需要管理的冒险者
2. 给某个冒险者增加一个瓶子
3. 删除某个冒险者的某个瓶子
4. 更新某个冒险者所持有的某个瓶子的价格
5. 更新某个冒险者所持有的某个瓶子是否装满
6. 查询某个冒险者所持有的某个瓶子的名字
7. 查询某个冒险者所持有的某个瓶子的价格
8. 查询某个冒险者所持有的某个瓶子的容量
9. 查询某个冒险者所持有的某个瓶子是否装满
10. 输出某个冒险者所持有的某个瓶子的字符串描述
11. 查询某个冒险者所持有瓶子的价格之和
12. 查询某个冒险者所持有瓶子价格的最大值

操作1-5不需要任何输出，只需要对操作 6-12 进行输出回答。

------

## 输入/输出格式

第一行一个整数 m，表示操作的个数。

接下来的 m 行，每行一个形如 `{type} {attribute}` 的操作，`{type}` 和 `{attribute}` 间、若干个 `{attribute}` 间使用若干个空格分割，操作输入形式及其含义如下：

| type | attribute                                     | 意义                                                         | 输出文本                                                     |
| :--- | :-------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1    | `{adv_id} {name}`                             | 加入一个 ID 为 `{adv_id}`、名字为 `{name}` 的冒险者，且未持有任何瓶子 | 无                                                           |
| 2    | `{adv_id} {bot_id} {name} {price} {capacity}` | 给 ID 为 `{adv_id}` 的冒险者增加一个瓶子，瓶子的 ID、名字、价格、容量分别为 `{bot_id}`、`{name}`、`{price}`、`{capacity}`，**且默认为已装满** | 无                                                           |
| 3    | `{adv_id} {bot_id}`                           | 将 ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子删除   | 无                                                           |
| 4    | `{adv_id} {bot_id}{price}`                    | 将 ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的价格更改为 `{price}` | 无                                                           |
| 5    | `{adv_id} {bot_id}{filled}`                   | 将 ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的装满的状态更改为 `{filled}` | 无                                                           |
| 6    | `{adv_id} {bot_id}`                           | 查询ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的名字 | 一个字符串，表示瓶子名字                                     |
| 7    | `{adv_id} {bot_id}`                           | 查询ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的价格 | 一个整数，表示瓶子价格                                       |
| 8    | `{adv_id} {bot_id}`                           | 查询ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的容量 | 一个浮点数，表示瓶子容量                                     |
| 9    | `{adv_id} {bot_id}`                           | 查询ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子是否装满 | 一个字符串，表示瓶子是否装满（输出true表示装满，false表示没有装满） |
| 10   | `{adv_id} {bot_id}`                           | 查询ID 为 `{adv_id}` 的冒险者的 id 为 `{bot_id}` 的瓶子的字符串描述 | 以 `The bottle's id is {id}, name is {name}, capacity is {capacity}, filled is {filled}.` 的形式打印状态。 |
| 11   | `{adv_id}`                                    | 查询 ID 为 `{adv_id}` 的冒险者所持有瓶子的价格之和           | 一个整数，表示瓶子价格之和                                   |
| 12   | `{adv_id}`                                    | 查询 ID 为 `{adv_id}` 的冒险者所持有瓶子价格的最大值         | 一个整数，表示瓶子价格的最大值                               |

## 数据范围与操作限制

### 变量约束

| 变量                  | 类型   | 说明                               |
| :-------------------- | :----- | :--------------------------------- |
| `id (adv_id, bot_id)` | 整数   | 取值范围：0 - 2147483647           |
| `name`                | 字符串 | 保证不会出现空白字符               |
| `price`               | 长整数 | 在 long 精度范围内，且保证不小于 0 |
| `capacity`            | 浮点数 | 在 double 精度范围内               |

### 操作约束

- **保证所有冒险者与瓶子的 ID 两两不同。**
- 操作 2-12：保证冒险者 ID 一定存在。
- 操作 3-10：冒险者一定持有该 ID 的瓶子。
- 操作 11：若冒险者不持有任何瓶子，则输出 0。
- 操作 12：冒险者持有至少一个瓶子。
- 操作数满足 1≤m≤2000。

## 测试样例

### **样例输入**

```none
17
1 2 Co20ocvblT
1 30 Al8QnWnkS7
1 91 pqWY5UNcm4
2 91  7 q6DlfOJGzf 82 48.5801
2 30  8 0vyv58Ec49 25 12.1451
2 30  56 OdcdRFEw7s 13 34.3745
2 91  64 jMZ9uBOLy4 45 38.1122
2 2  65 COIecJNdIH 89 41.7995
2 2  26 UXDaKL9P1O 79 36.1887
2 91  15 Vy6EKNgojP 10 35.5545
3 91 7
4 30 56 67
5 91 15 true
6 2 65
7 91 15
8 2 26
9 91 15
```

### **样例输出**

```none
COIecJNdIH
10
36.1887
true
```

# 题目思考&代码

我的思路：因为**保证所有冒险者与瓶子的 ID 两两不同**，采取 HashMap 管理冒险者。然后我们根据所需的操作，在 Bottle 类和 Adventurer 类里面添加方法即可。详细情况可见下图：

![](https://miaomiao-1-1319022947.cos.ap-beijing.myqcloud.com/202307101727.png)

## MainClass

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.io.PrintStream;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;

public class MainClass {
    public static void main(String[] argv) throws FileNotFoundException {
        Scanner scanner = new Scanner(System.in);
        int m = scanner.nextInt();
        int op; //操作符，标记是哪个指令
        int advId;
        HashMap<Integer, Adventurer> adventurers = new HashMap<>();
        for (int i = 0; i < m; i++) {
            op = scanner.nextInt();
            advId = scanner.nextInt();
            Adventurer adventurer = new Adventurer();
            if (op == 1) {
                ArrayList<Bottle> bottles = new ArrayList<>();
                adventurer.setAdventurer(advId, scanner.next(), bottles);
                adventurers.put(advId, adventurer);
            } else if (op >= 2 && op <= 5) {
                adventurer = adventurers.get(advId);
                ReadData.noPrint(op, adventurer, scanner);
            } else if (op >= 6 && op <= 10) {
                //System.out.print(i+2 + " ");
                adventurer = adventurers.get(advId);
                ReadData.opPrint(op, adventurer, scanner);
            } else {
                //System.out.print(i+2 + " ");
                adventurer = adventurers.get(advId);
                ReadData.arithPrint(op, adventurer);
            }
            scanner.nextLine();
        }
    }
}

```

## Bottle 类

```java
class Bottle {
    private int id;
    private String name;
    private long price;
    private double capacity;
    private boolean filled;

    public int getId() {
        return this.id;
    }

    public String getName() {
        return this.name;
    }

    public long getPrice() {
        return this.price;
    }

    public double getCap() {
        return this.capacity;
    }

    public boolean getFilled() {
        return this.filled;
    }

    public void setPrice(long price) {
        this.price = price;
    }

    public void setFilled(boolean filled) {
        this.filled = filled;
    }

    public Bottle(int id, String name, long price, double capacity) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.capacity = capacity;
        this.filled = true;
    }
}

```

## Adventurer 类

```java
import java.math.BigInteger;
import java.util.ArrayList;

public class Adventurer {
    private int id;
    private String name;
    private ArrayList<Bottle> bottles;

    public void addBot(int botId, String botName, long botPrice, double botCap) {
        Bottle bottle = new Bottle(botId, botName, botPrice, botCap);
        bottles.add(bottle);
    }

    public void removeBot(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                bottles.remove(i);
                break;
            }
        }
    }

    public void modPrice(int botId, long botPrice) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                i.setPrice(botPrice);
                break;
            }
        }
    }

    public void modFilled(int botId, boolean botFilled) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                i.setFilled(botFilled);
                break;
            }
        }
    }

    public void checkName(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                System.out.println(i.getName());
                break;
            }
        }
    }

    public void checkPrice(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                System.out.println(i.getPrice());
                break;
            }
        }
    }

    public void checkCap(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                System.out.println(i.getCap());
                break;
            }
        }
    }

    public void checkFilled(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                System.out.println(i.getFilled());
                break;
            }
        }
    }

    public void describeBot(int botId) {
        for (Bottle i : bottles) {
            if (i.getId() == botId) {
                System.out.print("The bottle's id is " + i.getId());
                System.out.print(", name is " + i.getName());
                System.out.print(", capacity is " + i.getCap());
                System.out.println(", filled is " + i.getFilled() + ".");
                break;
            }
        }
    }

    public void addPrice() {
        BigInteger a = new BigInteger("0");
        for (Bottle i : bottles) {
            BigInteger b = BigInteger.valueOf(i.getPrice());
            a = b.add(a);
        }
        System.out.println(a);
    }

    public void maxPrice() {
        long ans = 0;
        long b = 0;
        for (Bottle i : bottles) {
            b = i.getPrice();
            if (b > ans) {
                ans = b;
            }
        }
        System.out.print(ans + "\n");
    }

    public void setAdventurer(int id, String name, ArrayList<Bottle> bottles) {
        this.id = id;
        this.name = name;
        this.bottles = bottles;
    }
}

```

## ReadData

```java
import java.util.Scanner;

public class ReadData {
    public static void noPrint(int op, Adventurer adventurer, Scanner scanner) {
        int botId;
        switch (op) {
            case 2:
                botId = scanner.nextInt();
                adventurer.addBot(botId, scanner.next(), scanner.nextLong(), scanner.nextDouble());
                break;

            case 3:
                adventurer.removeBot(scanner.nextInt());
                break;

            case 4:
                adventurer.modPrice(scanner.nextInt(), scanner.nextLong());
                break;

            case 5:
                adventurer.modFilled(scanner.nextInt(), scanner.nextBoolean());
                break;

            default:
                break;
        }
    }

    public static void opPrint(int op, Adventurer adventurer, Scanner scanner) {
        switch (op) {
            case 6:
                adventurer.checkName(scanner.nextInt());
                break;

            case 7:
                adventurer.checkPrice(scanner.nextInt());
                break;

            case 8:
                adventurer.checkCap(scanner.nextInt());
                break;

            case 9:
                adventurer.checkFilled(scanner.nextInt());
                break;

            case 10:
                adventurer.describeBot(scanner.nextInt());
                break;

            default:
                break;
        }
    }

    public static void arithPrint(int op, Adventurer adventurer) {
        switch (op) {
            case 11:
                adventurer.addPrice();
                break;

            case 12:
                adventurer.maxPrice();
                break;

            default:
                break;
        }
    }
}

```

