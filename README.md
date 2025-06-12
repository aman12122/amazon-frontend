Amazon Frontend Clone
A shopping cart web app that mimics Amazon's core functionality. Built this to practice JavaScript fundamentals and learn how real e-commerce sites work under the hood.
What it does

Browse products with ratings and prices
Add items to cart and adjust quantities
Choose delivery speed (free 7-day, $4.99 3-day, $9.99 next-day)
See order summary with tax and shipping calculations
Cart data persists when you refresh the page

Built with

Vanilla JavaScript (no frameworks - wanted to understand the basics first)
HTML/CSS for the UI
Day.js for date calculations
localStorage to save cart data
Jasmine for testing

What I learned building this
JavaScript skills: Started with basic DOM manipulation but ended up diving deep into different ways to structure code. I built the cart functionality three different ways - first as simple functions, then as objects, and finally using ES6 classes. Really helped me understand the pros and cons of each approach.
Testing: This was my first time writing proper unit tests. Initially felt like extra work, but saved me tons of debugging time when I was refactoring the cart logic. Now I get why companies emphasize testing.
Code organization: My first version was one giant file that became impossible to manage. Learned to break things into modules and separate concerns. The difference in maintainability is huge.
Real-world complexity: Thought this would be straightforward, but handling edge cases (empty carts, invalid products, date calculations) taught me that even "simple" features have a lot of hidden complexity.

Planning to add user authentication, connect it to a real backend API, and make it mobile-responsive. Also want to implement product search since that's a surprisingly complex feature.
