# SOLID PRINCIPLES IN PYTHON

---

**S.O.L.I.D STANDS FOR:**

- S – Single-responsibility principle
- O – Open-closed principle
- L – Liskov substitution principle
- I – Interface segregation principle
- D – Dependency Inversion Principle
  **S – Single-responsibility principle**

Applying these principles in programming will allow us to write better quality code and therefore be a better developer.

---

## Single Responsibility Principle

Every module or function should have a single responsibility, and that responsibility should be entirely encapsulated by the module or function.

Consider a module `Calculator` and it has functions for addition, subtraction, multiplication, and division.

```python
class Calculator:
    def add(self,  a,  b):
        return a + b

    def subtract(self,  a,  b):
        return a - b

    def multiply(self,  a,  b):
        return a * b

    def divide(self,  a,  b):
        return a / b
```

This is not a good way of coding as Calculator class contains multiple responsibilities. Each operation should be in its separate class.

```python
class Adder:
    def add(self, a, b):
        return a + b

class Subtractor:
    def subtract(self, a, b):
        return a - b

class Multiplier:
    def multiply(self, a, b):
        return a * b

class Divider:
    def divide(self, a, b):
        return a / b
```

Now, each class holds the logic for its specific operation, complying with SRP as every class has its own responsibility.

## Open/Closed Principle

Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
Let's see another example:

```python
class ReportGenerator:
	def generate_report(self, data):
		# logic for generating report
		pass

	def format_report(self):
		# logic for formatting report
		pass
```

In this example, if we need to change the report format, we need to modify the ReportGenerator class, which violates the Open/Closed Principle.

```python
class ReportGenerator:
	def generate_report(self, data):
		# logic for generating report
		pass

class ReportFormatter:
	def format_report(self, report, format_type):
		# logic for formatting report based on format_type
		pass
```

In this updated design, ReportFormatter can be extended for new formats without modifying the existing ReportGenerator class.

## Liskov Substitution Principle

Subclasses should be substitutable for their base classes without altering the correctness of the program.

Consider the following example:

```python
class Bird:
	def fly(self):
		print("Flying")

class Sparrow(Bird):
	def fly(self):
		print("Sparrow flying")

class Ostrich(Bird):
	def fly(self):
		raise Exception("Cannot fly")
```

In this case, Ostrich violates LSP as it cannot fly, unlike other birds. A better design would be:

```python
class Bird:
	pass

class FlyingBird(Bird):
	def fly(self):
		print("Flying")

class Sparrow(FlyingBird):
	pass

class Ostrich(Bird):
	pass
```

Now FlyingBird and Bird are separate classes, ensuring that all subclasses of FlyingBird can fly, adhering to LSP.

## Interface Segregation Principle

No client should be forced to depend on methods it does not use.
Consider the following example:

```python
class Worker:
	def work(self):
		print("Working")

	def eat(self):
		print("Eating")

class Human(Worker):
	def work(self):
		print("Human working")

	def eat(self):
		print("Human eating")
```

In this design, Human is forced to implement both work and eat methods. A better design would be:

```python
class Workable:
	def work(self):
		pass

class Eatable:
	def eat(self):
		pass

class Human(Workable, Eatable):
	def work(self):
		print("Human working")

	def eat(self):
		print("Human eating")
```

Now Human can choose to implement either Workable, Eatable, or both, adhering to ISP.

## Dependency Inversion Principle

High-level modules should not depend on low-level modules. Both should depend on abstractions.
Consider the following example:

```python
class LightBulb:
	def turn_on(self):
	print("LightBulb: turned on")

	def turn_off(self):
		print("LightBulb: turned off")

class Switch:
	def __init__(self, bulb):
		self.bulb = bulb

	def operate(self):
		self.bulb.turn_on()
```

In this design, Switch is highly dependent on LightBulb. A better design would be:

```python
class Switchable:
	def turn_on(self):
		pass

	def turn_off(self):
		pass

class LightBulb(Switchable):
	def turn_on(self):
		print("LightBulb: turned on")

	def turn_off(self):
		print("LightBulb: turned off")

class Switch:
	def __init__(self, device):
		self.device = device

	def operate(self):
		self.device.turn_on()

```

Now Switch depends on the Switchable interface, not the concrete LightBulb class, adhering to DIP.
