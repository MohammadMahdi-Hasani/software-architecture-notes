# 🏢 Architecture Style vs. Architecture Pattern vs. Design Pattern

وقتی درباره‌ی **Software Architecture** صحبت می‌کنیم، خیلی زود با اصطلاحاتی مثل:

* Architecture Style
* Architecture Pattern
* Design Pattern
* Microservices
* Layered Architecture
* CQRS
* Factory
* Observer

مواجه می‌شویم.

مشکل از جایی شروع می‌شود که این اصطلاحات را در منابع مختلف با مرزهای متفاوتی تعریف می‌کنند. برای مثال، گاهی **Microservices** را یک Architecture Style می‌دانند، گاهی یک Architecture Pattern یا یک Architectural Approach. همچنین اصطلاحاتی مثل **CQRS، Saga و API Gateway** در منابع مختلف ممکن است در دسته‌بندی‌های متفاوتی قرار بگیرند.

بنابراین هدف این مقاله این نیست که یک دسته‌بندی «تنها و قطعی» ارائه دهد؛ بلکه می‌خواهیم یک **مدل ذهنی ساده و کاربردی** بسازیم تا بتوانیم تفاوت این مفاهیم را در طراحی سیستم درک کنیم.

به ساده‌ترین شکل:

```text
Architecture Style
        ↓
Architecture Pattern
        ↓
Design Pattern
        ↓
Code
```

یعنی هرچه پایین‌تر می‌آییم، از **تصمیم‌های بزرگ و سیستمی** به سمت **تصمیم‌های جزئی‌تر و نزدیک‌تر به کد** حرکت می‌کنیم.

---

# 🗺️ یک نگاه کلی

فرض کنید می‌خواهیم یک فروشگاه آنلاین طراحی کنیم.

در طول طراحی ممکن است تصمیم‌های زیر را بگیریم:

```text
کل سیستم چگونه ساخته شود؟
        ↓
Microservices

مشکل ارتباط و هماهنگی سرویس‌ها چگونه حل شود؟
        ↓
API Gateway / Saga / CQRS

داخل یک سرویس، منطق کد چگونه طراحی شود؟
        ↓
Factory / Strategy / Observer

در نهایت چه کلاسی داشته باشیم؟
        ↓
Python Classes
```

نکته‌ی اصلی این است:

> **این مفاهیم رقیب یکدیگر نیستند؛ در سطوح مختلف تصمیم‌گیری قرار دارند.**

---

# 1. 🏙️ Architecture Style

## Architecture Style چیست؟

**Architecture Style** یک نگاه سطح‌بالا به ساختار و نحوه‌ی سازمان‌دهی یک سیستم نرم‌افزاری است.

در این سطح هنوز وارد جزئیات کلاس‌ها، Interfaceها یا الگوریتم‌ها نشده‌ایم.

سؤال اصلی این است:

> «ساختار کلی سیستم من چگونه باشد؟»

برای مثال می‌توانیم بگوییم:

* سیستم لایه‌ای باشد.
* سیستم به چند سرویس مستقل تقسیم شود.
* سیستم مبتنی بر رویداد باشد.
* کل سیستم به صورت یک واحد deploy شود.
* سیستم Client/Server باشد.

### نمونه‌ها

```text
Layered
Client-Server
Monolithic
Microservices
Event-Driven
Service-Oriented
```

البته یک نکته‌ی مهم وجود دارد:

> اصطلاحات بالا در منابع مختلف ممکن است به‌عنوان Style، Architecture Pattern، Architecture یا Architectural Approach دسته‌بندی شوند.

آنچه مهم‌تر از اسم دسته‌بندی است، **سطح تصمیمی است که آن مفهوم روی آن اثر می‌گذارد**.

---

## 🎯 Scope در Architecture Style

Architecture Style معمولاً روی کل سیستم اثر می‌گذارد.

مثلاً اگر بگوییم:

```text
Microservices
```

یعنی ساختار سیستم ما احتمالاً چیزی شبیه این خواهد بود:

