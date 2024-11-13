---
title: Cpp - 常见设计模式
author: Boron
math: true
date: 2024-11-13 17:08:00 +0100
categories: [Blogs, Coding]
tags: [cpp, Coding]
---

设计模式是面向对象软件设计中常见的解决方案，它们提供了特定问题的最佳实践，帮助开发者构建更加灵活、可维护和可扩展的代码。下面我将介绍一些常见的编程模式，并通过具体案例来展示它们的细节和用处。

---

### **1. 单例模式（Singleton Pattern）**

- **概念**：确保一个类只有一个实例，并提供一个全局访问点来获取该实例。
- **用处**：当你需要确保某个类只有一个实例，且该实例需要被多个部分共享时使用。例如，数据库连接池、配置管理器等。

#### **实际案例**：数据库连接池

假设你有一个数据库连接池，你只希望在程序中有一个连接池实例，避免重复创建连接池对象。

```cpp
class DatabaseConnection {
public:
    static DatabaseConnection* getInstance() {
        if (instance == nullptr) {
            instance = new DatabaseConnection();
        }
        return instance;
    }
    void connect() {
        // 连接数据库的代码
    }
private:
    DatabaseConnection() {}  // 私有构造函数
    static DatabaseConnection* instance;
};
DatabaseConnection* DatabaseConnection::instance = nullptr;
int main() {
    DatabaseConnection* db = DatabaseConnection::getInstance();
    db->connect();
    return 0;
}
```

- **优点**：避免了多次创建对象，节省资源，保证系统的一致性。
- **应用场景**：用于共享资源的管理，如日志记录、配置管理、数据库连接等。

---

### **2. 工厂模式（Factory Pattern）**

- **概念**：提供一个创建对象的接口，让子类决定实例化哪个类。通过工厂类来创建对象，而不是在客户端代码中直接创建。
- **用处**：当你需要根据不同的条件创建不同类型的对象，而又不希望将对象的创建过程暴露给客户端时，可以使用工厂模式。

#### **实际案例**：图形界面（GUI）按钮的工厂

假设你在开发一个跨平台的应用，支持 Windows 和 Linux 系统。你可以使用工厂模式来创建不同操作系统下的按钮。

```cpp
class Button {
public:
    virtual void render() = 0;
};
class WindowsButton : public Button {
public:
    void render() override {
        std::cout << "Render Windows Button" << std::endl;
    }
};
class LinuxButton : public Button {
public:
    void render() override {
        std::cout << "Render Linux Button" << std::endl;
    }
};
class ButtonFactory {
public:
    static Button* createButton(const std::string& os) {
        if (os == "Windows") {
            return new WindowsButton();
        } else if (os == "Linux") {
            return new LinuxButton();
        }
        return nullptr;
    }
};
int main() {
    Button* button = ButtonFactory::createButton("Windows");
    button->render();
    delete button;
    return 0;
}
```

- **优点**：客户端不需要知道具体的类，实现了对象创建过程的解耦。
- **应用场景**：用于根据不同条件选择实例化不同对象的场景，如数据库连接、跨平台 GUI 等。

---

### **3. 观察者模式（Observer Pattern）**

- **概念**：当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并自动更新。实现对象之间的一对多依赖关系。
- **用处**：当一个对象的状态变化需要同时更新多个对象时，使用观察者模式，例如事件监听、UI 更新等。

#### **实际案例**：股票价格监控系统

假设你在开发一个股票价格监控系统，当股票价格变化时，需要通知多个不同的监听器（如图表、日志、通知系统等）。

```cpp
#include <iostream>
#include <vector>
class Observer {
public:
    virtual void update(float price) = 0;
};
class StockPrice : public Observer {
public:
    void update(float price) override {
        std::cout << "Stock price updated: " << price << std::endl;
    }
};
class Stock {
private:
    float price;
    std::vector<Observer*> observers;
public:
    void addObserver(Observer* observer) {
        observers.push_back(observer);
    }
    void setPrice(float newPrice) {
        price = newPrice;
        notifyObservers();
    }
    void notifyObservers() {
        for (Observer* observer : observers) {
            observer->update(price);
        }
    }
};
int main() {
    Stock stock;
    StockPrice stockPrice;
    stock.addObserver(&stockPrice);
    stock.setPrice(100.5f);  // 通知所有观察者价格更新
    return 0;
}
```

