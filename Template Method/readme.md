# JS    --模板方法模式
## 模板方法模式的定义和组成

    定义：模板方法模式是一种只需使用继承就可以实现的非常简单的模式。
    
    组成：模板方法模式由两部分结构组成，第一部分是抽象父类，第二部分是具体的实现子类。通常在抽象父类中封装了子类的算法框架，包括
    实现一些公共方法以及封装子类中所有方法的执行顺序。子类通过继承这个抽象类，也继承了整个算法结构，并且可以选择重写父类的方法。
    
## 举个例子————Coffee or Tea
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
    
### 思考时间到
	通过泡茶和泡咖啡，我们可以发现这两个冲泡步骤是大同小异的，它们的不同点在于：
    原料不同，泡的方式不同，加入的调料不同。
    经过抽象之后，我们可以发现它们的共同点可以整理如下：
    （1）把水煮沸
    （2）用沸水冲泡饮料
    （3）把饮料倒进杯子
    （4）加调料
    至此，我们可以开启一种新的冲泡方式来得到咖啡喝茶。
	首先，我们来创建一个抽象父类来表示泡一杯饮料的整个过程。代码如下：
	
	 var Beverage = function () {}
     Beverage.prototype.boilWater = function() {
       console.log('把水煮沸');
     }
     Beverage.prototype.brew = function () {}
     Beverage.prototype.pourInCup = function () {}
     Beverage.prototype.addCondiments = function () {}
     Beverage.prototype.init = function () {
       this.boilWater();
       this.brew();
       this.pourInCup();
       this.addCondiments();
     }
	 
	接下来创建我们的具体子类Coffee子类和Tea子类，代码分别如下：
	
```javascript
	//泡咖啡
	var Coffee = function() {}
    Coffee.prototype = new Beverage();
    
    Coffee.prototype.brew = function() {
      console.log('用沸水冲泡咖啡');
    }
    
    Coffee.prototype.pourInCup = function() {
      console.log('把咖啡倒进杯子');
    }
    
    Coffee.prototype.addCondiments = function () {
      console.log('加糖和牛奶');
    }
    
    var coffee = new Coffee();
    coffee.init();
```
```javascript
	//泡茶
    var Tea = function() {}
    Tea.prototype = new Beverage();
    
    Tea.prototype.brew = function() {
      console.log('用沸水浸泡茶叶');
    }
    
    Tea.prototype.pourInCup = function() {
      console.log('把茶水倒进杯子');
    }
    
    Tea.prototype.addCondiments = function () {
      console.log('加柠檬');
    }
    
    var tea = new Tea();
    tea.init();
```
	
	这样，就得到了我们的咖啡和茶。
    
## 抽象类
    模板方法模式是一种严重依赖抽象类的设计模式。
	JS抽象类的概念可以参考[Java抽象类](http://www.runoob.com/java/java-abstraction.html)
    抽象类的主要作用就是为它的子类定义公共接口，在上面的例子中Bevarage类的init方法里规定了冲泡一杯饮料的顺序如下：
```javascript
     this.boilWater();
     this.brew();
     this.pourInCup();
     this.addCondiments();
```

	如果在Coffee子类中没有实现对应的brew方法，那么我们百分百得不到一杯咖啡。父类规定了子类的方法和这些方法执行的顺序，
	子类就应该拥有这些方法，并且提供正确的实现。
    
## “继承”或许可以被取代
	模板方法模式是为数不多的基于继承的设计模式，但JavaScript语言实际上没有提供真正的类式继承，继承是通过对象与对象之间的委托来实现的。
	在好莱坞原则的指导之下，下面的代码可以达到和继承一样的效果。
```javascript
    var Beverage = function(param) {
      // 局部变量
      var boilWater = function () {
        console.log('把水煮沸');
      }
      var brew = param.brew || function() {
        throw new Error('必须传递brew方法');
      }
      var pourInCup = param.pourInCup || function () {
        throw new Error('必须传递pourInCup方法');
      }
      var addCondiments = param.addCondiments || function () {
        throw new Error('必须传递addCondiments方法');
      }

      // F 可以称之为代号
      var F = function() {}
      F.prototype.init = function() {
        boilWater();
        brew();
        pourInCup();
        addCondiments();
      }
      return F;
    }

    var Coffee = Beverage({
      brew: function() {
        console.log('用沸水泡咖啡');
      },
      pourInCup: function () {
        console.log('把咖啡倒进杯子');
      },
      addCondiments: function () {
        console.log('加糖和牛奶');
      }
    })
    
      var Tea = Beverage({
      brew: function() {
        console.log('用沸水浸泡茶叶');
      },
      pourInCup: function () {
        console.log('把茶倒进杯子');
      },
      addCondiments: function () {
        console.log('加柠檬');
      }
    })

    var coffee = new Coffee();
    coffee.init();
    
    var tea = new Tea();
    tea.init();
```
    这段代码中，我们把brew、pourInCup、addCondiments这些方法一次传入Beverage函数，Bevarage函数被调用之后返回构造器F，
	F类中包含了“模板方法”F.prototype.init,跟继承得到的效果一样。
    
