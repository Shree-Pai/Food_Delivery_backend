# Menu Order API

This is a simple API for managing a menu, placing orders, and tracking order statuses in a restaurant or food delivery service.

## Features

1. **Add or Update Menu Item**: Add new items to the menu or update existing items.
2. **Get Menu**: Retrieve all available menu items.
3. **Place Order**: Customers can place orders by selecting items from the menu.
4. **Get Order Details**: View the details of a specific order by order ID.
5. **Automated Status Updates**: A cron job updates the order status from "Preparing" → "Out for Delivery" → "Delivered".

## Technologies Used

- **Node.js**: Server-side JavaScript runtime.
- **Express**: Web framework for Node.js.
- **Body-Parser**: Middleware to parse JSON request bodies.
- **Node-Cron**: For automating the update of order statuses.

## API Endpoints

### 1. Add or Update Menu Item
**POST /menu**

Adds a new menu item or updates an existing item by name.

#### Request Body:
```json
{
  "name": "Dosa",
  "price": 100,
  "category": "South Indian"
}
```

#### Response:
- **Success (New Item Added)**:
```json
{
  "message": "New menu item added.",
  "item": {
    "id": 1,
    "name": "Dosa",
    "price": 100,
    "category": "South Indian"
  }
}
```
- **Success (Item Updated)**:
```json
{
  "message": "Menu item updated successfully.",
  "item": {
    "id": 1,
    "name": "Dosa",
    "price": 120,
    "category": "South Indian"
  }
}
```

### 2. Get Menu
**GET /menu**

Retrieves all menu items.

#### Response:
```json
[
  {
    "id": 1,
    "name": "Dosa",
    "price": 100,
    "category": "South Indian"
  }
]
```

### 3. Place Order
**POST /orders**

Places an order by selecting menu items.

#### Request Body:
```json
{
  "items": [1],
  "customerName": "John Doe"
}
```

#### Response:
```json
{
  "message": "Order placed successfully.",
  "orderId": 1,
  "status": "Preparing"
}
```

### 4. Get Order Details
**GET /orders/:id**

Fetches the details of a specific order by `orderId`.

#### Response:
```json
{
  "orderId": 1,
  "items": [
    {
      "id": 1,
      "name": "Dosa",
      "price": 100,
      "category": "South Indian"
    }
  ],
  "customerName": "John Doe",
  "status": "Preparing",
  "createdAt": "2024-12-04T10:30:00.000Z"
}
```

### 5. Automated Status Updates (Cron Job)
The cron job updates the status of all orders every minute:
- **"Preparing" → "Out for Delivery" → "Delivered"**

## Installation

### Prerequisites
- **Node.js** (version 14 or higher)
- **npm** (Node Package Manager)

### Steps to Run the Project Locally

1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/menu-order-api.git
   ```

2. Navigate into the project folder:
   ```bash
   cd menu-order-api
   ```

3. Install dependencies:
   ```bash
   npm install
   ```

4. Start the server:
   ```bash
   npm start
   ```

The server will start running on [http://localhost:3300](http://localhost:3300).

## Testing with Postman

You can test the API using [Postman](https://www.postman.com/). The following API endpoints can be tested:

1. **POST /menu** - Add or update a menu item.
2. **GET /menu** - Retrieve all menu items.
3. **POST /orders** - Place an order.
4. **GET /orders/:id** - Fetch order details by order ID.

