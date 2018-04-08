# A guide to code reviewing and clean code best practices

## Design rules 

### Prefer polymorphism to if/else or switch/case
(https://refactoring.guru/replace-conditional-with-polymorphism)

### Prevent over-configurability or under-configurability (find the sweet spot between being completely configurable and totally rigid).

### Use dependency injection.

### Follow Law of Demeter/principle of least knowledge. A class should know only its direct dependencies.