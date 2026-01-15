# Java Design Patterns

## Singleton Pattern
```java
public class DatabaseConnection {
    private static volatile DatabaseConnection instance;
    
    private DatabaseConnection() {}
    
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            synchronized (DatabaseConnection.class) {
                if (instance == null) {
                    instance = new DatabaseConnection();
                }
            }
        }
        return instance;
    }
}
```

## Factory Pattern
```java
public interface Vehicle {
    void drive();
}

public class Car implements Vehicle {
    @Override
    public void drive() {
        System.out.println("Driving a car");
    }
}

public class VehicleFactory {
    public static Vehicle createVehicle(String type) {
        switch (type.toLowerCase()) {
            case "car": return new Car();
            case "truck": return new Truck();
            default: throw new IllegalArgumentException("Unknown vehicle type");
        }
    }
}
```

## Observer Pattern
```java
public interface Observer {
    void update(String message);
}

public class EmailNotification implements Observer {
    @Override
    public void update(String message) {
        System.out.println("Email: " + message);
    }
}

public class NewsAgency {
    private List<Observer> observers = new ArrayList<>();
    
    public void addObserver(Observer observer) {
        observers.add(observer);
    }
    
    public void notifyObservers(String news) {
        observers.forEach(observer -> observer.update(news));
    }
}
```