
# Superstore KPI Database Design

## 1. **Database Creation**
The first step is to create the database that will hold all the tables and their relationships. This is done using the `CREATE DATABASE` statement.

```sql
CREATE DATABASE superstore_kpi;
USE superstore_kpi;
```

## 2. **Customer Table**
The `Customer` table stores the details of customers. The primary key is `customerId`, and it has attributes like `customer_name` and `segment`.

```sql
CREATE TABLE Customer(
  customerId VARCHAR(100),
  customer_name VARCHAR(100) NOT NULL,
  segment VARCHAR(30),
  PRIMARY KEY(customerId)
);
```

### **Attributes:**
- `customerId`: Unique identifier for each customer.
- `customer_name`: Name of the customer.
- `segment`: Customer segment (e.g., Consumer, Corporate).

## 3. **Category Table**
The `Category` table contains categories for the products sold in the store. The `categoryId` is the primary key, and `category_name` is the name of the category.

```sql
CREATE TABLE Category(
  categoryId INT AUTO_INCREMENT,
  category_name VARCHAR(30) NOT NULL,
  PRIMARY KEY(categoryId)
);
```

### **Attributes:**
- `categoryId`: Unique identifier for each product category.
- `category_name`: Name of the category (e.g., Furniture, Technology).

## 4. **Subcategory Table**
The `Subcategory` table holds more specific product categories under a broader `Category`. It has a foreign key referencing `Category`.

```sql
CREATE TABLE Subcategory(
  subcategoryId INT AUTO_INCREMENT,
  categoryId INT NOT NULL,
  subcategory_name VARCHAR(30) NOT NULL,
  PRIMARY KEY(subcategoryId),
  FOREIGN KEY(categoryId) REFERENCES Category(categoryId)
);
```

### **Attributes:**
- `subcategoryId`: Unique identifier for the subcategory.
- `categoryId`: References the `Category` table.
- `subcategory_name`: Name of the subcategory (e.g., Office Chairs under Furniture).

## 5. **People Table**
The `People` table stores information about individuals involved in business processes, such as sales representatives.

```sql
CREATE TABLE People (
  Id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  region VARCHAR(40) NOT NULL,
  PRIMARY KEY(Id)
);
```

### **Attributes:**
- `Id`: Unique identifier for each person.
- `name`: Name of the individual.
- `region`: The region they work in.

## 6. **Products Table**
The `Products` table contains the details of products, such as product name and subcategory.

```sql
CREATE TABLE Products (
  productId VARCHAR(100),
  product_name VARCHAR(100),
  subcategory INT NOT NULL,
  PRIMARY KEY(productId),
  FOREIGN KEY(subcategory) REFERENCES Subcategory(subcategoryId)
);
```

### **Attributes:**
- `productId`: Unique identifier for each product.
- `product_name`: Name of the product.
- `subcategory`: References the `Subcategory` table.

## 7. **Location Table**
The `Location` table stores geographical information about locations. Each location is unique based on city, state, country, and market.

```sql
CREATE TABLE Location (
  locationId INT NOT NULL AUTO_INCREMENT,
  city VARCHAR(100) NOT NULL,
  state VARCHAR(100) NOT NULL,
  country VARCHAR(100) NOT NULL,
  market VARCHAR(40) NOT NULL,
  PRIMARY KEY(locationId),
  UNIQUE(city, state, country, market)
);
```

### **Attributes:**
- `locationId`: Unique identifier for each location.
- `city`: The city of the location.
- `state`: The state of the location.
- `country`: The country of the location.
- `market`: The specific market (e.g., North America).

## 8. **Orders Table**
The `Orders` table contains the orders placed by customers. It includes details like order date, shipping date, sales, profit, discount, quantity, and shipping cost.

```sql
CREATE TABLE Orders(
  orderId VARCHAR(100),
  customerId VARCHAR(100) NOT NULL,
  locationId INT NOT NULL,
  order_date DATE NOT NULL,
  ship_date DATE NOT NULL,
  sales DECIMAL(10,2) NOT NULL DEFAULT 0.0,
  profit DECIMAL(10,2) NOT NULL DEFAULT 0.0,
  discount DECIMAL(5,2) NOT NULL DEFAULT 0.0 CHECK (discount >= 0 AND discount <= 1),
  quantity INT NOT NULL DEFAULT 1 CHECK (quantity >= 1),
  shipping_cost DECIMAL(10,2) NOT NULL DEFAULT 0.0,
  PRIMARY KEY(orderId),
  FOREIGN KEY(customerId) REFERENCES Customer(customerId),
  FOREIGN KEY(locationId) REFERENCES Location(locationId)
);
```

### **Attributes:**
- `orderId`: Unique identifier for each order.
- `customerId`: References the `Customer` table.
- `locationId`: References the `Location` table.
- `order_date`: The date the order was placed.
- `ship_date`: The date the order was shipped.
- `sales`: The sales amount for the order.
- `profit`: The profit from the order.
- `discount`: The discount applied to the order.
- `quantity`: The number of items ordered.
- `shipping_cost`: The cost to ship the order.

## 9. **Returns Table**
The `Returns` table tracks returned items, referencing the `Orders` table.

```sql
CREATE TABLE Returns (
  orderId VARCHAR(100) NOT NULL,
  PRIMARY KEY(orderId),
  FOREIGN KEY(orderId) REFERENCES Orders(orderId)
);
```

### **Attributes:**
- `orderId`: References the `Orders` table, identifying which orders are being returned.

## Conclusion

This schema design organizes and defines the various entities in the Superstore KPI database. By following this schema, you can ensure consistent data storage, proper relationships between tables, and smooth querying for analytics purposes.
