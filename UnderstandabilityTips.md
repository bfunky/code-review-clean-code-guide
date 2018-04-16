# A guide to code reviewing and clean code best practices

## Understandability tips

### Be consistent
Be careful with the conventions you choose, and once chosen, be careful to continue to follow them.

**The problem**

````php
class SaveCustomerUseCase {

	/** @var CustomerRepository */
	private $repository;
	
	public function execute(Customer $customer): bool {
		$this->repository->add($customer);
		return true;
	}
}
class EditCustomer {

	/** @var CustomerRepository */
	private $storage;
	
	public function edit(array $customer): Response {
		$this->storage->edit($dto);
		return Response(true);
	}
}
````

**The solution**

````php
class SaveCustomerUseCase {

	/** @var CustomerRepository */
	private $repository;
	
    public function execute(Customer $customer): Response {
    	$this->repository->add($customer);
		return Response(true);
    } 
}
class EditCustomerUseCase {

	/** @var CustomerRepository */
	private $repository;
	
	public function execute(Customer $customer): Response {
	    $this->repository->edit($customer);
		return Response(true);
	}
}
````

### Use explanatory variables

One of the more powerful ways to make a program readable is to break the calculations up into intermediate values that are held in variables with meaningful names.

**The problem**

````php
$split = split(' ', 'John Q. Citizen');
createPerson($split[0], $split[1], $split[2]);
````

**The solution**

````php
($name, $secondName, $lastName) = split(' ', 'John Q. Citizen');
createPerson($name, $secondName, $lastName);
````

### Encapsulate boundary conditions

Boundary conditions are hard to keep track of. Put the processing for them in one place.

**The problem**

````php
//notice that $level + 1 appears twice
if ($level + 1 < self::MAX_LEVEL){
	new Game($player, $level +1);
}
````

**The solution**

````php
//this boundary condition should be encapsulated in a variable as it follows
$nextLevel = $level + 1;
if ($nextLevel < self::MAX_LEVEL){
	new Game($player, $nextLevel);
}
````

### Prefer dedicated value objects to primitive type
Creating a primitive field is so much easier than making a whole new class, but with the past of the time the class became huge and unwieldy.

If you have a large variety of primitive fields, it may be possible to logically group some of them into their own class. Even better, move the behavior associated with this data into the class too.

**The problem**

````php
$customer = new Customer(
	'12345678-A',
	'john', 
	'doe', 
	1970, 
	1, 
	1, 
	self::INITIAL_STATUS_ID
);
// ... some LOC after ...
$customer->setAddress('2650 Geneva Street', 'Huntington', 'NY', '11743');
````

**The solution**

````php
$customer = new Customer(
	new CustomerId('12345678-A'),
	new Name('john', 'doe'), 
	new DateOfBirth(1970, 1, 1), 
	new InitialStatus()
);
// ... some LOC after ...
$address = new Address('2650 Geneva Street', 'Huntington', 'NY', '11743');
$customer->setStatus($address);
````

### Avoid negative conditionals
Negatives are a bit harder to understand than positives. Try to express conditionals as positives when possible. 

**The problem**

````php
if(!$isNotLogged){
	doStuff();
}
````

**The solution**

````php
if($isLogged){
	doStuff();
}
````