# JS    --模板方法模式
## 模板方法模式的定义和组成

    定义：模板方法模式是一种只需使用继承就可以实现的非常简单的模式。
    
    组成：模板方法模式由两部分结构组成，第一部分是抽象父类，第二部分是具体的实现子类。通常在抽象父类中封装了子类的算法框架，包括
    实现一些公共方法以及封装子类中所有方法的执行顺序。子类通过继承这个抽象类，也继承了整个算法结构，并且可以选择重写父类的方法。
    
## 第一个例子————Coffee or Tea
### 先泡一杯咖啡
    首先，如果没有什么个性化的需求，那么泡咖啡的步骤通常如下：
    （1）把水煮沸
    （2）把沸水冲泡咖啡
    （3）把咖啡倒进杯子
    （4）加糖和牛奶
    通过如下代码便能得到一杯香浓的咖啡了：
    
    var Coffee = function () {
    
    }
    Coffee.prototype.boilWater = function () {
      console.log('水煮开了');
    }
    Coffee.prototype.brewCoffeeGriends = function() {
      console.log('用沸水冲泡咖啡');
    }
    Coffee.prototype.pourInCup = function() {
      console.log('把咖啡倒进杯子');
    }
    Coffee.prototype.addSugarAndMilk = function() {
      console.log('加糖和牛奶');
    }
    Coffee.prototype.init = function() {
      this.boilWater();
      this.brewCoffeeGriends();
      this.pourInCup();
      this.addSugarAndMilk();
    }
    
    var coffee = new Coffee();
    coffee.init();
    
### 泡一壶茶
    泡茶的步骤与泡咖啡相似：
    （1）把水煮沸
    （2）用沸水浸泡茶叶
    （3）把茶水倒进杯子
    （4）加柠檬
    代码如下：
    
    class Tea {
      constructor () {}
      boilWater () {
        console.log('水煮开了');
      }
      brewTeaLeaves() {
        console.log('用沸水浸泡茶叶');
      }
      pourInCup () {
        console.log('把茶水倒进杯子');
      }
      addLemon () {
        console.log('加柠檬');
      }
      init() {
        this.boilWater();
        this.brewTeaLeaves();
        this.pourInCup();
        this.addLemon();
      }
    }
    var tea = new Tea();
    tea.init();
    
    
    
    
