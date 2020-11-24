# 设计模式笔记

1、评价代码的维度

- 可维护性：代码易维护，在不破坏原有代码设计、不引入新的 bug 的情况下，能够快速地修改或者添加代码。

- 可读性：我们需要看代码是否符合编码规范、命名是否达意、注释是否详尽、函数是否长短合适、模块划分是否清晰、是否符合高内聚低耦合等等。

- 可扩展性：我们在不修改或少量修改原有代码的情况下，通过扩展的方式添加新的功能代码。

- 灵活性：代码易扩展，代码易复用，代码易用（满足多种场景）

- 简洁性：KISS原则（Keep It Simple，Stupid），代码简单、逻辑清晰

- 可复用性：尽量减少重复代码的编写，复用已有的代码。多态、继承，单一职责原则，解耦、高内聚、模块化。DRY原则（Don’t Repeat Yourself）

- 可测试性

  ![](https://github.com/ochadesuka/Design-pattern/blob/main/f3262ef8152517d3b11bfc3f2d2b12d3.png)

2、面向对象

- 面向对象编程是一种编程范式或编程风格。它以类或对象作为组织代码的基本单元，并将封装、抽象、继承、多态四个特性，作为代码设计和实现的基石 。

面向对象编程语言是支持类或对象的语法机制，并有现成的语法机制，能方便地实现面向对象编程四大特性（封装、抽象、继承、多态）的编程语言。

面向对象分析（OOA）、面向对象设计（OOD）

- UML（Unified Model Language），统一建模语言

- 封装

信息隐藏或者数据访问保护。类通过暴露有限的访问接口，授权外部仅能通过类提供的方式（或者叫函数）来访问内部信息或者数据。

- 抽象

隐藏方法的具体实现，让调用者只需要关心方法提供了哪些功能，并不需要知道这些功能是如何实现的。

- 继承

表示类之间的 is-a 关系，比如猫是一种哺乳动物。从继承关系上来讲，继承可以分为两种模式，单继承和多继承。

好处：代码复用

- 多态

子类可以替换父类 ，包含重写和重载、接口类、duck-typing等

duck-typing：只要两个类具有相同的方法，就可以实现多态，并不要求两个类之间有任何关系，一般在动态语言中。

提高了代码的可扩展性和复用性

java不支持多继承的原因：菱形继承：假设类 B 和类 C 继承自类 A，且都重写了类 A 中的同一个方法，而类 D 同时继承了类 B 和类 C，那么此时类 D 会继承 B、C 的方法，那对于 B、C 重写的 A 中的方法，类 D 会继承哪一个呢？这里就会产生歧义。

- 面向过程编程

以过程（可以理解为方法、函数、操作）作为组织代码的基本单元，以数据（可以理解为成员变量、属性）与方法相分离为最主要的特点。面向过程风格是一种流程化的编程风格，通过拼接一组顺序执行的方法来操作数据完成一项功能。

- 面向对象编程的优势

对于大规模复杂程序的开发，程序的处理流程并非单一的一条主线，而是错综复杂的网状结构。面向对象编程比起面向过程编程，更能应对这种复杂类型的程序开发。面

向对象编程相比面向过程编程，具有更加丰富的特性（封装、抽象、继承、多态）。利用这些特性编写出来的代码，更加易扩展、易复用、易维护。

从编程语言跟机器打交道的方式的演进规律中，我们可以总结出：面向对象编程语言比起面向过程编程语言，更加人性化、更加高级、更加智能。

- 看似面向对象、实则面向过程

\1. 滥用 getter、setter 方法：不管三七二十一给类中所有属性都定义getter和setter方法，其实访问控制是无效的（属性一般为private），这样做实际是面向过程编程。

在设计实现类的时候，除非真的需要，否则，尽量不要给属性定义 setter 方法。除此之外，尽管 getter 方法相对 setter 方法要安全些，但是如果返回的是集合容器（比如例子中的 List 容器），也要防范集合内部数据被修改的危险。

在用getter获取集合时可以使用Collections.unmodifiableList防止数据被修改。

\2. 滥用全局变量和全局方法

常用的全局变量：单例类对象、静态成员变量、常量。

例：通常在项目中会将项目所用到的所有常量放在一个Contants类中，这样设计有以下的缺点：1）增加编译时间、降低开发效率，开发者都向这个类中添加常量，长期下来，常量会越来越多，实际我们需要使用的只有一小部分，但是每次单元测试或者打包都需要完整编译整个文件。2）影响代码复用性

改进思路：1）Contants类按照不同功能和用途进行拆解，比如Mysql相关的分为一个类，redis相关的分为一个类；2）将常量定义在类中，mysql配置类中定义mysql相关常量，redis配置类中定义redis相关常量。

例：Utils类，通常我们都会定义一些工具类来减少重复代码，Utils类中的方法是静态的，并不符合面向对象编程的思想，但是它能让我们的代码更简洁清晰，所以面向过程编程的代码也不全是不好的。Utils类也要注重功能细化。

\3. 基于贫血模型的开发模式

典型的MVC模式其实是面向过程的，它将数据和方法分离了，但是它也十分流行。

面向过程编程语言可以写出面向对象编程的代码，面向对象编程语言也可以写出面向过程编程的代码。

- 抽象类和接口的区别

抽象类：抽象类不允许被实例化，只能被继承。抽象类可以包含属性和方法。方法既可以包含代码实现，也可以不包含代码实现。不包含代码实现的方法叫作抽象方法。子类继承抽象类，必须实现抽象类中的所有抽象方法。

接口：接口不能包含属性（也就是成员变量）。接口只能声明方法，方法不能包含代码实现。类实现接口的时候，必须实现接口中声明的所有方法。

- 如何决定该用抽象类还是接口？

如果我们要表示一种 is-a 的关系，并且是为了解决代码复用的问题，我们就用抽象类；如果我们要表示一种 has-a 关系，并且是为了解决抽象而非代码复用的问题，那我们就可以使用接口。

- 如何用普通类模拟接口

1、接口不能被实例化，构造函数设为private

2、接口方法必须实现，让普通类方法抛出MethodUnSupportedException 异常

- 基于接口而非实现编程

“基于接口而非实现编程”这条原则的另一个表述方式，是“基于抽象而非实现编程”。后者的表述方式其实更能体现这条原则的设计初衷。在软件开发中，最大的挑战之一就是需求的不断变化，这也是考验代码设计好坏的一个标准。越抽象、越顶层、越脱离具体某一实现的设计，越能提高代码的灵活性，越能应对未来的需求变化。好的代码设计，不仅能应对当下的需求，而且在将来需求发生变化的时候，仍然能够在不破坏原有代码设计的情况下灵活应对。而抽象就是提高代码扩展性、灵活性、可维护性最有效的手段之一。

实现规则：

1、函数的命名不能暴露任何实现细节

2、封装具体的实现细节。

3、为实现类定义抽象的接口。具体的实现类都依赖统一的接口定义，遵从一致的功能协议。使用者依赖接口，而不是具体的实现类来编程。

- 是否需要为每个类定义接口？

否，从这个设计初衷上来看，如果在我们的业务场景中，某个功能只有一种实现方式，未来也不可能被其他实现方式替换，那我们就没有必要为其设计接口。

- 多用组合少用继承

少用继承的原因：继承层次过深、继承关系过于复杂会影响到代码的可读性和可维护性。

采用接口时，接口实现类中可能会有代码重复的情况，同样的逻辑需要在所有类中都实现一遍，这时候需要用到委托模式。

例：普通接口实现设计：

```
public interface Flyable {
  void fly();
}
public interface Tweetable {
  void tweet();
}
public interface EggLayable {
  void layEgg();
}
public class Ostrich implements Tweetable, EggLayable {//鸵鸟
  //... 省略其他属性和方法...
  @Override
  public void tweet() { //... }
  @Override
  public void layEgg() { //... }
}
public class Sparrow impelents Flayable, Tweetable, EggLayable {//麻雀
  //... 省略其他属性和方法...
  @Override
  public void fly() { //... }
  @Override
  public void tweet() { //... }
  @Override
  public void layEgg() { //... }
}
```

在Ostrich类和Sparrow类中都需要重复实现tweet()和layEgg()方法，可以单独针对Tweetable和EggLayable接口单数实现两个类，在Ostrich类和Sparrow类中去调用这两个类的方法（组合+委托）

```
public interface Flyable {
  void fly()；
}
public class FlyAbility implements Flyable {
  @Override
  public void fly() { //... }
}
//省略Tweetable/TweetAbility/EggLayable/EggLayAbility

public class Ostrich implements Tweetable, EggLayable {//鸵鸟
  private TweetAbility tweetAbility = new TweetAbility(); //组合
  private EggLayAbility eggLayAbility = new EggLayAbility(); //组合
  //... 省略其他属性和方法...
  @Override
  public void tweet() {
    tweetAbility.tweet(); // 委托
  }
  @Override
  public void layEgg() {
    eggLayAbility.layEgg(); // 委托
  }
}
```

- 如何判断该用组合还是继承？

继承改写成组合意味着要做更细粒度的类的拆分。这也就意味着，我们要定义更多的类和接口。类和接口的增多也就或多或少地增加代码的复杂程度和维护成本。所以，在实际的项目开发中，我们还是要根据具体的情况，来具体选择该用继承还是组合。

如果类之间的继承结构稳定（不会轻易改变），继承层次比较浅（比如，最多有两层继承关系），继承关系不复杂，我们就可以大胆地使用继承。反之，系统越不稳定，继承层次很深，继承关系复杂，我们就尽量使用组合来替代继承。

- 贫血模型与充血模型

贫血模型（Anemic Domain Model）：类似于Entity、BO、VO这种只包含数据不包含逻辑的类，是面向过程编程风格的。

充血模型（Rich Domain Model）：数据和逻辑封装于一个类中，面向对象编程风格。

领域驱动设计（Domain Driven Design）：主要是用来指导如何解耦业务系统，划分业务模块，定义业务领域模型及其交互

- 基于贫血模型的传统开发模式流行原因

业务系统比较简单，充血模型设计复杂难度大，思维固化、转型有成本

- 什么时候需要用到基于充血模型的DDD开发模式

基于充血模型的 DDD 开发模式的开发流程，在应对复杂业务系统的开发的时候更加有优势。在这种开发模式下，我们需要事先理清楚所有的业务，定义领域模型所包含的属性和方法。领域模型相当于可复用的业务中间层。新功能需求的开发，都基于之前定义好的这些领域模型来完成。

- 贫血模型和充血模型的区别（例）

基于充血模型的 DDD 开发模式跟基于贫血模型的传统开发模式相比，主要区别在 Service 层。在基于充血模型的开发模式下，我们将部分原来在 Service 类中的业务逻辑移动到了一个充血的 Domain 领域模型中，让 Service 类的实现依赖这个 Domain 类。

贫血模型：

```
public class VirtualWalletBo {//省略getter/setter/constructor方法
  private Long id;
  private Long createTime;
  private BigDecimal balance;
}

public class VirtualWalletService {
  // 通过构造函数或者IOC框架注入
  private VirtualWalletRepository walletRepo;
  private VirtualWalletTransactionRepository transactionRepo;
  
  public VirtualWalletBo getVirtualWallet(Long walletId) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWalletBo walletBo = convert(walletEntity);
    return walletBo;
  }
  
  public BigDecimal getBalance(Long walletId) {
    return walletRepo.getBalance(walletId);
  }
  
  public void debit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    BigDecimal balance = walletEntity.getBalance();
    if (balance.compareTo(amount) < 0) {
      throw new NoSufficientBalanceException(...);
    }
    walletRepo.updateBalance(walletId, balance.subtract(amount));
  }
  
  public void credit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    BigDecimal balance = walletEntity.getBalance();
    walletRepo.updateBalance(walletId, balance.add(amount));
  }
  
  public void transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) {
    VirtualWalletTransactionEntity transactionEntity = new VirtualWalletTransactionEntity();
    transactionEntity.setAmount(amount);
    transactionEntity.setCreateTime(System.currentTimeMillis());
    transactionEntity.setFromWalletId(fromWalletId);
    transactionEntity.setToWalletId(toWalletId);
    transactionEntity.setStatus(Status.TO_BE_EXECUTED);
    Long transactionId = transactionRepo.saveTransaction(transactionEntity);
    try {
      debit(fromWalletId, amount);
      credit(toWalletId, amount);
    } catch (InsufficientBalanceException e) {
      transactionRepo.updateStatus(transactionId, Status.CLOSED);
      ...rethrow exception e...
    } catch (Exception e) {
      transactionRepo.updateStatus(transactionId, Status.FAILED);
      ...rethrow exception e...
    }
    transactionRepo.updateStatus(transactionId, Status.EXECUTED);
  }
}
```

充血模型：

```
public class VirtualWallet { // Domain领域模型(充血模型)
  private Long id;
  private Long createTime = System.currentTimeMillis();;
  private BigDecimal balance = BigDecimal.ZERO;
  
  public VirtualWallet(Long preAllocatedId) {
    this.id = preAllocatedId;
  }
  
  public BigDecimal balance() {
    return this.balance;
  }
  
  public void debit(BigDecimal amount) {
    if (this.balance.compareTo(amount) < 0) {
      throw new InsufficientBalanceException(...);
    }
    this.balance.subtract(amount);
  }
  
  public void credit(BigDecimal amount) {
    if (amount.compareTo(BigDecimal.ZERO) < 0) {
      throw new InvalidAmountException(...);
    }
    this.balance.add(amount);
  }
}

public class VirtualWalletService {
  // 通过构造函数或者IOC框架注入
  private VirtualWalletRepository walletRepo;
  private VirtualWalletTransactionRepository transactionRepo;
  
  public VirtualWallet getVirtualWallet(Long walletId) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    return wallet;
  }
  
  public BigDecimal getBalance(Long walletId) {
    return walletRepo.getBalance(walletId);
  }
  
  public void debit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    wallet.debit(amount);
    walletRepo.updateBalance(walletId, wallet.balance());
  }
  
  public void credit(Long walletId, BigDecimal amount) {
    VirtualWalletEntity walletEntity = walletRepo.getWalletEntity(walletId);
    VirtualWallet wallet = convert(walletEntity);
    wallet.credit(amount);
    walletRepo.updateBalance(walletId, wallet.balance());
  }
  
  public void transfer(Long fromWalletId, Long toWalletId, BigDecimal amount) {
    //...跟基于贫血模型的传统开发模式的代码一样...
  }
}
```

- 充血模型中service的职责

1.Service 类负责与 Repository 交流，保持领域模型的独立性，不与任何其他层的代码（Repository 层的代码）或开发框架（比如 Spring、MyBatis）耦合在一起，将流程性的代码逻辑（比如从 DB 中取数据、映射数据）与领域模型的业务逻辑解耦，让领域模型更加可复用。

2.Service 类负责跨领域模型的业务聚合功能

3.Service 类负责一些非功能性及与三方系统交互的工作

- 如何对鉴权需求做面向对象分析

基础需求分析-分析优化-分析优化...-确定需求

- 如何进行面向对象设计

划分职责进而识别出有哪些类；

定义类及其属性和方法；

定义类与类之间的交互关系；

将类组装起来并提供执行入口。

结合上面的设计规则实现鉴权（实战）

- 设计原则

SOLID（单一职责原则、开闭原则、里式替换原则、接口隔离原则和依赖反转原则）

- 单一职责原则SRP：Single Responsibility Principle，一个类或者模块只负责完成一个职责（或者功能）。

如何判定职责是否单一：

类中的代码行数、函数或者属性过多；

类依赖的其他类过多，或者依赖类的其他类过多；

私有方法过多；

比较难给类起一个合适的名字；

类中大量的方法都是集中操作类中的某几个属性。

类的职责是否设计得越单一越好？：否，标准是看代码的可维护性

- 开闭原则OCP：Open Closed Principle，软件实体（模块、类、方法等）应该“对扩展开放、对修改关闭”。

”修改“代码：

```
public class Alert {
  private AlertRule rule;
  private Notification notification;

  public Alert(AlertRule rule, Notification notification) {
    this.rule = rule;
    this.notification = notification;
  }

  public void check(String api, long requestCount, long errorCount, long durationOfSeconds) {
    long tps = requestCount / durationOfSeconds;
    if (tps > rule.getMatchedRule(api).getMaxTps()) {
      notification.notify(NotificationEmergencyLevel.URGENCY, "...");
    }
    if (errorCount > rule.getMatchedRule(api).getMaxErrorCount()) {
      notification.notify(NotificationEmergencyLevel.SEVERE, "...");
    }
  }
}
```

当要添加新告警规则时，必须要修改check方法，需要添加参数或者增加if逻辑

“扩展”代码：

```
public class Alert {
  private List<AlertHandler> alertHandlers = new ArrayList<>();
  
  public void addAlertHandler(AlertHandler alertHandler) {
    this.alertHandlers.add(alertHandler);
  }

  public void check(ApiStatInfo apiStatInfo) {
    for (AlertHandler handler : alertHandlers) {
      handler.check(apiStatInfo);
    }
  }
}

public class ApiStatInfo {//省略constructor/getter/setter方法
  private String api;
  private long requestCount;
  private long errorCount;
  private long durationOfSeconds;
}

public abstract class AlertHandler {
  protected AlertRule rule;
  protected Notification notification;
  public AlertHandler(AlertRule rule, Notification notification) {
    this.rule = rule;
    this.notification = notification;
  }
  public abstract void check(ApiStatInfo apiStatInfo);
}

public class TpsAlertHandler extends AlertHandler {
  public TpsAlertHandler(AlertRule rule, Notification notification) {
    super(rule, notification);
  }

  @Override
  public void check(ApiStatInfo apiStatInfo) {
    long tps = apiStatInfo.getRequestCount()/ apiStatInfo.getDurationOfSeconds();
    if (tps > rule.getMatchedRule(apiStatInfo.getApi()).getMaxTps()) {
      notification.notify(NotificationEmergencyLevel.URGENCY, "...");
    }
  }
}

public class ErrorAlertHandler extends AlertHandler {
  public ErrorAlertHandler(AlertRule rule, Notification notification){
    super(rule, notification);
  }

  @Override
  public void check(ApiStatInfo apiStatInfo) {
    if (apiStatInfo.getErrorCount() > rule.getMatchedRule(apiStatInfo.getApi()).getMaxErrorCount()) {
      notification.notify(NotificationEmergencyLevel.SEVERE, "...");
    }
  }
}
```

“扩展”代码要增加新告警，只需要在 ApiStatInfo 类中添加新的属性，新增一个handler类。

类、模块、方法并不是完全不应该修改，扩展的意义在于尽量不改动原先的代码行，而是新增代码行。

为了尽量写出扩展性好的代码，我们要时刻具备扩展意识、抽象意识、封装意识。

开闭原则不是绝对的，比如在告警规则较少的场景下，“修改”代码可读性更好，“扩展”代码更复杂化了，而告警规则很多时，“扩展”代码反而更容易理解。写代码时要根据实际应用场景考虑，避免过渡设计。

- 里氏替换原则LSP：Liskov Substitution Principle，子类对象（object of subtype/derived class）能够替换程序（program）中父类对象（object of base/parent class）出现的任何地方，并且保证原来程序的逻辑行为（behavior）不变及正确性不被破坏。

多态和里式替换有点类似，但它们关注的角度是不一样的。多态是面向对象编程的一大特性，也是面向对象编程语言的一种语法。它是一种代码实现的思路。而里式替换是一种设计原则，是用来指导继承关系中子类该如何设计的，子类的设计要保证在替换父类的时候，不改变原有程序的逻辑以及不破坏原有程序的正确性。

- 哪些实现违背了LSP

\1. 子类违背父类声明要实现的功能，比如父类的排序接口是按金额大小排序的，子类是按时间排序的，那就违背了LSP原则。

\2. 子类违背父类对输入、输出、异常的约定

\3. 子类违背父类注释中所罗列的任何特殊说明

小窍门：拿父类的单元测试用例测试子类

- 接口隔离原则ISP：Interface Segregation Principle，

1.把“接口”理解为一组 API 接口集合，如果部分接口只被部分调用者使用，我们就需要将这部分接口隔离出来，单独给这部分调用者使用，而不强迫其他调用者也依赖这部分不会被用到的接口。

2.把“接口”理解为单个 API 接口或函数，部分调用者只需要函数中的部分功能，那我们就需要把函数拆分成粒度更细的多个函数，让调用者只依赖它需要的那个细粒度函数。

3.把“接口”理解为 OOP 中的接口，那接口的设计要尽量单一

- 控制反转IOC

框架提供了一个可扩展的代码骨架，用来组装对象、管理整个执行流程。程序员利用框架进行开发的时候，只需要往预留的扩展点上，添加跟自己业务相关的代码，就可以利用框架来驱动整个程序流程的执行。

这里的“控制”指的是对程序执行流程的控制，而“反转”指的是在没有使用框架之前，程序员自己控制整个程序的执行。在使用框架之后，整个程序的执行流程可以通过框架来控制。流程的控制权从程序员“反转”到了框架。

控制反转并不是一种具体的实现技巧，而是一个比较笼统的设计思想，一般用来指导框架层面的设计。

- 依赖注入

不通过 new() 的方式在类内部创建依赖类对象，而是将依赖的类对象在外部创建好之后，通过构造函数、函数参数等方式传递（或注入）给类使用。

- 依赖反转原则DIP

高层模块（high-level modules）不要依赖低层模块（low-level）。高层模块和低层模块应该通过抽象（abstractions）来互相依赖。除此之外，抽象（abstractions）不要依赖具体实现细节（details），具体实现细节（details）依赖抽象（abstractions）。

- KISS原则 Keep It Simple and Stupid.

保持代码可读和可维护的重要手段。代码足够简单，也就意味着很容易读懂，bug 比较难隐藏。即便出现 bug，修复起来也比较简单。

- 如何写出满足 KISS 原则的代码

不要使用同事可能不懂的技术来实现代码。

不要重复造轮子，要善于使用已经有的工具类库。

不要过度优化。不要过度使用一些奇技淫巧（比如，位运算代替算术运算、复杂的条件语句代替 if-else、使用一些过于底层的函数等）来优化代码，牺牲代码的可读性。

- YAGNI原则 You Ain’t Gonna Need It

不要去设计当前用不到的功能；不要去编写当前用不到的代码，不要做过度设计。

- DRY 原则 Don’t Repeat Yourself 不要写重复的代码。

代码重复：实现逻辑重复、功能语义重复和代码执行重复

- 怎么提高代码复用性？

减少代码耦合

满足单一职责原则

模块化

业务与非业务逻辑分离

通用代码下沉：越底层的代码越通用、会被越多的模块调用，越应该设计得足够可复用。

继承、多态、抽象、封装

应用模板等设计模式

- 高内聚：相近的功能应该放到同一个类中，不相近的功能不要放到同一个类中。
- 松耦合：类与类之间的依赖关系简单清晰。即使两个类有依赖关系，一个类的代码改动不会或者很少导致依赖类的代码改动。
- 迪米特法则LOD：