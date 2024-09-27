# Challenge-Backend-Developer
This repository contains the answers to the chanllenge by María Belén Guzmán.

1. You're building a high-throughput API for a cryptocurrency trading platform. For this platform, time is extremely important because microseconds count when processing high-volume trade orders. For communicating with the API, you want to choose the verb that is fastest for read-only operations.
What verb should you choose for retrieving trade orders with the API server?
SELECT ONLY ONE

My answer: 1) GET

Example:

const express = require('express');
const app = express();


const tradeOrders = [
  { id: 1, asset: 'BTC', quantity: 1.5 },
  { id: 2, asset: 'ETH', quantity: 10 }
];


app.get('/trades', (req, res) => {
  res.json(tradeOrders);
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});


2. You work for a Customer Relationship Management (CRM) company. The
company's clients gain CRM access through a RESTful API. The CRM allows clients to add contact information for customers, prospects, and related persons (e.g., virtual assistants or marketing directors). You want to choose an
appropriate API request path so clients can easily retrieve information for a single contact while also being flexible for future software changes.
Which of the following API paths should you use?
SELECT ONLY ONE
My answer: 2) /contacts/{contact_id}

Example: 

const express = require('express');
const app = express();

const contacts = [
  { id: 1, name: 'Client One', email: 'clientone@gmail.com' },
  { id: 2, name: 'Client Two', email: 'clienttwo@gmail.com' }
];

app.get('/contacts/:contact_id', (req, res) => {
  const contact = contacts.find(c => c.id == req.params.contact_id);
  if (!contact) {
    return res.status(404).json({ error: 'Contact not found' });
  }
  res.json(contact);
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});


3. You work for a large social media network, and you've been tasked witherror handling for the API. You're trying to decide on an appropriate errorcode for authentication failures based on non-existent users and incorrect passwords. You want to balance security against brute force attacks with providing descriptive and true error codes.
Which HTTP error code(s) should you use to keep the system secure and still report that an error occurred?
SELECT ONLY ONE
My answer: 1) 404 if the user doesn't exist, and 403 if the password is wrong.

Example:

const express = require('express');
const app = express();


const users = [
  { username: 'user one', password: 'password123' }
];

app.use(express.json());

app.post('/login', (req, res) => {
  const { username, password } = req.body;
  const user = users.find(u => u.username === username);

  // 404 
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }

  // 403 
  if (user.password !== password) {
    return res.status(403).json({ error: 'Incorrect password' });
  }

  res.json({ message: 'Login successful' });
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});

4. You're writing documentation for requesting information about a given user in your system. Your system uses UUIDS (universally unique identifiers) as user identifiers. In your documentation, you want to show an example.
True or false: You should put a fake UUID into the example code (instead of just the text "UUID") as a placeholder.
SELECT ONLY ONE
My answer:  1) TRUE


5. You're building code to handle errors issued from a remote API server. The
response may or may not have an error.
How much work should your method, handleErrors(response), handle?
SELECT ONLY ONE
My answer: 3)Check for the presence of an error. If it exists, set a class property to the error, then throw an exception.

 Example: 

function handleErrors(response) {
  if (response.error) {
    this.error = response.error;
    throw new Error(response.error);
  }
  return response.data;
}


try {
  const response = { error: 'Network issue' };
  handleErrors(response);
} catch (error) {
  console.error('Error caught:', error.message);
}



6. You have two classes: a database driver and an email driver. Both classes need to set errors so that your front-end interface displays any errors that transpire on your platform.
Which way should you implement this error handling?
SELECT ONLY ONE
My answer: 2) Make a trait to handle errors so it'll collect errors in any class that uses it.

class ErrorTrait {
  setError(error) {
    this.error = error;
  }

  getError() {
    return this.error;
  }
}

class DatabaseDriver extends ErrorTrait {}
class EmailDriver extends ErrorTrait {}

const dbDriver = new DatabaseDriver();
dbDriver.setError('Database connection failed');
console.log(dbDriver.getError()); // Output: Database connection failed



7. You need to name the private method in your class that handles loopingthrough
eCommerce products to collect and parse data. That data gets stored in an array and set as a class property.
Which of the following should you use to name your method?
SELECT ONLY ONE
My answer: 3) parseDataForProducts()

class ProductParser {
  parseDataForProducts(data) {
    // Procesa los datos del producto
    const parsedData = data.map(product => {
      return { id: product.id, name: product.name };
    });
    return parsedData;
  }
}



8. There are multiple places in your codebase that need to access the
database. To access the database, you need to supply credentials. You want to balance security with useability.
What strategy should you use to store and access these credentials? SELECT ONLY ONE
My answer: 4) Put them in a .env file, load data from it into a configuration system, then request the credentials from a database service provider.

Example:
Bash:
 # .env
DB_USER=root
DB_PASS=secret

Code:
require('dotenv').config();
const dbUser = process.env.DB_USER;
const dbPass = process.env.DB_PASS;

console.log(`Connecting to database with user ${dbUser}`);



Thank you for reading.