```text
              ┌─────────────┐
              │   Client    │
              └──────┬──────┘
                     │
                     ▼
              ┌─────────────┐
              │ API Gateway │
              └──────┬──────┘
                     │
       ┌─────────────┼─────────────┐
       ▼             ▼             ▼
┌────────────┐ ┌────────────┐ ┌────────────┐
│   Order    │ │  Payment   │ │ Inventory  │
│  Service   │ │  Service   │ │  Service   │
└────────────┘ └────────────┘ └────────────┘
```

این تصمیم روی deployment، communication، ownership و boundaries سیستم تأثیر می‌گذارد.

---

# 2. 🧩 Architecture Pattern

## Architecture Pattern چیست؟

حالا فرض کنید Architecture Style خود را انتخاب کرده‌ایم.

مثلاً:

```text
Microservices
```

اما حالا با مشکلات واقعی معماری مواجه می‌شویم:

* سرویس‌ها چگونه با هم ارتباط برقرار کنند؟
* درخواست‌ها چگونه به سرویس مناسب برسند؟
* تراکنش بین چند سرویس چگونه مدیریت شود؟
* خواندن و نوشتن چگونه از هم جدا شوند؟
* خطای یک سرویس چگونه روی سایر سرویس‌ها کنترل شود؟

اینجاست که **Architecture Pattern** یا الگوهای معماری وارد می‌شوند.

به‌صورت ساده:

> **Architecture Pattern یک راه‌حل قابل تکرار برای یک مشکل در سطح معماری است.**

این راه‌حل از Design Patternها بزرگ‌تر است، چون با مجموعه‌ای از Componentها، Serviceها، Data Flowها یا Communicationها سروکار دارد.

---

## مثال: API Gateway

فرض کنیم یک سیستم Microservices داریم:

```text
Client
  |
  ├── Order Service
  ├── Payment Service
  ├── Inventory Service
  └── User Service
```

اگر Client بخواهد مستقیماً با همه‌ی این سرویس‌ها ارتباط برقرار کند، پیچیدگی زیادی ایجاد می‌شود.

می‌توانیم یک Gateway در مقابل آن‌ها قرار دهیم:

```text
             Client
                |
                ▼
         ┌─────────────┐
         │ API Gateway │
         └──────┬──────┘
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
    Order    Payment  Inventory
```

در اینجا API Gateway یک تصمیم در سطح معماری است، نه صرفاً یک کلاس درون برنامه.

---

# 3. 🧠 Design Pattern

حالا وارد داخل یکی از سرویس‌ها شویم.

فرض کنیم در `Payment Service` چند روش پرداخت داریم:

```text
Credit Card
PayPal
Bank Transfer
Wallet
```

یک راه ساده این است که کد را با تعداد زیادی `if/else` بنویسیم:

```python
if payment_type == "card":
    ...
elif payment_type == "paypal":
    ...
elif payment_type == "wallet":
    ...
```

اما با بزرگ‌تر شدن سیستم این کد می‌تواند پیچیده و سخت‌نگهداری شود.

اینجا می‌توانیم از **Design Pattern** استفاده کنیم.

مثلاً:

```text
Factory
Strategy
Adapter
Observer
Decorator
Command
```

---

# 🧱 Design Pattern دقیقاً چه چیزی را حل می‌کند؟

Design Patternها معمولاً به مشکلاتی مربوط هستند که در سطح:

* Class
* Object
* Interface
* Responsibility
* Collaboration

اتفاق می‌افتند.

مثلاً Strategy Pattern می‌گوید:

> الگوریتم‌های مختلف را از هم جدا کن تا بتوانی آن‌ها را قابل تعویض کنی.

در Python می‌توانیم چیزی شبیه این داشته باشیم:

```python
from abc import ABC, abstractmethod


class PaymentStrategy(ABC):

    @abstractmethod
    def pay(self, amount: float) -> None:
        pass


class CreditCardPayment(PaymentStrategy):

    def pay(self, amount: float) -> None:
        print(f"Paying {amount} with credit card")


class WalletPayment(PaymentStrategy):

    def pay(self, amount: float) -> None:
        print(f"Paying {amount} with wallet")
```

در اینجا هنوز درباره‌ی کل معماری سیستم صحبت نمی‌کنیم.

فقط داریم **نحوه‌ی همکاری چند کلاس** را طراحی می‌کنیم.

