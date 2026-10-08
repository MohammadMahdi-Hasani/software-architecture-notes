# Software Architecture Notes 🏗️

My notes, practical exercises, and Python implementations while studying **Software Architecture**, **Architecture Patterns**, and **Design Patterns**.

The goal of this repository is not only to memorize patterns, but to understand **when to use them, why to use them, and what trade-offs they introduce**.

---

## 📚 Topics

### Architecture Styles

High-level approaches for organizing the structure of a software system.

* [Layered Architecture](./architecture-styles/layered-architecture.md)
* [Event-Driven Architecture](./architecture-styles/event-driven-architecture.md)
* [Microservices Architecture](./architecture-styles/microservices.md)
* [Client-Server Architecture](./architecture-styles/client-server.md)

### Architecture Patterns

Reusable solutions for common problems at the architectural level.

* [API Gateway](./architecture-patterns/api-gateway.md)
* [CQRS](./architecture-patterns/cqrs.md)
* [Saga](./architecture-patterns/saga.md)

### Design Patterns

Reusable solutions for common software design problems at the class and object level.

* [Factory](./design-patterns/factory.md)
* [Strategy](./design-patterns/strategy.md)
* [Observer](./design-patterns/observer.md)

---

## 🧠 Mental Model

A simple way to think about the different levels of abstraction:

```text
Architecture Style
        ↓
Architecture Pattern
        ↓
Design Pattern
        ↓
Implementation
        ↓
Code
```

For example:

```text
Microservices
      ↓
API Gateway / CQRS / Saga
      ↓
Factory / Strategy / Observer
      ↓
Python Classes
```

> The exact terminology and categorization can vary between books and authors.
> The purpose of this repository is to build a practical mental model for understanding the different levels of software design.

---

## 🧪 Practical Exercises

The concepts are reinforced through hands-on Python exercises.

```text
exercises/
├── layered/
├── event-driven/
└── microservices/
```

Each exercise will focus on applying architectural concepts in a small, practical project.

---

## 📖 Main Reference

The main reference for the architecture studies in this repository is:

**Software Architecture Patterns — Mark Richards**

Additional references will be added as the repository evolves.

---

## 🎯 Goal

The goal is to move from:

> **"I know what this pattern is."**

to:

> **"I understand when to use it, when not to use it, and what trade-offs it introduces."**

---

## 🚧 Status

This repository is a work in progress and will grow as I continue studying and implementing software architecture concepts with Python.
