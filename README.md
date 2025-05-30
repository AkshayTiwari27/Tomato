# Tomato - Food Delivery System

**Tomato** is a modern C++ command-line application that simulates a food delivery system. It uses object-oriented design and popular design patterns to provide a modular, scalable architecture for features like restaurant search, order management, cart handling, and payment processing.

---

## 🚀 Features

* **User Management**: Simulates interactions between users and the system.
* **Restaurant Search**: Search based on location.
* **Menu Browsing**: Menus with item details and pricing.
* **Shopping Cart**: Add, update, and remove menu items.
* **Order Placement**: Supports "now" and scheduled orders.
* **Payment Options**: Uses Strategy Pattern to offer UPI and Credit Card payments.
* **Order Types**: Delivery and Pickup support.
* **Notifications**: Sends order status notifications.

---

## 🎯 Design Patterns Used

* **Facade Pattern**: `TomatoApp` centralizes user interaction and system orchestration.
* **Singleton Pattern**: `RestaurantManager` and `OrderManager` maintain a single instance throughout the application.
* **Strategy Pattern**: Enables multiple payment strategies via a common interface.
* **Abstract Factory Pattern**: Facilitates dynamic creation of order types (`NowOrderFactory`, `ScheduledOrderFactory`).

---

## 📁 Project Structure

```
OnlineFoodOrderingSystem/
├── main.cpp                    # Entry point
├── TomatoApp.h                # Facade class
│
├── models/
│   ├── MenuItem.h
│   ├── Restaurant.h
│   ├── User.h
│   ├── Cart.h
│   ├── Order.h
│   ├── DeliveryOrder.h
│   ├── PickupOrder.h
│
├── managers/
│   ├── RestaurantManager.h
│   ├── OrderManager.h
│
├── strategies/
│   ├── PaymentStrategy.h
│   ├── CreditCardPaymentStrategy.h
│   ├── UpiPaymentStrategy.h
│
├── factories/
│   ├── OrderFactory.h
│   ├── NowOrderFactory.h
│   ├── ScheduledOrderFactory.h
│
├── services/
│   └── NotificationService.h
│
├── utils/
│   └── TimeUtils.h
```

---

## 🛠 Getting Started

### Prerequisites

* C++11 or newer (GCC, Clang, MSVC)
* `make` (optional)

### Compilation

**Manual Compilation:**

```bash
g++ main.cpp -std=c++11 -o tomato_app
```

**Using Makefile:**

```makefile
CXX = g++
CXXFLAGS = -std=c++11 -Wall
TARGET = tomato_app
SOURCES = main.cpp # Add other .cpp files if created

all: $(TARGET)

$(TARGET): $(SOURCES)
	$(CXX) $(CXXFLAGS) -I./models -I./managers -I./strategies -I./factories -I./services -I./utils $(SOURCES) -o $(TARGET)

clean:
	rm -f $(TARGET)
```

```bash
make
```

### Run

```bash
./tomato_app
```

---

## 🔍 How It Works

1. **Initialization**

   * `TomatoApp::initializeRestaurants()` adds restaurants and menus.

2. **User Interaction**

   * Users search for restaurants → view menu → add items → choose order type.

3. **Checkout**

   * Select "now" or "scheduled" order.
   * Choose delivery or pickup option.
   * Select payment method (UPI / Credit Card).
   * Complete payment.

4. **Notification & Cleanup**

   * Successful order triggers a notification.
   * Cart is cleared.

---

## 🔮 Future Enhancements

* Persistent storage (files or databases).
* Advanced restaurant filtering (ratings, cuisine).
* User authentication and profile management.
* Live order tracking.
* Admin panel for restaurant management.
* Payment gateway integration.
* GUI or web interface.
* Testing suite with mocks and stubs.
* Robust error handling.

---

## 📌 Repository

[GitHub - Tomato](https://github.com/AkshayTiwari27/Tomato.git)

---

## 🧑‍💻 Author

**Akshay Tiwari**

Feel free to contribute or suggest improvements!
