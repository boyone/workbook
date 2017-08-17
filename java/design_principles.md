## Design principles for Java developers

-----

### Object Oriented programming review

### SOLID principles

#### SRP: Single Responsibility Principle
A module should have one, and only one, reason to change.

Bad example
``` java
public class UserSettingService {
    public void changeEmail(User user) {
        if(checkAccess(user)) {
            //Grant option change.
        }
    }

    public boolean checkAccess(User user) {
        //Verify if the user is valid.
    }
}
```
Good example
``` java
public class UserSettingService {
    public void changeEmail(User user) {
        if(SecurityService.checkAccess(user)) {
            //Grant option change
        }
    }
}

public class SecurityService {
    public static boolean checkAccess(User user) {
        //Check the access
    }
}
```

#### OCP: Open-Closed Principle
A software artifact should be open for extension but closed for modification.
In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.

Bad example
``` java
public class LoanApprovalHandler {
    public void approveLoan(PersonalLoanValidator validator) {
        if( validator.isValid() ) {
            //Process the loan
        }
    }
}

public class PersonalLoanValidator {
    public boolean isValid() {
        //Validation logic
    }
}
```
And then we have new type of loan added into system.

```java
public class LoanApprovalHandler {
    public void approvePersonalLoan(PersonalLoanValidator validator) {
        if( validator.isValid() ) {
            //Process the loan
        }
    }

    public void approveVehicleLoan(VehicleLoanValidator validator) {
        if( validator.isValid() ) {
            //Process the loan
        }
    }
}

public class PersonalLoanValidator {
    public boolean isValid() {
        //Validation logic
    }
}

public class VehicleLoanValidator {
    public boolean isValid() {
        //Validation logic
    }
}
```
If we have another new type of loan we still have to add approve* functions to the class LoanApprovalHandler and the class will become more and more large for support every types of loan

To avoid OCP principle violation we have to bring  abstraction or interface concept in

Example

First create abstract class for any loan validations
```java
/**
 * Abstract Validator class
 * Extended to add different
 * validators for different loan type
 */
public abstract class Validator{
    public boolean isValid();
}

/**
 * Personal loan validator
 */
public class PersonalLoanValidator extends Validator
{
    public boolean isValid() {
        //Validation logic.
    }
}

/**
* VehicleLoanValidator
* */
public class VehicleLoanValidator extends Validator
{
    public boolean isValid() {
        //Validation logic.
    }
}

/*
 * Similarly any new type of validation can
 * be accommodated by creating a new subclass
 * of Validator
 */
 ```
Now using the above validators we can write a LoanApprovalHandler to use the Validator abstraction.
```java
public class LoanApprovalHandler {
    public void approveLoan(Validator validator) {
        if ( validator.isValid())
        {
            //Process the loan.
        }
    }
}
```
#### LSP: Liskov Substitution Principle
Methods that use references to the base classes must be able to use the objects of the derived classes without knowing it

Bad example
```java
class Bird {
    public void fly(){}
    public void eat(){}
}
class Crow extends Bird {}
class Ostrich extends Bird{
    fly(){
        throw new UnsupportedOperationException();
    }
}

public BirdTest{
    public static void main(String[] args){
        List<Bird> birdList = new ArrayList<Bird>();
        birdList.add(new Bird());
        birdList.add(new Crow());
        birdList.add(new Ostrich());
        letTheBirdsFly ( birdList );
    }

    static void letTheBirdsFly ( List<Bird> birdList ){
        for ( Bird b : birdList ) {
            b.fly();
        }
    }
}
```

How do we fix such issues?

By using factoring. Sometimes factoring out the common features into a separate class can help in creating a hierarchy that confirms to LSP.

In the above scenario we can factor out the fly feature into- Flight and NonFlight birds.

```java
class Bird{
    public void eat(){}
}
class FlightBird extends Bird{
    public void fly()()
}
class NonFlight extends Bird{}
```

#### ISP: Interface Segregation Principle
Clients should not be forced to implement interfaces they don't use. Instead of one fat interface many small interfaces are preferred based on groups of methods, each one serving one submodule.

Bad example
```java
interface IWorker {
    public void work();
    public void eat();
}

class Worker implements IWorker{
    public void work() {
        // ....working
    }
    public void eat() {
        // ...... eating in launch break
    }
}

class SuperWorker implements IWorker{
    public void work() {
        //.... working much more
    }

    public void eat() {
        //.... eating in launch break
    }
}

class Manager {
    IWorker worker;

    public void setWorker(IWorker w) {
        worker=w;
    }

    public void manage() {
        worker.work();
    }
}
```
From the bad example below. What if we need to add a new class called 'Robot' which can perform work like the others but they don't eat?

Following it's the code supporting the Interface Segregation Principle. By splitting the IWorker interface in 2 different interfaces the new Robot class is no longer forced to implement the eat method. Also if we need another functionality for the robot like recharging we create another interface IRechargeble with a method recharge.

```java
interface IWorker extends Feedable, Workable {}

interface IWorkable {
    public void work();
}

interface IFeedable{
    public void eat();
}

class Worker implements IWorkable, IFeedable{
    public void work() {
        // ....working
    }

    public void eat() {
        //.... eating in launch break
    }
}

class Robot implements IWorkable{
    public void work() {
        // ....working
    }
}

class SuperWorker implements IWorkable, IFeedable{
    public void work() {
        //.... working much more
    }

    public void eat() {
        //.... eating in launch break
    }
}

class Manager {
    Workable worker;

    public void setWorker(Workable w) {
        worker=w;
    }

    public void manage() {
        worker.work();
    }
}
```

#### DIP: Dependencies Inversion Principle
- High-level modules should not depend on low-level modules. Both should depend on abstractions.

- Abstractions should not depend on details. Details should depend on abstractions.

Bad example
```java
class Worker {
    public void work() {
        // ....working
    }
}

class Manager {
    Worker worker;
    public void setWorker(Worker w) {
        worker = w;
    }

    public void manage() {
        worker.work();
    }
}

class SuperWorker {
    public void work() {
        //.... working much more
    }
}
```
Below is the code which supports the Dependency Inversion Principle. In this new design a new abstraction layer is added through the IWorker Interface. Now the problems from the above code are solved(considering there is no change in the high level logic):

- Manager class doesn't require changes when adding SuperWorkers.
- Minimized risk to affect old functionality present in Manager class since we don't change it.
- No need to redo the unit testing for Manager class.

```java
interface IWorker {
	public void work();
}

class Worker implements IWorker{
    public void work() {
        // ....working
    }
}

class SuperWorker  implements IWorker{
    public void work() {
        //.... working much more
    }
}

class Manager {
    IWorker worker;

    public void setWorker(IWorker w) {
        worker = w;
    }

    public void manage() {
        worker.work();
    }
}
```
### Others interesting design principles

#### DRY: Don't Repeat Yourself

#### Tell don't ask

#### KISS: Keep It Simple And Stupid

-----

References

https://www.javacodegeeks.com/2011/11/solid-single-responsibility-principle.html

http://www.oodesign.com/dependency-inversion-principle.html

http://www.oodesign.com/interface-segregation-principle.html

https://www.javacodegeeks.com/2011/11/solid-liskov-substitution-principle.html

https://www.javacodegeeks.com/2011/11/solid-open-closed-principle.html
