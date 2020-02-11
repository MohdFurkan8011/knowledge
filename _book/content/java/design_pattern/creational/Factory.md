# Factory

What is the most usual method of creating an instance of a class in java? Most people will answer this question: “*using new keyword*“. Well, it is considered old-fashioned now. Let’s see how??

If object creation code is spread in the whole application, and if you need to change the process of object creation then you need to go in each and every place to make necessary changes. After finishing this article, while writing your application, consider using the **Java factory pattern**.

```java
public class CarFactory {
    
    public static Car buildCar(CarType model) {
        Car car = null;
        switch (model) {
        case SMALL:
            car = new SmallCar();
            break;
 
        case SEDAN:
            car = new SedanCar();
            break;
 
        case LUXURY:
            car = new LuxuryCar();
            break;
 
        default:
            // throw some exception
            break;
        }
        return car;
    }
    
}
```

