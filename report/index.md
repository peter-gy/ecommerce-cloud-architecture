@import "./assets/tailwind.min.css"
@import "./node_modules/@shd101wyy/mume/styles/preview_theme/gothic.css"
@import ".mume/style.less"

# Cloud Architecture of an E-Commerce Platform

<div class="p-4 bg-blue-100 shadow-md rounded-md italic text-center">Submission of Péter Ferenc Gyarmati - a11913446</div>

## Application Overview

Selling products online is on the rise, however there is a significant entry-barrier for small and medium sized businesses to enter the market. The main reason for this is the high cost of setting up and maintaining an online store. This is where an e-commerce marketplace comes in. An e-commerce marketplace is a platform that allows vendors to list their products and buyers to purchase them. The marketplace takes a commission on each sale. This allows vendors to focus on their core business and buyers to have a wide variety of products to choose from while delegating the task of developing and maintaining the platform where the actual sales and logistics take place. The marketplace also provides a platform for vendors to advertise their products and buyers to find them and leave reviews. The information system I propose and design in this project aims to realise such an E-Commerce platform.

### Functional Requirements

- Customers can register and login to the system
- Vendors can register and list their products
- Vendors can promote their products for a period of time
- Customers can search for products and observe them in detail
- Customers can buy products
- Customers can choose from payment methods such as credit card, PayPal, and bank transfer
- Customers can leave ratings and reviews for products
- Customers can connect with vendors in built-in chat rooms

### Non-Functional Requirements

- The system should be highly available across the globe
- The system should have low latency to ensure a good user experience
- The system should be scalable to handle a large number of concurrent users
- The system should tolerate spikes in traffic (e.g. before Holidays, Black Friday, etc.)
- The system should be secure and protect customer and vendor data
- Data-loss should be prevented to maximize the satisfaction of customers and vendors

<div class="pagebreak"></div>

## Architecture Overview

In what follows, I will describe the logical architecture of the system using textual and UML-diagrammatic representations.

### Use Cases

To give a better impression of the system and its foreseen capabilities, I present a use case diagram in this section.

#### Actors

In the context of the proposed system, the below-described actors can be identified.

- **Admin**: An employee of the marketplace platform, responsible for admitting new vendors to the system and verifying that they represent a legitimate business.
- **Customer**: A user of the system who can buy products from vendors.
- **Vendor**: A user of the system who can list products for sale.
- **Payment Service Provider**: A third-party service that provides payment processing capabilities to the system.

#### Specifications

The specification of the diagrammed use cases are defined as follows.

##### Register as Customer

- **Description**: A customer can register to the system by providing their name, email address, and password.
- **Pre-conditions**: The customer is not registered to the system.
- **Post-conditions**: The customer is registered to the system.
- **Basic Flow**: The customer provides their name, email address, and password. The system verifies that the email address is not already registered to the system. If the email address is not registered, the system creates a new customer account and sends a verification email to the customer. The customer clicks on the verification link in the email and is redirected to the system. The system verifies the verification link and marks the customer as verified.
- **Alternative Flow**: If the email address is already registered to the system, the system notifies the customer and asks them to login or reset their password.
- **Involved Actors**: _Customer_

##### Register as Vendor

- **Description**: A vendor can register to the system by providing their name, email address, and password.
- **Pre-conditions**: The vendor is not registered to the system.
- **Post-conditions**: The vendor is registered to the system.
- **Basic Flow**: The vendor provides their name, email address, and password. The system verifies that the email address is not already registered to the system. If the email address is not registered, the system creates a new vendor account and sends a verification email to the vendor. The vendor clicks on the verification link in the email and is redirected to the system. The system verifies the verification link and marks the vendor as verified.
- **Alternative Flow**: If the email address is already registered to the system, the system notifies the vendor and asks them to login or reset their password.
- **Involved Actors**: _Vendor_

##### Login

- **Description**: A user can login to the system by providing their email address and password.
- **Pre-conditions**: The user is registered to the system.
- **Post-conditions**: The user is logged in to the system.
- **Basic Flow**: The user provides their email address and password. The system verifies that the email address is registered to the system and that the password is correct. If the email address and password are correct, the system logs the user in and redirects them to the home page.
- **Alternative Flow**: If the email address is not registered to the system, the system notifies the user and asks them to register. If the email address is registered to the system but the password is incorrect, the system notifies the user and asks them to try again.
- **Involved Actors**: _Customer_, _Vendor_

##### Vendor Verification

