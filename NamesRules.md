# A guide to code reviewing and clean code best practices

## Names rules

### Choose descriptive and unambiguous names

Make sure the name is descriptive, names are too important to treat carelessly.

**The problem**

````php
$result = $query->getResult();
if (count($result) > 0) {
	foreach($result as $row){
		Log::error("Error:" . $row->description);
	}
}
````

**The solution**

````php
$errorsStoredResultset = $queryToFindStoredErrors->getResult();
if (count($errorsStoredResultset) > 0) {
	foreach($errorsStoredResultset as $errorStoredRow){
		Log::error("Error:" . $errorStoredRow->description);
	}
}
````

### Use pronounceable names

If you can’t pronounce a name it requires an effort of look-up to understand. When a name is pronounceable also it is searchable, and searchable names is a must to enhance find operations in refactoring.

**The problem**

````php
$appt = new DateTime("2015-12-10");
$hToWork = $appt->diff(new DateTime())->format("H");
````

**The solution**

````php
$appointment = new DateTime("2015-12-10");
$hoursToWork = $appointment->diff(new DateTime())->format("H");
````

### Replace magic numbers with named constants

You should hide raw number behind well-named constants. 
 
In most cases, some constants are so easy to recognise that they don’t always need a named constant.

**The problem**

````php
function minutesOfDailyWork(){
	return 8 * 60;
}
````

**The solution**

````php
function minutesOfDailyWork(){
	//the minutes value does not need to be hide in a constant because is obvious
	return COMPANY.WORK_HOURS_PER_DAY * 60;
}
````

### Avoid encodings

Don't append prefixes, type information or scope information. This can be a hint of a bad approach in the code.

**The problem**

````php
$globalResult = 100;
$strDateOfBirth = '1980-01-01';
$WPPluginPath = '/myPath/plugin';
````

**The solution**

````php
$result = 100;
$dateOfBirth = '1980-01-01';
$blogPluginPath = '/myPath/plugin';
````
