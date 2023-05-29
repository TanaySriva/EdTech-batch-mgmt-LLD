# Prototype-LLD

This project was created to understand the <b>Prototype design pattern</b>.


## Builder Pattern
The prototype design pattern is a creational design pattern that allows us to create new objects by cloning existing objects. Instead of creating objects from scratch, we can make copies of an existing object, called a prototype, and modify those copies as needed.

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
<b>Client</b> : Chief of Staff at a hospital.
<br>
What does he want to know : To get a list of doctors and nurses on duty with the number of hours they have worked.
<br>
What does he want to do : To make them attend trainings and surgeries.


### Classes Used
1. Staff - This class is the one that needs to be directed by the Chief of Staff. A staff has certain attributes like job "startTime", job "endTime", "floorNo" of work, what is their work "timeLimit" and a "staffList" of all the docs and nurses on duty.
2. StaffBuilder - This class helps in setting the attributes of the Staff class by building the object step by step and finally passing the instance to the constructor of staff class to set the required values.
3. DoctorBuilder, NurseBuilder - These are child classes of the StaffBuilder and them implement the abstracted "setStaffList()" method. This method is there to add the list of docs and nurses and their current working hours. This is hardcoded right now.
4. StaffDirector - A director class is needed because the Chief of Staff doesn't know what attributes of Staff to set. He has other work and he just wants to call a method called getStaff() based on his choice of Doctor or Nurse. So the director is the one that sets the required values. Chief of Staff can obviously override and directly do that if he wants to.
5. ClientChiefStaff - This is the client class where the client wants to just get the list of staff, make them go do training or surgery.