# A guide to code reviewing and clean code best practices

## Understandability tips

### Be consistent. If you do something a certain way, do all similar things in the same way.

### Use explanatory variables.
One of the more powerful ways to make a program readable is to break the calculations up into intermediate values that are held in variables with meaningful names.

### Encapsulate boundary conditions. Boundary conditions are hard to keep track of. Put the processing for them in one place.
````
//this has to be fixed
if ($level + 1 < self::MAX_LEVEL){
	new Game($player, $level +1);
}
//notice that $level + 1 appears twice, this boundary condition should be encapsulated in a variable as it follows
$nextLevel = $level + 1;
if ($nextLevel < self::MAX_LEVEL){
	new Game($player, $nextLevel);
}
````

### Prefer dedicated value objects to primitive type.

### Avoid negative conditionals.
````
//dirty
if(!$isNotLogged){
	doStuff();
}

//clean
if($isLogged){
	doStuff();
}
````