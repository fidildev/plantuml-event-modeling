# Fields Enhancement for PlantUML Event Modeling Library

## Overview
This enhancement adds the ability to specify fields/properties for commands, events, views, policies, and other elements in the PlantUML Event Modeling library.

## What Was Changed

### 1. New Helper Function
Added `$_formatFields($fields)` function that formats field strings with:
- A separator line (`---`) for visual separation between element name and fields

### 2. Updated Core Function
Modified `$_addNode()` procedure to:
- Accept a new optional `$fields` parameter (default: empty string)
- Format the element name with fields before storing
- Maintain backward compatibility (fields parameter is optional)

### 3. Updated Public Procedures
All public element procedures now accept an optional `$fields` parameter:
- `$command($name, $offset, $arrow, $alias, $figure, $fields)`
- `$event($name, $laneAlias, $offset, $arrow, $alias, $figure, $fields)`
- `$view($name, $offset, $arrow, $alias, $figure, $fields)`
- `$policy($name, $laneAlias, $offset, $arrow, $alias, $figure, $fields)`
- `$wireframe($name, $laneAlias, $offset, $arrow, $alias, $figure, $fields)`
- `$extra($name, $offset, $arrow, $alias, $figure, $fields)`
- `$externalsystem($name, $laneAlias, $offset, $arrow, $alias, $figure, $fields)`
- `$question($name, $laneAlias, $offset, $arrow, $alias, $figure, $fields)`
- Persona variants: `$event_persona()`, `$command_persona()`, `$view_persona()`, `$wireframe_persona()`

## Usage Examples

### Basic Field Usage
```plantuml
$command("CreateSubscription", $fields = "userId: string\nplanId: string\namount: decimal")
```

### Event with Data Fields
```plantuml
$event("SubscriptionCreated", Subscription, $fields = "subscriptionId: UUID\nuserId: string\nplanId: string\ncreatedAt: timestamp")
```

### Policy with Validation Rules
```plantuml
$policy("CreateSubscriptionPolicy", $fields = "Validate userId exists\nCheck plan is active\nVerify amount > 0")
```

### View with Display Fields
```plantuml
$view("Subscriptions View", $fields = "subscriptionId\nstatus\nplanName\nexpiryDate")
```

### Wireframe with UI Elements
```plantuml
$wireframe("Subscription Screen", Client, $fields = "Display subscription details\nShow payment history\nCancel button")
```

### Using Creole Formatting
You can use PlantUML creole syntax for enhanced formatting:
```plantuml
$command("CreateOrder", $fields = "<b>Required:</b>\n• customerId: UUID\n• items: array\n• total: decimal")

$view("Orders", $fields = "<b>Columns:</b>\n- Order ID\n- Customer\n- Status\n- Total")
```

## Example Files

### 1. fields-example.puml
Comprehensive example demonstrating field usage across all element types including:
- Commands with typed fields
- Policies with validation rules
- Events with data schemas
- Views with display fields
- Wireframes with UI elements
- External systems with API details

### 2. rendering-error.puml (Updated)
Updated the existing example to demonstrate field usage in a real-world subscription flow.

## Backward Compatibility
✅ **Fully backward compatible** - All existing diagrams continue to work without modification since the `$fields` parameter is optional and defaults to an empty string.

## Testing
All examples have been tested and render successfully:
- ✅ fields-example.puml - Renders without errors
- ✅ rendering-error.puml - Renders without errors  
- ✅ Example1.puml - Existing example still works (backward compatibility confirmed)

## Benefits
1. **Better Documentation** - Fields provide clear schema/contract information directly in diagrams
2. **Improved Communication** - Stakeholders can see exactly what data flows through the system
3. **Design Validation** - Helps identify missing or inconsistent fields early
4. **Code Generation Ready** - Field definitions can be used to generate code scaffolding
5. **Flexible Formatting** - Supports plain text and creole formatting for customization

