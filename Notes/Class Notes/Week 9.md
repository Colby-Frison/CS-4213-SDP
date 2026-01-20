# Weekly question

**Question:** 
How does the "program to an interface" technique help achieve polymorphism in software design?

**Answer:** 
Programming to an interface helps achieve polymorphism by letting you write code that works with a general category of things instead of one specific type. You define what needs to be done (the interface) without worrying about how each different object will do it. For example, if you have a 'Drawable' interface, your main program just knows it needs to call a 'draw()' method. It can hold a 'Drawable' object that could be a 'Circle', a 'Square', or anything else that can be drawn. This is core of polymorphism, the same 'draw()' command results in different behavior depending on whether the object is a circle or a square. The main program doesn't need to know the details; it just trusts that whatever object it's given knows how to draw itself. This makes your code much more flexible because you can easily add new types of drawable objects later without having to change the main program.


>From chapter 16
	16.1, 16.2, 16.3

---

# Monday


# Wednesday


# Friday

What are patterns: "Patterns are effective design solutions to common design problems."
Why be a good software engineer: "Allows you to be more efficient, saving time, which is the only thing you can't get back"
Problem directed approach vs pattern directed approach: ""
Is the right pattern being applied or is the pattern applied correctly: ""