---

# 4. 💻 Code

در پایین‌ترین سطح، همه‌ی تصمیم‌های قبلی در نهایت تبدیل به کد می‌شوند.

برای مثال:

```python
class CreditCardPayment:
    def pay(self, amount):
        pass


class WalletPayment:
    def pay(self, amount):
        pass


class PaymentService:
    def process(self, payment):
        payment.pay()
```

این دیگر خود Pattern نیست؛

این **پیاده‌سازی Pattern** است.

این تمایز بسیار مهم است:

> **Factory Pattern یک ایده است؛ `PaymentFactory` یک پیاده‌سازی از آن ایده در کد است.**

---

# 🧭 یک مدل ذهنی ساده

برای درک بهتر، سیستم را مانند یک شهر در نظر بگیرید.

```text
🏙️ City
   ↓
Architecture Style

🏘️ نحوه‌ی تقسیم مناطق و خیابان‌ها
   ↓
Architecture Patterns

🏠 نقشه‌ی ساخت ساختمان
   ↓
Design Patterns

🧱 آجر، دیوار، در و پنجره
   ↓
Code
```

یعنی:

### Architecture Style

می‌گوید:

> شهر من چگونه سازمان‌دهی شود؟

### Architecture Pattern

می‌گوید:

> یک مشکل مشخص در این شهر را چگونه حل کنم؟

### Design Pattern

می‌گوید:

> یک ساختمان یا بخشی از آن چگونه طراحی شود؟

### Code

می‌گوید:

> در نهایت دقیقاً چه چیزی بسازم؟

---

# 📊 تفاوت‌ها در یک نگاه

| ویژگی     | Architecture Style             | Architecture Pattern                       | Design Pattern                 |
| --------- | ------------------------------ | ------------------------------------------ | ------------------------------ |
| سطح       | کل سیستم                       | سطح معماری و Componentها                   | Class و Object                 |
| سؤال اصلی | سیستم چگونه سازمان‌دهی شود؟    | یک مشکل معماری چگونه حل شود؟               | یک مشکل طراحی کد چگونه حل شود؟ |
| Scope     | بسیار بزرگ                     | متوسط تا بزرگ                              | کوچک‌تر                        |
| تمرکز     | Structure و Communication کلان | Interaction و Responsibility در سطح معماری | Collaboration بین Objects      |
| مثال      | Layered, Microservices         | API Gateway, CQRS, Saga                    | Factory, Strategy, Adapter     |
| اثر       | کل سیستم                       | بخش‌های اصلی سیستم                         | بخشی از کد                     |

---

# 🔥 حالا همه را کنار هم ببینیم

فرض کنید می‌خواهیم یک سیستم E-Commerce طراحی کنیم.

## مرحله‌ی اول: Architecture Style

تصمیم می‌گیریم سیستم از چند سرویس تشکیل شود:

```text
Microservices
```

ساختار کلی:

```text
              Client
                 |
                 ▼
           API Gateway
                 |
      ┌──────────┼──────────┐
      ▼          ▼          ▼
    Order     Payment    Inventory
   Service     Service     Service
```

---

## مرحله‌ی دوم: Architecture Pattern

حالا با مسائل معماری مواجهیم.

مثلاً:

### API Gateway

برای مدیریت ورودی سیستم:

```text
Client
  ↓
API Gateway
  ↓
Services
```

### CQRS

برای جدا کردن عملیات خواندن و نوشتن:

```text
             Order
               |
        ┌──────┴──────┐
        ▼             ▼
      Write          Read
       Side          Side
```

### Saga

برای هماهنگ کردن یک عملیات توزیع‌شده بین چند سرویس:

```text
Order
  ↓
Payment
  ↓
Inventory
  ↓
Shipping
```

اگر یکی از مراحل شکست بخورد، سیستم باید بتواند عملیات‌های قبلی را جبران کند یا وضعیت مناسب ایجاد کند.

---

# مرحله‌ی سوم: Design Pattern

حالا وارد یکی از سرویس‌ها می‌شویم.

فرض کنید:

```text
Payment Service
```

برای پرداخت از Strategy استفاده می‌کنیم:

