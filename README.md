# EdTech-batch-mgmt-LLD

This project was created to understand the <b>Prototype design pattern</b>.


## Prototype Pattern
The prototype design pattern is a creational design pattern that allows us to create new objects by cloning existing objects. Instead of creating objects from scratch, we can make copies of an existing object, called a prototype, and modify those copies as needed.

Let's understand more via an example [later](https://github.com/TanaySriva/Prototype-LLD#prototype-design-pattern-example).

<b>Client</b> : Person that handles batches of students for an ed-tech company.
<br>
<b>What does he want to do</b> : To add new student details and assign a batch or modify existing details(like batch change).<br>
To understand more about Prototype pattern, we have two types of Students(classes) -> 1. Student(Regular) 2. Intelligent Student.<br>
Intelligent Student has an extra property -> IQ<br>
Rest all properties lie with the Student class -> Name, Age, BatchID, BatchName



### Classes Used
1. Student - This class has all the Student details.
2. IntelligentStudent - This class has an extra 'IQ' attribute.
3. Prototype - This an interface that gets implemented by Student to make sure that Student and IntelligentStudent have a copy() function that will create a clone of the object passed.
4. StudentRegistry - We wouldn't want client to create the original objects again and again and the application might need those objects at other places as well. Therefore, we have registry(like a central repository) that will hold the original objects and the client or any class can directly fetch those objects from here.
5. Client - Here the client can fetch the original objects and make copies and modifications.

### Prototype design pattern example:
Let's imagine you are building a game that involves creating different types of monsters. Each monster has various attributes like health, attack power, and special abilities. Instead of defining each monster's attributes from scratch every time you want to create a new monster, you can use the prototype design pattern.

Here's how it works:

Create a prototype object, let's say a "Monster" object, with default attribute values. This object serves as a blueprint or template for creating other monsters.

When you want to create a new monster, instead of creating it from scratch, you clone the prototype object. This creates a new instance with the same initial attribute values.

You can then modify the cloned object to customize it as needed. For example, you can change the health, attack power, or assign unique special abilities to the new monster.

By using the prototype design pattern, you avoid the overhead of creating objects from scratch and gain flexibility in creating variations of objects.

Here's an example of the prototype design pattern in Java:

```java
import java.util.ArrayList;
import java.util.List;

class Monster implements Cloneable {
    private int health;
    private int attackPower;
    private List<String> abilities;

    public Monster(int health, int attackPower, List<String> abilities) {
        this.health = health;
        this.attackPower = attackPower;
        this.abilities = abilities;
    }

    public void setHealth(int health) {
        this.health = health;
    }

    public void setAttackPower(int attackPower) {
        this.attackPower = attackPower;
    }

    public void addAbility(String ability) {
        abilities.add(ability);
    }

    public Monster clone() throws CloneNotSupportedException {
        List<String> clonedAbilities = new ArrayList<>(abilities);
        return new Monster(health, attackPower, clonedAbilities);
    }

    public void printInfo() {
        System.out.println("Health: " + health);
        System.out.println("Attack Power: " + attackPower);
        System.out.println("Abilities: " + abilities);
    }
}

public class PrototypeExample {
    public static void main(String[] args) {
        // Create a prototype monster
        Monster prototypeMonster = new Monster(100, 10, new ArrayList<>());
        prototypeMonster.addAbility("Fireball");

        try {
            // Create a new monster by cloning the prototype
            Monster newMonster = prototypeMonster.clone();
            newMonster.setHealth(150);
            newMonster.addAbility("Ice Blast");

            // Create another monster
            Monster anotherMonster = prototypeMonster.clone();
            anotherMonster.setAttackPower(15);

            // Print the attributes of the monsters
            newMonster.printInfo();
            anotherMonster.printInfo();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```
In this Java example, we have a Monster class that implements the Cloneable interface, allowing us to clone objects. The class has attributes such as health, attack power, and abilities stored in a list. The clone method creates a new Monster object by making a deep copy of the attributes.

In the main method, we create a prototype monster and customize it by adding an ability. Then, we clone the prototype to create new monsters and modify their attributes accordingly. Finally, we print the information of each monster.

By utilizing the prototype design pattern, we can create new objects by cloning an existing prototype, modify the cloned objects as needed, and avoid repetitive object creation code.
### What is a registry?
In software development, a registry is a centralized data structure or service that stores and manages objects or resources in a system. It provides a way to access and retrieve objects or resources based on unique keys or identifiers. The primary purpose of a registry is to facilitate the sharing, lookup, and management of objects or resources throughout an application or system.

Here are a few reasons why we might need a registry:

Object Management: A registry can be used to manage and track objects or resources in a system. It provides a central point of control for creating, accessing, and releasing objects. By using a registry, we can ensure that objects are properly instantiated, configured, and cleaned up when no longer needed.

Object Lookup: A registry can act as a lookup mechanism for objects or resources. Instead of instantiating or accessing objects directly, we can use the registry to retrieve them by providing a unique key or identifier. This allows for more flexibility in managing object dependencies and decouples the code from explicit object creation.

Object Sharing: A registry can facilitate object sharing and reuse. Instead of creating new instances of objects every time they are needed, we can register them in the registry and retrieve them when required. This helps to reduce resource consumption and improve performance by reusing existing objects.

Configuration Management: A registry can be used to store and manage configuration settings or parameters for various components or modules in an application. It allows for centralized configuration management, making it easier to update or modify settings without requiring changes in multiple places.

Service Location: In the context of service-oriented architectures or dependency injection frameworks, a registry can act as a service locator. It provides a way to locate and retrieve specific services or dependencies based on their registered keys or names.

Overall, a registry provides a centralized and organized approach to manage, access, and share objects or resources within a system. It promotes modular design, improves code flexibility, and enhances code reuse.

Major functionalities in use: Regsiter() -> To register new objects as a key and value pair, get() -> to get the object needed based on a key.


### Singleton

We also use Singleton design pattern to design the registry class.<br>
<b>WHY?</b>

A registry is often implemented as a singleton because it provides a central point of access for managing and retrieving objects or resources throughout an application. By enforcing the singleton pattern, you ensure that there is only one instance of the registry class within the application.

Here are a few reasons why a registry is commonly implemented as a singleton:

Centralized access: A registry acts as a centralized repository or registry of objects, configurations, or resources. It provides a single point of access for other parts of the application to interact with and retrieve these objects or resources. By having a singleton registry, you can ensure that all parts of the application are accessing the same instance of the registry, avoiding inconsistencies or conflicts that may arise from multiple instances.

Global availability: As a singleton, the registry instance is globally accessible throughout the application. Any component or module can access the registry without having to pass around references or instantiate it repeatedly. This makes it convenient to retrieve objects or resources from the registry whenever needed.

Resource management: In some cases, a registry may be responsible for managing limited resources or controlling access to shared resources. By using a singleton registry, you can enforce control over the allocation and availability of these resources. Multiple instances of the registry could lead to resource duplication or conflicts.

Encapsulation and organization: Implementing a registry as a singleton allows you to encapsulate and organize related functionality within a single class. It provides a clear boundary and separation of concerns for managing and accessing objects or resources. Other parts of the application can interact with the registry through well-defined methods or APIs, promoting a clean and modular design.

However, it's important to note that not all registries must be implemented as singletons. The decision to use a singleton pattern for a registry depends on the specific requirements and constraints of the application. In some cases, alternative approaches such as dependency injection frameworks or application contexts may be more suitable for managing object dependencies or resource access.