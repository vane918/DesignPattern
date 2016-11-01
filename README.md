# DesignPattern
##Java 设计模式（观察者模式、工厂模式、单例模式、策略模式、命令模式、装饰者模式）
> 设计模式（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。

###主要参照Hongyang的CSDN博客所写：
>[http://blog.csdn.net/lmj623565791/article/category/2206597](http://blog.csdn.net/lmj623565791/article/category/2206597)

###一. Blog Catalogue：
####1. [设计模式 观察者模式(Observer Pattern) 以微信公众服务为例](http://blog.csdn.net/lmj623565791/article/details/24179699)

####2. [设计模式 工厂模式(Factory Pattern) 从卖肉夹馍说起](http://blog.csdn.net/lmj623565791/article/details/24460585)

####3. [设计模式 单例设计模式(Singleton Pattern) 完全解析](http://blog.csdn.net/dmk877/article/details/50311791)

####4. [设计模式 策略模式(Strategy Pattern) 以角色游戏为背景](http://blog.csdn.net/lmj623565791/article/details/24116745)

####5. [设计模式 适配器模式(Adapter Pattern) 以手机充电器为例](http://blog.csdn.net/lmj623565791/article/details/25833393)

####6. [设计模式 命令模式(Command Pattern) 管理智能家电](http://blog.csdn.net/lmj623565791/article/details/24602057)

####7. [设计模式 装饰者模式(Decorator Pattern) 带你重回传奇世界](http://blog.csdn.net/lmj623565791/article/details/24269409)

-----

###二. Source Code
> - 1. [Observer](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/observer)
> - 2. [Factory](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/factory)
> - 3. [Singleton](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/singleton)
> - 4. [Strategy](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/strategy)
> - 5. [Adapter](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/adapter)
> - 6. [Command](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/command)
> - 7. [Decorator](https://github.com/youlookwhat/DesignPattern/tree/master/app/src/main/java/com/example/jingbin/designpattern/decorator)

----

###三. Pattern Analysis
####1. 观察者模式
 >  定义了对象之间的一对多的依赖，这样一来，当一个对象改变时，它的所有的依赖者都会收到通知并自动更新。

 - 对于JDK或者Andorid中都有很多地方实现了观察者模式，比如XXXView.addXXXListenter ， 当然了 XXXView.setOnXXXListener不一定是观察者模式，因为观察者模式是一种一对多的关系，对于setXXXListener是1对1的关系，应该叫回调。

 - 专题接口：[Subject.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/observer/interfaces/Subject.java) ;  3D服务号的实现类：[ObjectFor3D.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/observer/classs/ObjectFor3D.java)
 - 所有观察者需要实现此接口:[Observer.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/observer/interfaces/Observer.java)

--
####2. 工厂模式
简单列一下这个模式的家族：

- 1、静态工厂模式

	- 这个最常见了，项目中的辅助类，TextUtil.isEmpty等，类+静态方法。

- 2、简单工厂模式（店里买肉夹馍）

	- 根据类型直接创建肉夹馍：[SimpleRoujiaMoFactory.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/jdgc/SimpleRoujiaMoFactory.java)

- 3、工厂方法模式（开分店）
	-  定义：定义一个创建对象的接口，但由子类决定要实例化的类是哪一个。工厂方法模式把类实例化的过程推迟到子类。
	-  对比定义：
  	 - 1、定义了创建对象的一个接口：public abstract RouJiaMo sellRoujiaMo(String type);
 	 - 2、由子类决定实例化的类，可以看到我们的馍是子类生成的。
 - 提供创建肉夹馍店抽象方法：[RoujiaMoStore.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/gcff/RoujiaMoStore.java)
 - 具体实现抽象方法：[XianRoujiaMoStore.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/gcff/XianRoujiaMoStore.java)
 - 分店依旧使用简单工厂模式：[XianSimpleRoujiaMoFactory.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/gcff/XianSimpleRoujiaMoFactory.java)

- 4、抽象工厂模式（使用官方提供的原料）
	 - 定义：提供一个接口，用于创建相关的或依赖对象的家族，而不需要明确指定具体类。
	 - 对比定义：
	 	- 1、提供一个接口：public interface RouJiaMoYLFactroy
	 	- 2、用于创建相关的或依赖对象的家族 public Meat createMeat();public YuanLiao createYuanliao();我们接口用于创建一系列的原材料。
	 - 创建用于提供原料的接口工厂：[RoujiaMoYLFactory.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/cxgc/RoujiaMoYLFactory.java)
	 - 各自分店实现接口，完成原料提供：[XianRoujiaMoYLFoctory.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/cxgc/XianRoujiaMoYLFoctory.java)
	 - 准备时，使用官方的原料：[RoujiaMo.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/factory/cxgc/RoujiaMo.java)

--
####3. 单例设计模式
 >  单例模式主要是为了避免因为创建了多个实例造成资源的浪费，且多个实例由于多次调用容易导致结果出现错误，而**使用单例模式能够保证整个应用中有且只有一个实例**。
 
 - 定义：只需要三步就可以保证对象的唯一性
   - (1) 不允许其他程序用new对象
   - (2) 在该类中创建对象
   - (3) 对外提供一个可以让其他程序获取该对象的方法
 - 对比定义：
  - (1) 私有化该类的构造函数
  - (2) 通过new在本类中创建一个本类对象
  - (3) 定义一个公有的方法，将在该类中所创建的对象返回

- 饿汉式[可用]：[SingletonEHan.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/singleton/ehan/SingletonEHan.java)
- 含懒汉式[双重校验锁 推荐用]：[SingletonLanHan.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/singleton/lanhan/SingletonLanHan.java)

  ```java
 private SingletonLanHan() {}
 private static SingletonLanHan singletonLanHanFour;
 public static SingletonLanHan getSingletonLanHanFour() {
	    if (singletonLanHanFour == null) {
	        synchronized (SingletonLanHan.class) {
	            if (singletonLanHanFour == null) {
	                singletonLanHanFour = new SingletonLanHan();
	            }
	        }
	    }
	    return singletonLanHanFour;
}
    
 ```
 
- 内部类[推荐用]：[SingletonIn.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/singleton/inclass/SingletonIn.java)
- 枚举[推荐用]：[SingletonEnum.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/singleton/enums/SingletonEnum.java)
 
--

####4. 策略模式
> 策略模式：定义了算法族，分别封装起来，让它们之间可相互替换，此模式让算法的变化独立于使用算法的客户。

 - 以创建游戏角色为例子：
 	 - 最初的游戏角色的父类：[Role.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/strategy/old/Role.java)
 	 - 发现有重复代码后，重构后的父类：[Role.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/strategy/better/Role.java)
 - 总结：
	 - 1、封装变化（把可能变化的代码封装起来）
	 - 2、多用组合，少用继承（我们使用组合的方式，为客户设置了算法）
	 - 3、针对接口编程，不针对实现（对于Role类的设计完全的针对角色，和技能的实现没有关系）
 - 最后测试：创建角色：
 
 ```java
 RoleA roleA = new RoleA("---A");
 roleA.setiDisplayBehavior(new DisplayYZ())
       .setiAttackBehavior(new AttackXL())
       .setiDefendBehavior(new DefendTMS())
       .setiRunBehavior(new RunJCTQ());
 roleA.display();// 样子
 roleA.attack();// 攻击
 roleA.run();// 逃跑
 roleA.defend();// 防御
 ```

--
####5. 适配器模式
> 定义：将一个类的接口转换成客户期望的另一个接口，适配器让原本接口不兼容的类可以相互合作。这个定义还好，说适配器的功能就是把一个接口转成另一个接口。

 - 以充电器为实例: 手机充电器一般都是5V左右吧，咱天朝的家用交流电压220V，所以手机充电需要一个适配器（降压器）
 - 一部手机: [Mobile.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/adapter/Mobile.java)
 - 手机依赖一个提供5V电压的接口: [V5Power.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/adapter/V5Power.java)
 - 我们拥有的是220V家用交流电: [V220Power.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/adapter/V200Power.java)
 - **适配器，完成220V转5V的作用**：[V5PowerAdapter.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/adapter/V5PowerAdapter.java)
 - 最后测试：给手机冲个电：
 	
 	```java
 	Mobile mobile = new Mobile();
   V5Power v5Power = new V5PowerAdapter(new V200Power());
   mobile.inputPower(v5Power);
 	```

--
####6. 命令模式
> 定义：将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。(简化: 将请求封装成对象，将动作请求者和动作执行者解耦。)

 - 需求：最近智能家电很火热，假设现在有电视、电脑、电灯等家电，现在需要你做个遥控器控制所有家电的开关，要求做到每个按钮对应的功能供用户个性化，对于新买入家电要有非常强的扩展性。
 - 1、家电的API：[Door.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/Door.java)
 - 2、把命令封装成类： 
 	- 统一的命令接口：[Command.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/Command.java)
 	- 家电实现该接口：[DoorOpenCommand.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/DoorOpenCommand.java)
 - 3、遥控器：[ControlPanel.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/ControlPanel.java)
 - 4、定义一个命令，可以干一系列的事情：[QuickCommand.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/QuickCommand.java)
  
  ```java
  QuickCommand quickCloseCommand = new QuickCommand(new Command[]{new LightOffCommand(light), new ComputerOffCommand(computer), new DoorCloseCommand(door)});
  controlPanel.setCommands(6, quickOpenCommand);
  controlPanel.keyPressed(6);
  ```
  
 - 5、遥控器面板执行：[CommandActivity.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/command/CommandActivity.java)
 
 ```java
 controlPanel.setCommands(0, new DoorOpenCommand(door));// 开门
 controlPanel.keyPressed(0);
 ```

--

####7. 装饰者模式
> 装饰者模式：若要扩展功能，装饰者提供了比集成更有弹性的替代方案，动态地将责任附加到对象上。

 - 先简单描述下装饰者模式发挥作用的地方，当我们设计好了一个类，我们需要给这个类添加一些辅助的功能，并且不希望改变这个类的代码，这时候就是装饰者模式大展雄威的时候了。这里还体现了一个**原则：类应该对扩展开放，对修改关闭。**
 
 - 需求：设计游戏的装备系统，基本要求，要可以计算出每种装备在镶嵌了各种宝石后的攻击力和描述：
 - 1、装备的超类：[IEquip.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/decorator/IEquip.java)
 - 2、各个装备的实现类：
   - eg：**武器**的实现类: [ArmEquip.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/decorator/equip/ArmEquip.java)
- 3、装饰品的超类（装饰品也属于装备）：[IEquipDecorator.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/decorator/gem/IEuipDecotator.java)
- 4、装饰品的实现类：
  - eg：**蓝宝石**的实现类(可累加): [BlueGemDecorator.java](https://github.com/youlookwhat/DesignPattern/blob/master/app/src/main/java/com/example/jingbin/designpattern/decorator/gem/BlueGemDecotator.java) 
- 5、最后测试：计算攻击力和查看描述：

	```java
	Log.e("---", "一个镶嵌2颗红宝石,1颗蓝宝石的靴子: ");
    IEquip iEquip = new RedGemDecotator(new RedGemDecotator(new BlueGemDecotator(new ShoeEquip())));
    Log.e("---", "攻击力:" + iEquip.caculateAttack());
    Log.e("---", "描述语:" + iEquip.description());
	```

---

###四. Thanks
- [CSDN：张鸿洋](http://blog.csdn.net/lmj623565791)
- [CSDN：dmk877](http://blog.csdn.net/dmk877/article/details/50311791)