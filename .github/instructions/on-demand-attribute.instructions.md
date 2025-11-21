# On-Demand Attribute Instructions

When a user requests to add attributes to code elements, follow these guidelines to implement attributes in a flexible and maintainable way.

## Purpose

This instruction guides the addition of attributes, metadata, or decorators to code elements based on user requirements, ensuring consistency and maintainability.

## Scope

These instructions apply when:
- Adding attributes to classes, functions, or variables
- Implementing decorators in Python, Java annotations, C# attributes, etc.
- Adding metadata tags or JSDoc comments
- Implementing feature flags or configuration attributes

## Steps

1. **Identify the target elements**: Determine which code elements need the attribute
2. **Choose the appropriate mechanism**: Select the language-appropriate way to add attributes
3. **Define the attribute**: Create or use existing attribute definitions
4. **Apply consistently**: Add the attribute to all identified elements
5. **Document the attribute**: Add documentation explaining the attribute's purpose and usage

## Language-Specific Guidelines

### Python

Use decorators for function/method attributes:
```python
@attribute_name(param1="value1")
def example_function():
    pass
```

Use class variables or type hints for data attributes:
```python
class Example:
    attribute_name: str = "value"
```

### JavaScript/TypeScript

Use JSDoc comments for documentation attributes:
```javascript
/**
 * @attribute attributeName
 * @description Attribute description
 */
function exampleFunction() {}
```

Use decorators (TypeScript with experimental decorators):
```typescript
@AttributeName()
class Example {}
```

### Java

Use annotations:
```java
@AttributeName(value = "example")
public class Example {}
```

### C#

Use attributes:
```csharp
[AttributeName("example")]
public class Example {}
```

## Best Practices

1. **Consistency**: Apply the same attribute pattern across similar code elements
2. **Documentation**: Always document what the attribute does and why it's needed
3. **Validation**: Ensure attribute values are validated where appropriate
4. **Testing**: Add tests to verify attribute behavior
5. **Minimal changes**: Only add attributes where explicitly requested

## Common Patterns

### Feature Flags

Add attributes to enable/disable features:
```python
@feature_flag("new_feature", default=False)
def new_feature_function():
    pass
```

### Metadata

Add metadata for categorization or filtering:
```python
@metadata(category="utility", priority="high")
def utility_function():
    pass
```

### Validation

Add validation attributes:
```python
@validate(required=True, type=str)
def process_data(data):
    pass
```

## Rules

- Only add attributes where explicitly requested by the user
- Follow existing attribute patterns in the codebase
- Maintain backward compatibility when adding new attributes
- Document any new attribute types in appropriate documentation files
- Include the attribute in relevant tests

## Output

When adding attributes, ensure:
- All requested code elements have the attribute applied
- Documentation is updated to explain the new attributes
- Tests cover the attribute functionality
- Code style remains consistent with the project
