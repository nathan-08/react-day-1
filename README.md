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

## Part 1

### Summary

In this step we will create a class component called App, with state. State should have one property, an array of products. You will need to fill this array with a list of products. Each product is represented by an object with the following properties: id (number), imageUrl (string), title (string), price (number), and description (string). The display of our App component should have a left and right side; on the left we will display the list of products. On the right will be the cart, where users can add see the items that they are going to purchase. A user should have the ability to add an item from the products list to the cart by clicking a button. If an item is clicked multiple times, simply add duplicates of that item to the cart. We will implement a quantity counter later on.

### Instructions

1. Open `src/App.js`. This file will be empty. Create a class component that is the default export.
    <details>
    <summary> Detailed Instructions </summary>
    <br />

    Let's begin by opening `src/App.js`. Create a class component called App that is the default export.

    ```js
    import React, { Component } from "react";

    export default class App extends Component {}
    ```
    </details>

2. Create an array on state called products and populate it with a few product objects. Each product is represented by an object with the following properties: id (number), imageUrl (string), title (string), price (number), and description (string). Create an empty array on state called cart.

    <details>
    <summary> Detailed Instructions </summary>
    <br />
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
    </details>


4. Create two sections in the return statement of App's render method. The first will hold the products list, the other will hold the cart list. Create an h1 for each of these divs, to label them as Products and Cart respectively.

    <details>
    <summary>Detailed Instructions</summary>
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
    </details>



4. In the products section, map over the products array on state and return a div container with an image, h4, and p tags to represent the data for the specific product. Don't forget to give your outer div a key attribute. There should also be an Add to Cart button, but don't worry about hooking up an onclick function yet.
    <details>
    <summary>Detailed Instructions</summary>
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
    </details>

5. In the cart section, map over the cart array and render the product name and price.
    <details>
    <summary>Detailed Instructions</summary>
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
    </details>

6. Write a method on the App component called `handleAddToCart`. This will take one parameter, an object, which it will add to the cart array on state. Now we can attach this method to the onClick event listener on the Add to Cart button, and pass in the product object.



    <details>
    <summary>Detailed Instructions</summary>
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

## Part 2

### Summary

In this step we will calculate and display the total price from the cart. We will reorganize the products into categories, and store them in seperate arrays on state. E.g. `this.state = { shoes: [...], shirts: [...], hats: [...] }`, where each item on state is an array of product objects. Then display the products sorted into categories with a header for the type of product. We also want to have a checkout button on the cart side. This should clear out the cart and display an alert to inform the user that their purchase has been completed.

### Instructions

1. Change the structure of state, so that instead of a products array, there are seperate arrays for different product categories (which you can make up), e.g. shoes, shirts, pants.
    <details>
    <summary> Detailed Instructions </summary>

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
    </details>
2. Now map over these arrays within the products section, and create a header for each category.
Once we have created these product category arrays, we will display them in sections for each category. 
    <details>
    <summary>Detailed Instructions</summary>
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
3. Create a container to display the Total amount, at the bottom of the App component; this container can be a div with an 'h1' inside it and a 'p' tag
    <details>
    <summary>Detailed Instructions</summary>
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
    </details>
4. This container should also include the Checkout Button, which should call the checkout method, to clear out the cart and call an alert to let the user know that their purchase has been completed.
    <details>
    <summary>Detailed Instructions</summary>
    checkout method on App component
    ```js
    checkout = () => {
        this.setState({
            cart: []
        });
        alert('Purchase is complete!');
    }
    ```
    </details>

## Part 3

### Summary

In this step we will add two text input fields on the cart side of our app. These will take in an mailing address and a credit-card number from the user. We want to verify that these fields have been filled out and are not empty when the user goes to checkout. If the user attempts to checkout without filling out both of these fields, call an alert which will inform them of the error.

### Instructions

1. At the bottom of our cart section but before the total container, create a div that will be the inputs container. 
    <details><summary>Detailed Instructions</summary>

    Add an inputs container, which will allow the user to enter an address and credit card number.
    These input fields should store their value on state, using an onChange event listener. 

    ```js
    <div className="inputs">
        <input placeholder="address" value={this.state.address} onChange={ this.handleAddressInput } />
        <input placeholder="credit card number" value={this.state.creditCard} onChange={this.handleCreditCardInput} />
    </div>
    ```
    </details>
2. Add an input for address and one for credit card. These should be able to store their values on state.
    <details><summary>Detailed Instructions</summary>
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

## Part 4

### Summary