- **优点**：支持松耦合的组件之间的交互，便于扩展和维护。
- **应用场景**：用于事件驱动系统、UI 更新、实时数据推送等。

---

### **4. 策略模式（Strategy Pattern）**

- **概念**：定义一系列算法，将它们封装起来，并使它们可以互相替换。客户端可以选择不同的算法而无需修改代码。
- **用处**：当你有多个算法或者策略可以选择时，策略模式可以让你将这些算法封装起来，使得它们可以独立变化而不影响其他部分。

#### **实际案例**：排序策略

假设你需要根据不同的条件来选择不同的排序算法。使用策略模式可以将排序算法封装到策略类中。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
class SortStrategy {
public:
    virtual void sort(std::vector<int>& data) = 0;
};
class BubbleSort : public SortStrategy {
public:
    void sort(std::vector<int>& data) override {
        std::cout << "Bubble sorting..." << std::endl;
        std::sort(data.begin(), data.end());  // 简单的排序实现
    }
};
class QuickSort : public SortStrategy {
public:
    void sort(std::vector<int>& data) override {
        std::cout << "Quick sorting..." << std::endl;
        std::sort(data.begin(), data.end());  // 简单的排序实现
    }
};
class SortContext {
private:
    SortStrategy* strategy;
public:
    SortContext(SortStrategy* strategy) : strategy(strategy) {}
    void setStrategy(SortStrategy* newStrategy) {
        strategy = newStrategy;
    }
    void sortData(std::vector<int>& data) {
        strategy->sort(data);
    }
};
int main() {
    std::vector<int> data = {4, 2, 5, 1, 3};
    SortContext context(new BubbleSort());
    context.sortData(data);
    context.setStrategy(new QuickSort());
    context.sortData(data);
    return 0;
}
```

- **优点**：可以根据需要动态地改变算法，减少了条件语句的使用。
- **应用场景**：用于实现多个算法之间的选择，如支付方式、策略选择、排序算法等。

---

### **5. 状态模式（State Pattern）**

- **概念**：允许对象在其内部状态改变时改变其行为。状态模式将对象的行为与状态之间的关系封装。
- **用处**：当对象的行为依赖于它的状态，并且根据不同的状态改变时，使用状态模式可以避免大量的条件语句。

#### **实际案例**：文档编辑器的状态管理

假设一个文档编辑器有多个状态（如草稿、审核中、发布），不同状态下的操作可能会有所不同。

```cpp
#include <iostream>
class State {
public:
    virtual void handle() = 0;
};
class DraftState : public State {
public:
    void handle() override {
        std::cout << "Document is in Draft state." << std::endl;
    }
};
class ReviewState : public State {
public:
    void handle() override {
        std::cout << "Document is under review." << std::endl;
    }
};
class PublishedState : public State {
public:
    void handle() override {
        std::cout << "Document is published." << std::endl;
    }
};
class Document {
private:
    State* state;
public:
    Document(State* initialState) : state(initialState) {}
    void setState(State* newState) {
        state = newState;
    }
    void publish() {
        state->handle();
    }
};
int main() {
    Document doc(new DraftState());
    doc.publish();
    doc.setState(new ReviewState());
    doc.publish();
    doc.setState(new PublishedState());
    doc.publish();
    return 0;
}
```

- **优点**：避免了大量的条件判断语句，行为随着状态变化而改变，代码更加清晰。
- **应用场景**：用于状态转移系统，如工作流管理、游戏角色状态、订单管理等。

---

### **总结**

编程模式通过为常见的编程问题提供已验证的解决方案，帮助开发者提高代码的复用性、可维护性和扩展性。通过使用适当的设计模式，我们能够减少复杂的条件判断，简化代码结构，使代码更加清晰和易于理解。
一些常见的编程
模式，如**单例模式**、**工厂模式**、**观察者模式**、**策略模式**和**状态模式**，在实际项目中都有广泛的应用。通过这些模式的合理应用，开发者可以更好地管理系统复杂性，减少代码重复，增强系统的可扩展性。
