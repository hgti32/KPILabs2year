# Промпт 2: Генерація декларативної ER-діаграми

## Запит до ШІ (Prompt)

На основі моєї специфікації (`spec.md`) згенеруй концептуальну ER-діаграму в синтаксисі Mermaid (`erDiagram`).

### Сутності та атрибути для моделі:

- **User**: `name` (string), `email` (string)
- **Product**: `title` (string), `description` (string)
- **ProductVariant**: `size` (string), `color` (string), `price` (decimal), `stock` (int)
- **Cart**: `session_id` (string)
- **CartItem**: `quantity` (int)
- **Order**: `status` (string), `total_amount` (decimal)
- **OrderItem**: `quantity` (int), `unit_price` (decimal)
- **Payment**: `payment_method` (string), `payment_status` (string)
- **Shipment**: `tracking_number` (string), `delivery_status` (string)

### Вимоги до генерації:

1. Фокус на зв'язках і кардинальностях (`1:1`, `1:N`).
2. Без фізичної схеми БД (без первинних/зовнішніх ключів `PK`/`FK` та SQL-типів).
3. Зв'язки «багато-до-багатьох» між `Cart` ↔ `ProductVariant` та `Order` ↔ `ProductVariant` реалізувати через асоціативні сутності `CartItem` і `OrderItem`, оскільки вони несуть власні атрибути (`quantity`, `unit_price`).
4. Порядок запису в блоках сутностей: спочатку назва атрибута, праворуч — тип даних (наприклад, `email string`).

---

## Відповідь ШІ (Output)

erDiagram
    User ||--o{ Cart : has
    User ||--o{ Order : places
    Product ||--|{ ProductVariant : "has variants"
    Cart ||--o{ CartItem : contains
    ProductVariant ||--o{ CartItem : "refers to"
    Order ||--|{ OrderItem : contains
    ProductVariant ||--o{ OrderItem : "refers to"
    Order ||--|| Payment : paid_by
    Order ||--|| Shipment : shipped_via

    User {
        name string
        email string
    }
    Product {
        title string
        description string
    }
    ProductVariant {
        size string
        color string
        price decimal
        stock int
    }
    Cart {
        session_id string
    }
    CartItem {
        quantity int
    }
    Order {
        status string
        total_amount decimal
    }
    OrderItem {
        quantity int
        unit_price decimal
    }
    Payment {
        payment_method string
        payment_status string
    }
    Shipment {
        tracking_number string
        delivery_status string
    }