In this step we want to keep track of quantity if there are multiple copies of an item in the cart. We also want to be able to delete an item from the cart. We also want to be able to toggle between a simple list view and a full card view for the products on display, using conditional rendering.

### Instructions

1. In order to keep track of quantity, modify the addItemToCart method. When adding to the cart, it should check if the item is already on the cart, and if so, increase that object's quantity value by one.
    <details><summary> Detailed Instructions </summary>
    Modify the addItemToCart method, so that it can keep track of quantity if their are multiple instances of an item in the cart.

    ```js
    addItemToCart( item ){
        // make a deep copy of the cart array, to avoid mutating state.

        let newCart = this.state.cart.map( cartItem => Object.assign({}, cartItem) )
        let itemIndex = newCart.findIndex( cartItem => cartItem.id === item.id)
        if( itemIndex!== -1){
        newCart[itemIndex].quantity++
        } else {
        item.quantity++
        newCart.push(item)
        }
        this.setState({
        cart:newCart
        })
    }
    ```
    </details>

2. Create a deleteFromCart method. This should take in one parameter, an id, which it will use to remove the matching item from the cart array.
    <details><summary> Detailed Instructions </summary>
    Create a deleteFromCart method that takes an id parameter and removes the matching item from the cart array.

    ```js
    removeItemFromCart( id ){
        let newCart = this.state.cart.map( cartItem => Object.assign({}, cartItem) )
        let itemIndex = newCart.findIndex( cartItem => cartItem.id === id)
        if(newCart[itemIndex].quantity === 1){
        newCart.splice(itemIndex,1)
        }
        else {
        newCart[itemIndex].quantity--
        }
        this.setState({
        cart:newCart
        })
    }
    ```
    </details>
3. Create a button at the top of the products section, and a method for it called handleToggleView. Create a boolean value on state called toggleView. The handleToggleView method should set the toggleView value on state to its opposite value. We will use this boolean to conditionally render our products. Based on the value of toggleView, we want to switch between a detailed card view and a simple list. You can do this either by writing more JSX, or simply writing two different sets of CSS and toggling classes. 

    <details><summary> Detailed Instructions </summary>

    Create a Toggle View button at the top of the products section, and create a handleToggleView method which will toggle a toggleView boolean on state.

    ```js
    this.state = {
        toggleView: true,
        // ...

    }
    ```

    ```js
    <button onClick={ this.handleToggleView }>Toggle View</button>
    ```

    ```js
    handleToggleView = () => this.setState(state => { toggleView: !state.toggleView })
    ```

    Here we will toggle the class of our product elements, to render them either in more detailed card view or list view.

    ```js
    <div className={ this.state.toggleView ? 'product_card' : 'product_list' }>
        // ...

    </div>
    ```

    </details>
<!-- Modify the addItemToCart method, so that it can keep track of quantity if their are multiple instances of an item in the cart. -->

<!-- ```js
addItemToCart( item ){
    // make a deep copy of the cart array, to avoid mutating state.
    let newCart = this.state.cart.map( cartItem => Object.assign({}, cartItem) )
    let itemIndex = newCart.findIndex( cartItem => cartItem.id === item.id)
    if( itemIndex!== -1){
      newCart[itemIndex].quantity++
    } else {
      item.quantity++
      newCart.push(item)
    }
    this.setState({
      cart:newCart
    })
  }
``` -->

<!-- Create a deleteFromCart method that takes an id parameter and removes the matching item from the cart array.

```js
removeItemFromCart( id ){
    let newCart = this.state.cart.map( cartItem => Object.assign({}, cartItem) )
    let itemIndex = newCart.findIndex( cartItem => cartItem.id === id)
    if(newCart[itemIndex].quantity === 1){
      newCart.splice(itemIndex,1)
    }
    else {
      newCart[itemIndex].quantity--
    }
    this.setState({
      cart:newCart
    })
  }
```

Create a Toggle View button at the top of the products section, and create a handleToggleView method which will toggle a toggleView boolean on state.

```js
this.state = {
    toggleView: true,
    // ...
}
```

```js
<button onClick={ this.handleToggleView }>Toggle View</button>
```

```js
handleToggleView = () => this.setState(state => { toggleView: !state.toggleView })
```

Here we will toggle the class of our product elements, to render them either in more detailed card view or list view.

```js
<div className={ this.state.toggleView ? 'product_card' : 'product_list' }>
    // ...
</div>
``` -->

<!-- </details> -->

_____________________________end of day 1_______________________________________

