# Fields Parameter - Quick Reference Guide

## Syntax
All element procedures now support an optional `$fields` parameter:

```plantuml
$command("Name", $fields = "field1: type\nfield2: type")
$event("Name", Lane, $fields = "field1: type\nfield2: type")
$view("Name", $fields = "field1\nfield2\nfield3")
$policy("Name", $fields = "Rule 1\nRule 2")
$wireframe("Name", Lane, $fields = "Element 1\nElement 2")
```

## Common Patterns

### Commands - Required Input Fields
```plantuml
$command("CreateUser", $fields = "email: string\npassword: string\nfirstName: string\nlastName: string")
```

### Events - Data Schema
```plantuml
$event("UserCreated", User, $fields = "userId: UUID\nemail: string\nfirstName: string\nlastName: string\ncreatedAt: timestamp")
```

### Views - Display Fields
```plantuml
$view("Users List", $fields = "userId\nfullName\nemail\nstatus\ncreatedAt")
```

### Policies - Business Rules
```plantuml
$policy("ValidateUser", $fields = "Email must be unique\nPassword min 8 chars\nAge must be 18+")
```

### Wireframes - UI Elements
```plantuml
$wireframe("Login Screen", User, $fields = "Email input\nPassword input\nLogin button\nForgot password link")
```

## Formatting Options

### Plain List
```plantuml
$fields = "field1\nfield2\nfield3"
```

### Typed Fields
```plantuml
$fields = "field1: string\nfield2: int\nfield3: UUID"
```

### Bullet Points
```plantuml
$fields = "• field1\n• field2\n• field3"
```

### Bold Headers (Creole)
```plantuml
$fields = "<b>Required:</b>\nfield1\nfield2\n<b>Optional:</b>\nfield3"
```

### Numbered List
```plantuml
$fields = "1. First step\n2. Second step\n3. Third step"
```

### Mixed Format
```plantuml
$fields = "<b>Input:</b>\n• userId: UUID\n• amount: decimal\n<b>Validation:</b>\n✓ Amount > 0\n✓ User exists"
```

## Complete Example

```plantuml
@startuml
!include_once event-modeling-lib.iuml

$enableAutoAlias()
$enableAutoSpacing()

$configureWireframeLane(Customer)
$configureEventLane(Order)

$wireframe("Product Page", Customer, 
    $fields = "Product image\nPrice display\nQuantity selector\nAdd to cart button")

$command("AddToCart", 
    $fields = "customerId: UUID\nproductId: UUID\nquantity: int")

$event("ItemAddedToCart", Order, 
    $fields = "cartId: UUID\ncustomerId: UUID\nproductId: UUID\nquantity: int\naddedAt: timestamp")

$view("Shopping Cart", 
    $fields = "cartId\nproductName\nquantity\nunitPrice\ntotalPrice")

$wireframe("Cart Page", Customer, 
    $fields = "Cart items list\nTotal amount\nCheckout button\nContinue shopping link")

$renderEventModelingDiagram()
@enduml
```

## Tips

1. **Use `\n` for line breaks** - Each field on a new line
2. **Keep it concise** - Too many fields can make diagrams cluttered
3. **Be consistent** - Use the same format across your diagrams
4. **Use types** - Helps developers understand data types
5. **Leverage creole** - Use bold, bullets, etc. for better readability

## Backward Compatibility

The `$fields` parameter is **optional**. All existing diagrams work without modification:

```plantuml
' Old style - still works
$command("CreateOrder")

' New style - with fields
$command("CreateOrder", $fields = "customerId: UUID\nproductId: UUID")
```

