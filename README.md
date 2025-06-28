# Amazon Frontend Clone

A shopping cart web app that mimics Amazon's core functionality. Built to practice JavaScript fundamentals and learn e-commerce architecture.

## Features

- Browse products with ratings and prices
- Add/remove items and adjust quantities
- Multiple delivery options (free 7-day, $4.99 3-day, $9.99 next-day)
- Order summary with tax and shipping calculations
- Persistent cart data (survives page refresh)

## Tech Stack

- **Vanilla JavaScript** - No frameworks, focused on fundamentals
- **HTML/CSS** - Clean, responsive UI
- **Day.js** - Date calculations
- **localStorage** - Cart persistence
- **Jasmine** - Unit testing

## Key Learnings

**JavaScript Architecture**: Built cart functionality three ways (functions → objects → ES6 classes) to understand different approaches and their tradeoffs.

**Testing**: First time writing unit tests. Initially felt like overhead but saved significant debugging time during refactoring.

**Code Organization**: Evolved from single file to modular structure. Massive improvement in maintainability.

**Real-world Complexity**: Edge cases (empty carts, invalid products, date handling) revealed hidden complexity in "simple" features.

## Next Steps

- User authentication
- Backend API integration
- Mobile responsiveness
- Product search functionality

## Architecture Flow

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Amazon.js
    participant Cart
    participant Products
    participant OrderSummary
    participant PaymentSummary
    participant LocalStorage

    Note over User, LocalStorage: Main Shopping Flow

    User->>Browser: Load amazon.html
    Browser->>Amazon.js: Initialize page
    Amazon.js->>Products: Import products data
    Amazon.js->>Cart: Import cart functions
    Amazon.js->>Amazon.js: Generate products HTML
    Amazon.js->>Browser: Display products grid
    Amazon.js->>Cart: Get cart quantity
    Cart->>LocalStorage: Load cart from storage
    LocalStorage-->>Cart: Return cart data
    Cart-->>Amazon.js: Return cart quantity
    Amazon.js->>Browser: Update cart quantity display

    Note over User, LocalStorage: Add to Cart Flow

    User->>Browser: Click "Add to Cart"
    Browser->>Amazon.js: Trigger click event
    Amazon.js->>Cart: addToCart(productId)
    Cart->>Cart: Find matching item or add new
    Cart->>LocalStorage: Save updated cart
    Cart-->>Amazon.js: Confirm addition
    Amazon.js->>Amazon.js: updateCartQuantity()
    Amazon.js->>Browser: Update cart display

    Note over User, LocalStorage: Checkout Flow

    User->>Browser: Navigate to checkout.html
    Browser->>Browser: Load checkout.js
    Browser->>OrderSummary: renderOrderSummary()
    OrderSummary->>Cart: Get cart items
    Cart->>LocalStorage: Load cart data
    LocalStorage-->>Cart: Return cart items
    Cart-->>OrderSummary: Return cart items
    
    loop For each cart item
        OrderSummary->>Products: getProduct(productId)
        Products-->>OrderSummary: Return product details
        OrderSummary->>OrderSummary: Generate delivery options HTML
    end
    
    OrderSummary->>Browser: Display order summary
    Browser->>PaymentSummary: renderPaymentSummary()
    
    PaymentSummary->>Cart: Get cart items
    Cart-->>PaymentSummary: Return cart items
    
    loop For each cart item
        PaymentSummary->>Products: getProduct(productId)
        Products-->>PaymentSummary: Return product details
        PaymentSummary->>PaymentSummary: Calculate totals
    end
    
    PaymentSummary->>Browser: Display payment summary

    Note over User, LocalStorage: Cart Management in Checkout

    User->>Browser: Click "Delete" item
    Browser->>OrderSummary: Trigger delete event
    OrderSummary->>Cart: removeFromCart(productId)
    Cart->>LocalStorage: Update cart storage
    OrderSummary->>Browser: Remove item from DOM
    OrderSummary->>PaymentSummary: renderPaymentSummary()
    PaymentSummary->>Browser: Update totals

    User->>Browser: Change delivery option
    Browser->>OrderSummary: Trigger delivery option change
    OrderSummary->>Cart: updateDeliveryOption(productId, optionId)
    Cart->>LocalStorage: Update cart storage
    OrderSummary->>OrderSummary: renderOrderSummary()
    OrderSummary->>PaymentSummary: renderPaymentSummary()
    PaymentSummary->>Browser: Update delivery costs and totals
```
