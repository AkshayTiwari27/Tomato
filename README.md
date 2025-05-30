# Tomato - Food Delivery System

Tomato is a C++ command-line application that simulates a food delivery system. It allows users to search for restaurants, add items to a cart, checkout, and process payments. The system is designed with a focus on object-oriented principles and common design patterns.

## Features

* **User Management:** Simulates a user interacting with the system.
* **Restaurant Search:** Users can search for restaurants based on location.
* **Menu Browsing:** Restaurants have menus with items and prices.
* **Shopping Cart:** Users can add and manage items in their cart.
* **Order Placement:** Supports both immediate ("now") and scheduled delivery/pickup orders.
* **Multiple Payment Options:** Implemented using a strategy pattern, supporting UPI and Credit Card payments.
* **Order Types:** Supports both Delivery and Pickup orders.
* **Notifications:** Simulates notifications for placed orders.

## Design Patterns Used

This project demonstrates several design patterns:

* **Facade Pattern:** The `TomatoApp` class acts as a facade, providing a simplified interface to the complex underlying system.
* **Singleton Pattern:** `RestaurantManager` and `OrderManager` are implemented as singletons to ensure a single instance manages all restaurants and orders respectively.
* **Strategy Pattern:** The `PaymentStrategy` interface allows for different payment methods (e.g., `CreditCardPaymentStrategy`, `UpiPaymentStrategy`) to be used interchangeably.
* **Factory Pattern (Abstract Factory):** `OrderFactory` is an abstract factory for creating different types of orders (`NowOrderFactory`, `ScheduledOrderFactory`). This allows for the creation of order objects without specifying the exact class of object that will be created.

## Folder Structure

The project follows a structured organization to separate concerns:


OnlineFoodOrderingSystem/
│
├── main.cpp                    # Composition root and entry point
├── TomatoApp.h                # Facade class (main orchestrator)
│
├── models/                     # Contains the data structures
│   ├── MenuItem.h
│   ├── Restaurant.h
│   ├── User.h
│   ├── Cart.h
│   ├── Order.h                # Abstract Order
│   ├── DeliveryOrder.h
│   ├── PickupOrder.h
│
├── managers/                   # Contains manager classes for models
│   ├── RestaurantManager.h
│   ├── OrderManager.h
│
├── strategies/                 # Contains different strategies (e.g., for payment)
│   ├── PaymentStrategy.h      # Base class
│   ├── CreditCardPaymentStrategy.h
│   ├── UpiPaymentStrategy.h
│
├── factories/                  # Contains factory classes for object creation
│   ├── OrderFactory.h         # Abstract factory
│   ├── NowOrderFactory.h
│   ├── ScheduledOrderFactory.h
│
├── services/                   # Contains service classes (e.g., notification)
│   └── NotificationService.h
│
├── utils/                      # Utility classes
│   └── TimeUtils.h


## Getting Started

### Prerequisites

* A C++ compiler that supports C++11 or later (e.g., GCC, Clang, MSVC).
* Make (Optional, but recommended for easier compilation).

### Compilation and Execution

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd <repository-directory>/OnlineFoodOrderingSystem
    ```

2.  **Compile the code:**
    You can compile the `main.cpp` file along with other necessary `.h` files. A simple way to compile all (assuming all .cpp files are in the root or you adjust paths):
    ```bash
    g++ main.cpp -std=c++11 -o tomato_app 
    ```
    *(Note: The command above assumes that all necessary header files are correctly included in `main.cpp` and other relevant files, and that the compiler can find them. For a project of this structure, you would typically compile by listing all `.cpp` source files if you had separate implementations. However, based on the provided files, most logic seems to be within header files or `main.cpp`. If you create separate `.cpp` files for your classes, you'll need to include them in the compilation command, e.g., `g++ main.cpp models/User.cpp ... -o tomato_app` or use a build system like Make or CMake.)*

    **Example using Make (create a `Makefile`):**
    ```makefile
    CXX = g++
    CXXFLAGS = -std=c++11 -Wall
    TARGET = tomato_app
    SOURCES = main.cpp # Add other .cpp files if you create them e.g., models/User.cpp

    all: $(TARGET)

    $(TARGET): $(SOURCES)
    	$(CXX) $(CXXFLAGS) -I./models -I./managers -I./strategies -I./factories -I./services -I./utils $(SOURCES) -o $(TARGET)

    clean:
    	rm -f $(TARGET)
    ```
    Then run:
    ```bash
    make
    ```

3.  **Run the application:**
    ```bash
    ./tomato_app
    ```

    The `main.cpp` file contains a simulation of a user interacting with the system, demonstrating the core functionalities.

## How it Works

1.  **Initialization (`TomatoApp::initializeRestaurants`)**:
    * Several sample restaurants with their menus are created and added to the `RestaurantManager`.

2.  **User Interaction (`main.cpp`)**:
    * A `User` object is created.
    * The user searches for restaurants by location using `TomatoApp::searchRestaurants`.
    * The user selects a restaurant.
    * Items are added to the user's cart (`TomatoApp::addToCart`).
    * The user checks out the cart (`TomatoApp::checkoutNow` or `TomatoApp::checkoutScheduled`).
        * An `OrderFactory` (either `NowOrderFactory` or `ScheduledOrderFactory`) creates the appropriate `Order` object (`DeliveryOrder` or `PickupOrder`).
        * A `PaymentStrategy` (e.g., `UpiPaymentStrategy`) is chosen.
    * The user pays for the order (`TomatoApp::payForOrder`).
        * If payment is successful, a notification is sent via `NotificationService`, and the user's cart is cleared.

## Future Enhancements

* Persistent storage for users, restaurants, and orders (e.g., using files or a database).
* More sophisticated search and filtering options for restaurants.
* User authentication and accounts.
* Real-time order tracking.
* Admin interface for managing restaurants and users.
* Integration with actual payment gateways.
* A graphical user interface (GUI) or web interface.
* Comprehensive unit and integration tests.
* Improved error handling and input validation.
