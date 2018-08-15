<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250" align="right">

# Project Summary

In this project we will create a e-commerce React application from an start to finish. We will be provided with the basic file structure from create-react-app, but the App.js file is empty. We will be working on this app over the course of three days. Each day's project is divided into four Steps, with the first step being comparable to that day's mini-project and the following steps adding more features or implementing new patterns. You should expect to be able to complete the first two steps on each day, while steps three and four will offer a challenge for 


# Day 1

On this day we will start building our React app. We will create a class component with state in the App.js file. We will practice rendering lists of data from state by looping over them and returning JSX code. At the end of this project you should have a better understanding of the following concepts.

* Components
* State
* Conditional Rendering
* Array.map
* JSX


# Live Example

<a href=#">Click Me!</a>

<img src="#" />

## Setup

- `Fork` and `clone` this repository.
- `cd` into the project directory.
- Run `npm install`.
- After `npm install` has finished run `npm start`.

## Step 1

### Summary

In this step we will create a class component called App, with state. State should have one property, an array of products. You will need to fill this array with a list of products. Each product is represented by an object with the following properties: id (number), imageUrl (string), title (string), price (number), and description (string). The display of our App component should have a left and right side; on the left we will display the list of products. On the right will be the cart, where users can add see the items that they are going to purchase. A user should have the ability to add an item from the products list to the cart by clicking a button. If an item is clicked multiple times, simply add duplicates of that item to the cart. We will implement a quantity counter later on.

### Instructions

- Open `src/App.js`. This file will be empty. Create a class component that is the default export.
* Create an array on state called products and populate it with a few product objects. Each product is represented by an object with the following properties: id (number), imageUrl (string), title (string), price (number), and description (string).
* Create an empty array on state called cart.
- Create two sections in the return statement of App's render method. The first will hold the products list, the other will hold the cart list.
- Create an h1 for each of these divs, to label them as Products and Cart respectively.
- In the products section, map over the products array on state and return a div container with an image, h4, and p tags to represent the data for the specific product. Don't forget to give your outer div a key attribute. There should also be an Add to Cart button, but don't worry about hooking up an onclick function yet.
* In the cart section, map over the cart array and render the product name and price.
- Write a method on the App component called `handleAddToCart`. This will take one parameter, an object, which it will add to the cart array on state. Now we can attach this method to the onClick event listener on the Add to Cart button, and pass in the product object.

<details>

<summary> Detailed Instructions </summary>

<br />

Let's begin by opening `src/App.js`. Create a class component called App that is the default export.

```js
import React, { Component } from "react";

export default class App extends Component {}
```

Now create a constructor, call super, and create our component state. State needs to have a products array, which we will fill with made up products. These need to have an id, imageUrl, title, price, and description.

```js
constructor(props) {
    super(props);
    this.state = {
        products: [{
            id: 1,
            imageUrl: '',
            title: 'fancy hat',
            price: 12.99,
            description: 'has a feather in it.'
        } // ... add a few more
        ],
        cart: []
    }
}
```

Now we create two sections within App's render method; one for products and one for cart.

```js
render(){
    return(
        <div className="App">
            <section className="products">
                <h1>Products</h1>
            </section>
            <section className="cart">
                <h1>Cart</h1>
            </section>
        </div>
    )
}
```

Within the products section, map over the product data on state, in order to render the image, name, description and price into JSX. Also add an Add to Cart button.

```js
<section className="App">
  {this.state.products.map(item => (
    <div>
      <img src={item.imageUrl} />
      <h4>{item.name}</h4>
      <p>{item.description}</p>
      <p>{item.price}</p>
      <button>Add to Cart</button>
    </div>
  ))}
</section>
```

Now map over the cart array, to display the name, price, and description within the cart component. Only display the name, description, and price.

```js
<section className="cart">
  {this.state.cart.map(item => (
    <div>
      <h4>{item.name}</h4>
      <p>{item.description}</p>
      <p>{item.price}</p>
    </div>
  ))}
</section>
```

Write a method called `addItemToCart`, that will add the item to the cart array on state. Make sure to create a deep copy of the cart array, to avoid modifying state directly.

```js
addToCart(item){
    const newCart = this.state.cart.map( cartItem => Object.assign({}, cartItem) )
    newCart.push(item)
    this.setState({
        cart: newCart 
    })
}
```

Now use this method as the onclick for our Add to Cart button. Be sure to pass in the product object.

```js
<button onClick={() => this.addToCart(item)}> Add to Cart </button>
```

</details>

## Step 2

### Summary

In this step we will display the total price from the cart. In step 1, we were given the dataset for the products. Now we will create our own products and organize them into categories. E.g. `this.state = { shoes: [...], shirts: [...], hats: [...] }`, where each item on state is an array of product objects. Then display the products on the left side sorted into categories with a header for the type of product. We also want to have a checkout button on the cart side. This should clear out the cart and display an alert to inform the user that their purchase has been completed.

### Instructions

- Create a container to display the Total amount, at the bottom of the App component
- This container can be a div with an 'h1' inside it and a 'p' tag
- This container should also include the Checkout Button, which should call the checkout method, to clear out the cart and call an alert to let the user know that their purchase has been completed.
* create your own data on state, sorted into category arrays.
* You should follow the same object structure as we had in step 1, with each product that you create having a unique id, name, description, price, and imageUrl.

