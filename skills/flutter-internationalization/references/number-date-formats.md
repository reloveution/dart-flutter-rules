# Number and Date Formatting

Complete reference for number and date formatting in Flutter internationalization.

## Number Formatting

### Basic Number Formats

Supported placeholder types: `int`, `double`, `num`

| Format | Example Input | Example Output (en_US) |
|---------|---------------|----------------------|
| `compact` | 1200000 | 1.2M |
| `compactCurrency` | 1200000 | $1.2M |
| `compactSimpleCurrency` | 1200000 | $1.2M |
| `compactLong` | 1200000 | 1.2 million |
| `currency` | 1200000 | USD1,200,000.00 |
| `decimalPattern` | 1200000 | 1,200,000 |
| `decimalPatternDigits` | 1200000 | 1,200,000 |
| `decimalPercentPattern` | 1.2 | 120% |
| `percentPattern` | 1.2 | 120% |
| `scientificPattern` | 1200000 | 1E6 |
| `simpleCurrency` | 1200000 | $1,200,000 |

### Currency Formats

#### Currency with Default Symbol

```json
{
  "price": "Price: {value}",
  "@price": {
    "placeholders": {
      "value": {
        "type": "int",
        "format": "currency"
      }
    }
  }
}
```

#### Currency with Custom Symbol

```json
{
  "price": "Price: {value}",
  "@price": {
    "placeholders": {
      "value": {
        "type": "int",
        "format": "simpleCurrency",
        "optionalParameters": {
          "symbol": "€"
        }
      }
    }
  }
}
```

#### Compact Currency

```json
{
  "followers": "{count} followers",
  "@followers": {
    "placeholders": {
      "count": {
        "type": "int",
        "format": "compactCurrency"
      }
    }
  }
}
```

### Decimal Places Control

```json
{
  "price": "Price: {value}",
  "@price": {
    "placeholders": {
      "value": {
        "type": "double",
        "format": "compactCurrency",
        "optionalParameters": {
          "decimalDigits": 2
        }
      }
    }
  }
}
```

### Percentage

```json
{
  "progress": "Progress: {value}",
  "@progress": {
    "placeholders": {
      "value": {
        "type": "double",
        "format": "percentPattern"
      }
    }
  }
}
```

## Date Formatting

### DateFormat Patterns

Supported placeholder type: `DateTime`

| Pattern | Example (en_US) | Description |
|----------|------------------|-------------|
| `y` | 2024 | Year |
| `M` | 1 | Month |
| `d` | 15 | Day |
| `E` | Mon | Day name (short) |
| `EEEE` | Monday | Day name (long) |
| `LLL` | Jan | Month name (short) |
| `LLLL` | January | Month name (long) |

### Common Date Formats

```json
{
  "eventDate": "Event on {date}",
  "@eventDate": {
    "placeholders": {
      "date": {
        "type": "DateTime",
        "format": "yMd"
      }
    }
  }
}
```

### Full Date Formats

| Format | Example (en_US) | Example (ru_RU) |
|---------|------------------|-----------------|
| `yMd` | 1/15/2024 | 15.01.2024 |
| `yMMMd` | Jan 15, 2024 | 15 янв. 2024 |
| `yMMMMd` | January 15, 2024 | 15 января 2024 |
| `yMMMMEEEEd` | Monday, January 15, 2024 | понедельник, 15 января 2024 |
| `Hm` | 14:30 | 14:30 |
| `Hms` | 14:30:45 | 14:30:45 |
| `j` | 2:30 PM | 14:30 |
| `jm` | 2:30 PM | 14:30 |

### Relative Time

For relative time (e.g., "2 minutes ago"), use `intl` package directly:

```dart
import 'package:intl/intl.dart';

final timeAgo = DateFormat('jm').format(DateTime.now().subtract(Duration(minutes: 2)));
```

## Platform-Specific Formatting

Flutter automatically formats numbers and dates according to locale. Examples:

### English (en_US)
- Numbers: 1,234,567.89
- Currency: $1,234.57
- Date: January 15, 2024

### Spanish (es_ES)
- Numbers: 1.234.567,89
- Currency: 1.234,57 €
- Date: 15 de enero de 2024

### French (fr_FR)
- Numbers: 1 234 567,89
- Currency: 1 234,57 €
- Date: 15 janvier 2024

### German (de_DE)
- Numbers: 1.234.567,89
- Currency: 1.234,57 €
- Date: 15. Januar 2024

### Russian (ru_RU)
- Numbers: 1 234 567,89
- Currency: 1 234,57 ₽
- Date: 15 января 2024

## Best Practices

1. **Use locale-aware formatting**: Always specify `format` for numbers/dates
2. **Don't format manually**: Let Flutter handle locale-specific formatting
3. **Test across locales**: Verify formatting in target locales
4. **Use compact for large numbers**: Makes UI more readable
5. **Consider context**: Use currency symbol appropriate for audience
6. **Handle special cases**: Some languages have unique formatting rules

## Common Patterns

### Price Display

```json
{
  "itemPrice": "Price: {price}",
  "@itemPrice": {
    "placeholders": {
      "price": {
        "type": "double",
        "format": "simpleCurrency"
      }
    }
  }
}
```

### Count Display

```json
{
  "itemCount": "{count, plural, =0{No items} =1{1 item} other{{count} items}}",
  "@itemCount": {
    "placeholders": {
      "count": {
        "type": "int",
        "format": "compact"
      }
    }
  }
}
```

### Date Range

```json
{
  "dateRange": "From {start} to {end}",
  "@dateRange": {
    "placeholders": {
      "start": {
        "type": "DateTime",
        "format": "yMMMd"
      },
      "end": {
        "type": "DateTime",
        "format": "yMMMd"
      }
    }
  }
}
```