- **Description**: An admin verifies a vendor by checking their business information, before allowing them to list products for sale.
- **Pre-conditions**: The vendor is registered to the system and is not verified.
- **Post-conditions**: The vendor is verified and can list products for sale.
- **Basic Flow**: The admin verifies whether the business represented by the vendor is legitimate with the help of a pre-defined checklist. If the business is legitimate, the admin verifies the vendor and allows them to list products for sale.
- **Alternative Flow**: If the business is not legitimate, the admin rejects the vendor and notifies them of the reason.
- **Involved Actors**: _Admin_, _Vendor_

##### List Products for Sale

- **Description**: A vendor can list products for sale by providing their name, description, price, and images.
- **Pre-conditions**: The vendor is verified.
- **Post-conditions**: The vendor has listed a product for sale.
- **Basic Flow**: The vendor provides the product name, description, price, and images. The system verifies that the vendor is verified. If the vendor is verified, the system lists the product for sale.
- **Alternative Flow**: If the vendor is not verified, the system notifies the vendor and asks them to contact an admin.
- **Involved Actors**: _Vendor_

##### Promote Product

- **Description**: A vendor can promote a product for a period of time by paying a fee.
- **Pre-conditions**: The vendor is verified and has listed a product for sale.
- **Post-conditions**: The vendor has promoted a product for a period of time.
- **Basic Flow**: The vendor selects a product and specifies the duration of the promotion. The system verifies that the vendor is verified and that the product is listed for sale. If the vendor is verified and the product is listed for sale, the system charges the vendor's account and promotes the product for the specified duration.
- **Alternative Flow**: If the vendor is not verified, the system notifies the vendor and asks them to contact an admin. If the product is not listed for sale, the system notifies the vendor and asks them to list the product for sale.
- **Involved Actors**: _Vendor_

##### View Listed Products

- **Description**: A customer can view products listed for sale by vendors.
- **Pre-conditions**: The customer is logged in to the system.
- **Post-conditions**: The customer has viewed products listed for sale by vendors.
- **Basic Flow**: The customer selects a category and a sub-category. The system displays the products listed for sale in the selected category and sub-category.
- **Alternative Flow**: None.
- **Involved Actors**: _Customer_

##### Buy Products

- **Description**: A customer can buy products listed for sale by vendors.
- **Pre-conditions**: The customer is logged in to the system and has selected a product to buy.
- **Post-conditions**: The customer has bought a product.
- **Basic Flow**: The customer selects a product and specifies the quantity. The system verifies that the product is listed for sale and that the quantity is available. If the product is listed for sale and the quantity is available, the system charges the customer's account and delivers the product to the customer.
- **Alternative Flow**: If the selected quantity is not available, the system notifies the customer and asks them to select a different quantity.
- **Involved Actors**: _Customer_

##### Conduct Payment

- **Description**: A customer can conduct a payment by choosing one of the available payment methods: credit card, PayPal or bank transfer.
- **Pre-conditions**: The customer is logged in to the system and has selected a product to buy.
- **Post-conditions**: The customer has conducted a payment.
- **Basic Flow**: The customer selects a payment method and provides the required information. The system verifies that the payment method is supported by the vendor. If the payment method is supported, the system charges the customer's account and delivers the product to the customer.
- **Alternative Flow**: If the payment method is not supported, the system notifies the customer and asks them to select a different payment method.
- **Involved Actors**: _Customer_, _Payment Service Provider_

##### Leave Rating and Review

- **Description**: A customer can leave a rating and review for a product after buying it.
- **Pre-conditions**: The customer is logged in to the system and has bought a product.
- **Post-conditions**: The customer has left a rating and review for a product.
- **Basic Flow**: The customer selects a product and leaves a rating and review. The system verifies that the customer has bought the product. If the customer has indeed bought the product, the system saves the rating and review.
- **Alternative Flow**: If the customer has not bought the product, the system notifies the customer that leaving a rating and review is not allowed.
- **Involved Actors**: _Customer_

##### Chat with Vendor

- **Description**: A customer can chat with a vendor about a product.
- **Pre-conditions**: The customer is logged in to the system and has selected a product to buy.
- **Post-conditions**: The customer has chatted with a vendor
- **Basic Flow**: After a user buys a product from a vendor, the system puts the involved parties in a chat room. The customer and the vendor can chat with each other about the product, the delivery, or any other issue.
- **Alternative Flow**: None.
- **Involved Actors**: _Customer_, _Vendor_

@import "./diagrams/use-case.puml"

<div class="pagebreak"></div>

### Components

The component diagram presented below shows the components of the system and how they play together to achieve the information system's goals.

@import "./diagrams/component.puml"

<div class="pagebreak"></div>

## Applicable Cloud Patterns

### Vendor Agnostic Cloud Patterns

### Vendor Specific Cloud Patterns