```text
PaymentStrategy
      │
      ├── CreditCardPayment
      ├── WalletPayment
      └── BankTransferPayment
```

و برای ساخت Strategy مناسب می‌توانیم از Factory استفاده کنیم:

```text
PaymentFactory
      │
      ├── CreditCardPayment
      ├── WalletPayment
      └── BankTransferPayment
```

یعنی ممکن است در یک معماری واقعی، چند لایه از این مفاهیم را هم‌زمان داشته باشیم.

---

# 🤯 چرا این مفاهیم این‌قدر با هم قاطی می‌شوند؟

دلیل اصلی این است که در دنیای واقعی مرز آن‌ها همیشه کاملاً مشخص نیست.

مثلاً:

* بعضی منابع Microservices را Architecture Style می‌نامند.
* بعضی منابع آن را Architecture Pattern می‌دانند.
* بعضی منابع CQRS را Architectural Pattern می‌دانند.
* بعضی منابع آن را Architectural Pattern یا Design Approach معرفی می‌کنند.
* بعضی مفاهیم نیز در یک پروژه می‌توانند از چند زاویه دیده شوند.

بنابراین نباید بیش از حد درگیر اسم دسته‌بندی شویم.

چیزی که مهم‌تر است این است که بدانیم:

> **این تصمیم در چه سطحی گرفته می‌شود و چه نوع مشکلی را حل می‌کند؟**

---

# 🎯 یک روش ساده برای تشخیص

وقتی با یک Pattern یا مفهوم جدید مواجه شدید، سه سؤال از خودتان بپرسید.

### سؤال اول:

> آیا این تصمیم روی ساختار کل سیستم اثر می‌گذارد؟

اگر بله، احتمالاً با یک **Architecture Style / Architectural Approach** طرف هستیم.

مثلاً:

```text
Layered
Microservices
Event-Driven
```

---

### سؤال دوم:

> آیا این مفهوم یک مشکل در سطح Serviceها، Componentها یا ارتباط بین بخش‌های بزرگ سیستم را حل می‌کند؟

اگر بله، احتمالاً در قلمرو **Architecture Pattern** هستیم.

مثلاً:

```text
API Gateway
Saga
CQRS
```

---

### سؤال سوم:

> آیا این مفهوم بیشتر درباره‌ی همکاری Classها و Objectهاست؟

اگر بله، احتمالاً یک **Design Pattern** است.

مثلاً:

```text
Factory
Strategy
Observer
Adapter
Decorator
```

---

# 🧩 یک مثال واقعی‌تر با Python

فرض کنیم یک E-Commerce داریم.

در سطح معماری:

```text
Microservices
```

سرویس‌ها:

```text
Order Service
Payment Service
Inventory Service
Notification Service
```

در سطح معماری ممکن است بگوییم:

```text
API Gateway
Event-Driven Communication
Saga
```

و داخل `Payment Service` بگوییم:

```text
Strategy
Factory
Adapter
```

در نهایت کدی شبیه این داریم:

```python
class PaymentStrategy:
    def pay(self, amount):
        raise NotImplementedError


class CreditCardPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Charging {amount} with credit card")


class WalletPayment(PaymentStrategy):
    def pay(self, amount):
        print(f"Charging {amount} from wallet")


class PaymentFactory:

    @staticmethod
    def create(method: str) -> PaymentStrategy:
        if method == "card":
            return CreditCardPayment()

        if method == "wallet":
            return WalletPayment()

        raise ValueError("Unsupported payment method")
```

این کد فقط بخش کوچکی از سیستم است.

Architecture کل سیستم چیز بزرگ‌تری است:

```text
                 Architecture
                       │
        ┌──────────────┴──────────────┐
        │                             │
Architecture Style            Architecture Patterns
        │                             │
  Microservices              API Gateway / Saga / CQRS
        │
        ▼
    Services
        │
        ▼
  Design Patterns
        │
 Strategy / Factory / Adapter
        │
        ▼
       Code
```

---

# ⚠️ یک اشتباه رایج

بعضی وقت‌ها وقتی کسی Design Pattern یاد می‌گیرد، تصور می‌کند که با یاد گرفتن:

```text
Factory
Strategy
Observer
Singleton
Adapter
```

