# PlayWright-Practice
SauceDemo Practice 
import { test, expect } from '@playwright/test';

test('Add 3 items to cart on Saucedemo', async ({ page }) => {
  // Step 1: Go to the Saucedemo login page
  await page.goto('https://www.saucedemo.com/');

  // Step 2: Log in with valid credentials
  await page.fill('#user-name', 'standard_user');
  await page.fill('#password', 'secret_sauce');
  await page.click('#login-button');

  // Step 3: Wait for inventory page to load
  await expect(page).toHaveURL('https://www.saucedemo.com/inventory.html');

  // Step 4: Add 3 items to cart
  await page.click('#add-to-cart-sauce-labs-backpack');
  await page.click('#add-to-cart-sauce-labs-bike-light');
  await page.click('#add-to-cart-sauce-labs-bolt-t-shirt');

  // Step 5: Click cart icon
  await page.click('.shopping_cart_link');

  // Step 6: Verify 3 items are in cart
  const cartItems = await page.locator('.cart_item');
  await expect(cartItems).toHaveCount(3);
});