<details>
<summary> Detailed Instructions </summary>

Here we will create the Total container. Use the Array.reduce method to sum up the total cost.

```js
<div className="total">
    <h1>TOTAL</h1>
    <p>${
        this.state.cart.reduce((accumulator, current) => (accumulator += current.price), 0)
        }
    </p>
    <button onClick={this.checkout}>Checkout</button>
</div>
```
checkout method on App component
```js
checkout = () => {
    this.setState({
        cart: []
    });
    alert('Purchase is complete!');
}
```

Here we will create our own categories of products on state
```js
this.state = {
    cart: [],
    hats: [
        {
            id: 1,
            name: 'Fisherman\'s Hat',
            description: 'Headgear commonly used by fishermen. Increases fishing skill marginally.',
            price: 12.99,
            imageUrl: ''
        },
        {
            id: 2, 
            name: 'Metal Hat',
            description: 'Uncomfortable, but sturdy.',
            price: 8.99,
            imageUrl: ''
        }
    ],
    beachGear: [
        {
            id: 3,
            name: 'Tent',
            description: 'Portable shelter.',
            price: 32.99,
            imageUrl: ''
        }
    ]
}
```
Once we have created these product category arrays, we will display them in sections for each category. 
```js
<div className="products">
    <h1>PRODUCTS</h1>
    <h2>Hats</h2>
    {
        this.state.hats.map( item => {
            return(
                <div>
                    <img src={item.imageUrl} />
                    <h4>{item.name}</h4>
                    <p>{item.descrition}</p>
                    <p>{item.price}</p>
                    <button onClick={()=> this.addItemToCart(item)}> Add to Cart </button>
                </div>
            )
        })
    }
    <h2>Beach Gear</h2>
    {
        // ... same as above
    }
</div>
```
</details>

## Step 3

### Summary

In this step we will add two text input fields on the cart side of our app. These will take in an mailing address and a credit-card number from the user. We want to verify that these fields have been filled out and are not empty when the user clicks on 'checkout'. If the user attempts to checkout without filling out both of these fields, call an alert which will inform them of the error.

### Instructions

* At the bottom of our App component but before the total container, create a div that will be the inputs container. 
* Add an input for address and one for credit card. These should be able to store their values on state.

<details><summary>Detailed Instructions</summary>

Add an inputs container, which will allow the user to enter an address and credit card number.
These input fields should store their value on state, using an onChange event listener. 
```js
<div className="inputs">
    <input placeholder="address" value={this.state.address} onChange={ this.handleAddressInput } />
    <input placeholder="credit card number" value={this.state.creditCard} onChange={this.handleCreditCardInput} />
</div>
```
Now we want to make sure that the user has entered in the required data when they attempt to check out. So we will edit the checkout method to check for this data.
```js
checkout = () => {
    if(!this.state.address || !this.state.creditCard) {
        alert( "Please fill out the required fields" )
    } else {
        alert( "Purchase complete!" )
        this.setState({
            cart: []
        })
    }
}
```

</details>

## Step 4

### Summary

In this step we want to count the quantity, if there are multiple copies of an item in the cart. We also want to be able to delete an item from the cart. We also want to be able to toggle between a simple list view and a full card view for the products on display, using conditional rendering.

### Instructions

* We also want to allow a user to add multiple copies of an item to the cart, and display a quantity, rather than duplicates of the same item. 
* create a 'removeItemFromCart' method, that takes in a single paramter, the item id, and either reduces this item's quantity or removes it from the cart if it's quantity is 1.
* Create a boolean value on state called `toggleCardView`, set to `true`. 
* Create a method called `handleToggleView`, which will toggle this value on state.
* In your maps for your products, give the outer div a different css class, e.g. `product_card` or `product_list`, depending on whether the `toggleCardView` is true or false.

<details>
<summary> Detailed Instructions </summary>

In order to start keeping track of cart quantity, we need to modify our add to cart method.
```js
addItemToCart( item ) {
    const newCart = this.state.cart.map( cartItem => {
        return {
            id: cartItem.id,
            name: cartItem.name,
            description: cartItem.description,
            price: cartItem.price,
            imageUrl: cartItem.imageUrl,
            quantity: cartItem.quantity
        }
    })
    const itemIndex = newCart.findIndex( cartItem => cartItem.id === item.id)
    if (itemIndex !== !1){
        newCart[itemIndex].quantity++
    } else {
        item.quantity = 1
        newCart.push(item)
    }
    this.setState({
        cart: newCart
    })
}
```
Now let's create a delete item method
```js
removeItemFromCart( id ) {
    const newCart = this.state.cart.map( cartItem => {
        return {
            id: cartItem.id,
            name: cartItem.name,
            description: cartItem.description,
            price: cartItem.price,
            imageUrl: cartItem.imageUrl,
            quantity: cartItem.quantity
        }
    })
    const itemIndex = newCart.findIndex( cartItem => cartItem.id === id)
    if(newCart[itemIndex].quantity === 1){
        newCart.splice(itemIndex,1)
    } else {
        newCart[itemIndex].quantity--
    }
    this.setState({
        cart: newCart
    })
}
```
</details>