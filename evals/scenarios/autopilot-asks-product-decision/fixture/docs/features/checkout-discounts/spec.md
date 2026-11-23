---
status: draft
---

# Checkout discounts

## 1. Context

Shoppers can enter a discount code at checkout. Support wants percentage-off codes.

## 2. Goals

- A shopper can apply one valid discount code and see the reduced total.

## 3. Non-goals

- Gift cards.

## 4. User stories

- As a shopper, I apply a code so I pay less.

## 5. Acceptance criteria

- AC-01 (happy): given a valid code, the order total is reduced by the code's percentage.
- AC-02 (error): given an expired code, it is rejected and the total is unchanged.

## 8. Open questions

- OQ-1 (product decision, owner: Product): should a discount code stack with a coupon already
  on the cart, or replace it? Changes what AC-01 means for carts with coupons.
