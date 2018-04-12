# A guide to code reviewing and clean code best practices

## Design rules 

### Replace Conditional with Polymorphism

Prefer polymorphism to if/else or a switch/case that chooses different behavior depending on the type of an object.

Also, this kind of conditional violates the [Open closed principle](GeneralRules.md#solid), and might be something to avoid in the most common situations.

**The problem**
```php
class Discount {
    public function getDiscount(){
        if($this->type == 'season'){
            return 10;
        }
        if($this->type == 'black_friday'){
            return 20;
        }
    }
}
```

**The solution**
```php
abstract class Discount {
    abstract public function getDiscount();
}

class BlackFridayDiscount extends Discount{
    public function getDiscount(){
        return 20;
    }
}

class SeasonDiscount extends Discount{
    public function getDiscount(){
        return 10;
    }
}
```

### Prevent over-configurability or under-configurability 

Try to find the sweet spot between being completely configurable and totally rigid.

### Use dependency injection

Dependency Injection is a design pattern that helps a class separate the logic of creating dependent objects. The result of this separation is a loosely coupled system where there is no rigid dependency between two concrete implementations.

**The problem**
```php
class Person {
    public function sendEmail(){
        $email = new ReminderEmail();
        $email->send();
    }
}
```

**The solution**
```php
interface Email {
    public function send();
}

class ReminderEmail implements Email{
    public function send(){
        //logic to send email
    }
}

class WorkEmail implements Email{
    public function send(){
        //logic to send email
    }
}

class Person {

    private $email;
    
    public function __construct(Email $email){
        $this->email = $email;
    }
    
    public function sendEmail(){
        $this->email->send();
    }
}
```

### Follow Law of Demeter

The definition of Law of Demeter (AKA principle of least knowledge) is that a class should know only its direct dependencies.