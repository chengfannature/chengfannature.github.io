---
layout: post
title: Java Builder 模式
---
Builder设计模式是JAVA的一种创造设计模式，例如用来构造对象，类似工厂模式。
每一种设计模式都是为了解决某种问题，一般都是比较复杂的问题，引入设计模式后可以使得架构上更分明、结构上更简单。先来看下Builder模式能解决什么问题。

##在JAVA编程中，Builder模式能解决什么问题？
前面提到Builer模式是一种跟实例化对象相关的设计模式。一般情况下我们使用构造函数来实例化对象。通常构造函数会有一些参数。考虑一下这种情况，构造函数的参数很多，有一些是必须的，有一些是可选的，这样在实例化的时候构造函数会显得很臃肿。
举个例子。有个做蛋糕的类，做蛋糕需要鸡蛋、牛奶、面粉。同样的，做蛋糕的时候也是有些是必选材料，有些是可选材料，如樱桃、草莓等等。如果我们想为不同种类的蛋糕重载构造函数，那么会出现很多种类型的构造函数，再加上如果参数很多，那更是不堪设想。
总结而言，Builder模式是为了解决以下两类问题：

 1. 构造函数的参数很多；
 2. 容易出错。因为很多参数的属性是类似的，比如糖和黄油都可以用勺来衡量，本来你应该给两勺糖，结果给了两勺黄油，编译器不会报错，单结果是做出来的是个差不多没有糖的黄油蛋糕。
这些问题都可以用Builder设计模式来解决。Builder设计模式不仅可以提升可读性，还可以通过一步步明确地加调料直到完全构造好再实例化对象来减少出现错误的机率。

##例子
还是用上面做蛋糕的例子来描述如何使用Builder设计模式。这里用了一个静态内部类来创建对象。

Builder设计模式的步骤：

 1. 在需要被创建对象的类里面创建一个名为Builder的内部静态类；
 2. Builder类有原始类的所有属性；
 3. Builder类需要暴露添加属性的方法，每个方法都返回相同的Builder对象。Buidler在每次调用后获得增强。
 4. Builder.build()方法会拷贝所有的builder 属性值到实际的类中，并返回该类的实例。
 5. 外部类必须有一个private的构造函数用来给build()方法创建实例，并隔离外部调用。

~~~java
public class BuilderPatternExample {
  
    public static void main(String args[]) {
      
        //Creating object using Builder pattern in java
        Cake whiteCake = new Cake.Builder()
				.sugar(1).butter(0.5)
				.eggs(2).vanila(2)
				.flour(1.5). bakingpowder(0.75)
				.milk(0.5).build();
      
        //Cake is ready to eat :)
        System.out.println(whiteCake);
    }
}

class Cake {

    private final double sugar;   //cup
    private final double butter;  //cup
    private final int eggs;
    private final int vanila;     //spoon
    private final double flour;   //cup
    private final double bakingpowder; //spoon
    private final double milk;  //cup
    private final int cherry;

    public static class Builder {

        private double sugar;   //cup
        private double butter;  //cup
        private int eggs;
        private int vanila;     //spoon
        private double flour;   //cup
        private double bakingpowder; //spoon
        private double milk;  //cup
        private int cherry;

        //builder methods for setting property
        public Builder sugar(double cup)
		{this.sugar = cup; return this; }
	
        public Builder butter(double cup)
		{this.butter = cup; return this; }

        public Builder eggs(int number)
		{this.eggs = number; return this; }

        public Builder vanila(int spoon)
		{this.vanila = spoon; return this; }

        public Builder flour(double cup)
		{this.flour = cup; return this; }

        public Builder bakingpowder(double spoon)
		{this.sugar = spoon; return this; }

        public Builder milk(double cup)
		{this.milk = cup; return this; }

        public Builder cherry(int number)
		{this.cherry = number; return this; }
      
      
        //return fully build object
        public Cake build() {
            return new Cake(this);
        }
    }

    //private constructor to enforce object 
    //creation through builder
    private Cake(Builder builder) {
        this.sugar = builder.sugar;
        this.butter = builder.butter;
        this.eggs = builder.eggs;
        this.vanila = builder.vanila;
        this.flour = builder.flour;
        this.bakingpowder = builder.bakingpowder;
        this.milk = builder.milk;
        this.cherry = builder.cherry;       
    }

    @Override
    public String toString() {
        return "Cake{" + "sugar=" + sugar + ", butter=" + butter + 
	", eggs=" + eggs + ", vanila=" + vanila + ", flour=" + flour + 
	", bakingpowder=" + bakingpowder + ", milk=" + milk + 
	", cherry=" + cherry + '}';

    } 
  
}
~~~

OupPut：

    Cake{sugar=0.75, butter=0.5, eggs=2, vanila=2, flour=1.5, bakingpowder=0.0, milk=0.5, cherry=0}

##Builder设计模式的优缺点
优点：

 1. 如果参数超过四到五个，使用Builder模式更易于维护；
 2. 不易于出现参数传递错误，因为每个参数传递都是通过显示的方法调用完成的；
 3. 更加健壮，因为只有一个全构造的对象向客户端体现。

缺点：

 代码累赘和重复和明显，看了上面的例子可以知道，因为需要在外部类里面新建一个参数完全一样的Builder类出来；

##Builder设计模式和Factory设计模式的区别
虽然都是用来实例化对象的设计模式，但是二者有明显的区别。factory设计模式可以构造实现某个接口的不同实现类，而Builder模式构造的始终只有外部类一种类

