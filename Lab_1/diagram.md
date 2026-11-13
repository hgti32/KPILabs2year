```erDiagram
User |o--o{ Cart : has
User ||--o{ Order : places
Product ||--|{ ProductVariant : "has variants"
Cart ||--o{ CartItem : contains
ProductVariant ||--o{ CartItem : "refers to"
Order ||--|{ OrderItem : contains
ProductVariant ||--o{ OrderItem : "refers to"
Order ||--o{ Payment : paid_by
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
        id PK
        order_id FK
        payment_method string
        payment_status string
    }
    Shipment {
        tracking_number string
        delivery_status string
    }
