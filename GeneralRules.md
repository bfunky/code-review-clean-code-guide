# A guide to code reviewing and clean code best practices

## General rules

### Follow standard conventions
Follow any conventions the organization has already defined, most typical situations can be names of classes, properties or methods, camel case / snake case coding, or name of columns and tables on DB.

### KISS
KISS is an acronym for "Keep it simple, stupid" . The KISS principle states that most systems work best if they are kept simple rather than made complicated; therefore simplicity should be a key goal in design and unnecessary complexity should be avoided.

The primary goal in managing such complexity is to organize it so that a developer knows where to look to find things and need only understand the directly affected complexity at any given time. In contrast, a system with larger, multipurpose classes always hampers us by insisting we wade through lots of things we don’t need to know right now.

Use a tool to calculate **Cyclomatic Complexity**, in order to the structural complexity of the code. 
A program that has complex control flow will require more tests to achieve good code coverage and will be less maintainable. 

### Boy scout rule
**Leave the campground cleaner than you found it.**

The code has to be kept clean over time. We’ve all seen code rot and degrade as time passes. So we must take an active role in preventing this degradation.

If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot. The cleanup doesn’t have to be something big. Change one variable name for the better, break up one function that’s a little too large, eliminate one small bit of duplication, clean up one composite if statement. 