در حال یادگیری Software Architecture است.

در حالی که این‌ها فقط بخشی از تصویر هستند.

همان‌طور که بلد بودن `Adapter Pattern` به این معنی نیست که می‌توانیم یک Microservices System طراحی کنیم، بلد بودن `Factory` هم به این معنی نیست که می‌دانیم چه زمانی باید سیستم را به Microservice تبدیل کنیم.

در Architecture، سؤالات بزرگ‌تری مطرح می‌شوند:

```text
چطور سیستم را به مرزهای مناسب تقسیم کنم؟

کدام Componentها باید مستقل باشند؟

داده کجا نگهداری شود؟

Communication بین سرویس‌ها چگونه باشد؟

چه میزان Coupling قابل قبول است؟

Consistency را چگونه مدیریت کنم؟

چه چیزی باید Scale شود؟

Failure در کجا اتفاق می‌افتد؟

Deployment Boundary کجاست؟
```

این‌ها دیگر صرفاً سؤال‌های Design Pattern نیستند.

---

# 🧠 مهم‌ترین تفاوت: Level of Abstraction

اگر بخواهیم تمام مقاله را در یک نمودار خلاصه کنیم:

```text
                HIGH ABSTRACTION
                       │
                       ▼
              ┌─────────────────┐
              │ Architecture    │
              │     Style       │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Architecture    │
              │     Pattern     │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Design Pattern  │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │      Code       │
              └─────────────────┘
                       │
                       ▼
                LOW ABSTRACTION
```

هرچه به سمت بالا می‌رویم، درباره‌ی:

```text
System
Components
Communication
Boundaries
Deployment
```

بیشتر صحبت می‌کنیم.

هرچه به سمت پایین می‌آییم، درباره‌ی:

```text
Classes
Objects
Methods
Interfaces
```

بیشتر صحبت می‌کنیم.

---

# 🏁 جمع‌بندی

می‌توانیم این سه مفهوم را خیلی ساده این‌طور به خاطر بسپاریم:

### Architecture Style

> **سیستم من در مقیاس بزرگ چه شکلی باشد؟**

مثلاً:

```text
Layered
Microservices
Event-Driven
```

---

### Architecture Pattern

> **یک مشکل مهم معماری را چگونه حل کنم؟**

مثلاً:

```text
API Gateway
Saga
CQRS
```

---

### Design Pattern

> **یک مشکل تکرارشونده در طراحی کد را چگونه حل کنم؟**

مثلاً:

```text
Factory
Strategy
Observer
Adapter
```

---

و در نهایت:

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

پس وقتی در یک پروژه می‌بینیم:

```text
Microservices
        ↓
API Gateway
        ↓
Payment Service
        ↓
Factory + Strategy
        ↓
Python Classes
```

این‌ها با یکدیگر تناقض ندارند.

برعکس، می‌توانند **لایه‌های مختلف یک تصمیم طراحی واحد** باشند.

> **Architecture مشخص می‌کند سیستم چگونه سازمان‌دهی شود؛
> Architecture Patterns به حل مشکلات معماری کمک می‌کنند؛
> Design Patterns به حل مشکلات طراحی کد کمک می‌کنند؛
> و در نهایت همه‌ی این تصمیم‌ها در Code پیاده‌سازی می‌شوند.**

---

## 📚 یک نکته‌ی پایانی

نباید هدف یادگیری Architecture این باشد که فقط بتوانیم نام Patternهای زیادی را حفظ کنیم.

هدف اصلی این است که بتوانیم برای یک مسئله بگوییم:

> «این تصمیم در چه سطحی قرار دارد؟ چه مشکلی را حل می‌کند؟ چه Trade-offهایی دارد؟ و چرا این راه‌حل را به گزینه‌های دیگر ترجیح می‌دهم؟»

این دقیقاً همان جایی است که **Software Architecture** از صرفاً بلد بودن چند Design Pattern جدا می‌شود.

---

## 📖 References

* *Software Architecture Patterns* — Mark Richards
* *Design Patterns: Elements of Reusable Object-Oriented Software* — Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides
* *Fundamentals of Software Architecture* — Mark Richards & Neal Ford
