# DAY 4: Unary & Special Operators

## Session Outline (3 Hours)
- **0:00-0:10:** Recap & Quiz on Comparison & Logical Ops
- **0:10-1:00:** Theory: Unary Operators, Ternary, typeof, Nullish Coalescing
- **1:00-1:30:** Break
- **1:30-2:45:** Practical: Advanced Operator Puzzles
- **2:45-3:00:** Q&A & Assignment Intro

---

## 📖 Theory Content

### Unary Operators

Unary operators work with **one value**. We've seen some before!

#### Unary Plus & Minus
```javascript
const num = 5;
+num            // 5 (positive)
-num            // -5 (negative)

// Useful for type conversion
const str = "42";
+str            // 42 (converts to number)
-str            // -42

const price = "99.99";
+price          // 99.99 (forces number)
```

#### Increment & Decrement (++, --)

```javascript
let count = 5;

// Pre-increment (increment, then use)
++count;        // count = 6, then returns 6
const result1 = ++count;  // count = 7, result1 = 7

// Post-increment (use, then increment)
count++;        // count increases, but returns old value
const result2 = count++;  // result2 = 7, then count = 8

// Same for decrement
--count;        // Pre-decrement
count--;        // Post-decrement
```

**Rule of Thumb:** Avoid ++ and -- in complex expressions. They confuse beginners.

```javascript
// ❌ Confusing
let x = 5;
console.log(++x * 2);  // 12 (x becomes 6, then 6*2)

// ✅ Clear
let x = 5;
x = x + 1;
console.log(x * 2);    // 12
```

#### typeof Operator

Returns the type of a value as a string.

```javascript
typeof 42               // "number"
typeof "hello"          // "string"
typeof true             // "boolean"
typeof undefined        // "undefined"
typeof null             // "object" (quirk!)
typeof Symbol()         // "symbol"
typeof {}               // "object"
typeof []               // "object"
typeof function(){}     // "function"

// Check if variable exists
typeof undefinedVar     // "undefined" (doesn't throw error)
```

**Real-World: Type Checking**
```javascript
function processInput(value) {
    if (typeof value === "string") {
        console.log("Processing text: " + value);
    } else if (typeof value === "number") {
        console.log("Processing number: " + value);
    } else {
        console.log("Unknown type");
    }
}
```

### The Ternary (Conditional) Operator

The **only operator with 3 parts**: `condition ? valueIfTrue : valueIfFalse`

```javascript
// Simple example
const age = 20;
const status = (age >= 18) ? "Adult" : "Minor";
console.log(status);  // "Adult"

// Format: condition ? trueValue : falseValue
const score = 45;
const result = (score >= 50) ? "PASS" : "FAIL";
console.log(result);  // "FAIL"

// Nested ternary (avoid if possible—hard to read!)
const temp = 25;
const weather = (temp > 30) ? "Hot" : (temp > 20) ? "Warm" : "Cold";
console.log(weather);  // "Warm"
```

**vs if/else (we'll learn next week):**
```javascript
// Using ternary (one-liner)
const message = isValid ? "Success" : "Error";

// Using if/else (multi-line)
let message;
if (isValid) {
    message = "Success";
} else {
    message = "Error";
}
```

**Real-World: User Display**
```javascript
const isLoggedIn = true;
const displayText = isLoggedIn ? "Logout" : "Login";
console.log(displayText);  // "Logout"

// Message based on email verification
const emailVerified = false;
const message = emailVerified ? "Account active" : "Verify email first";
```

### The typeof Operator in Detail

```javascript
// Primitives
typeof 123        // "number"
typeof "str"      // "string"
typeof true       // "boolean"
typeof undefined  // "undefined"
typeof Symbol()   // "symbol"
typeof 123n       // "bigint"

// Objects
typeof null       // "object" (BUG in JavaScript!)
typeof {}         // "object"
typeof []         // "object" (arrays are objects)
typeof function(){} // "function"

// Check for null properly
const value = null;
console.log(value === null);        // true (correct)
console.log(typeof value === "object");  // true (but misleading)
```

### Nullish Coalescing Operator (??)

Returns the **right value if left is null/undefined**. (ES2020)

```javascript
// Practical use: default values
const name = null;
const displayName = name ?? "Guest";
console.log(displayName);  // "Guest"

const age = 0;
const displayAge = age ?? "Unknown";
console.log(displayAge);   // 0 (because 0 is not null/undefined)

// Compare with OR operator (||)
const value = 0;
const result1 = value || 10;   // 10 (0 is falsy)
const result2 = value ?? 10;   // 0 (0 is not null)
```

**Real-World: API Response Handling**
```javascript
// Server returns null if data unavailable
const userData = null;
const userName = userData ?? "Not provided";
console.log(userName);  // "Not provided"

// Default configuration
const timeout = null;
const finalTimeout = timeout ?? 3000;  // 3000 ms if not specified
```

### Optional Chaining Operator (?.)

Access nested properties safely. (ES2020)

```javascript
// Without optional chaining (crashes if obj is null)
const obj = null;
const value = obj.property;  // Error: Cannot read property of null

// With optional chaining (returns undefined safely)
const value = obj?.property;  // undefined (no error)

// With arrays
const arr = null;
const first = arr?.[0];  // undefined (safe)

// With functions
const obj = { method: function() { return 42; } };
const result = obj.method?.();  // 42
```

---

## 💻 Practical Session (1h 15min)

### Exercise 4.1: typeof Operator

**Goal:** Identify data types

```javascript
// Test different values
console.log(typeof 123);       // "number"
console.log(typeof "hello");   // "string"
console.log(typeof true);      // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object" (quirk!)
console.log(typeof {});        // "object"
console.log(typeof []);        // "object"

// Practical: Validate input type
function doubleNumber(value) {
    if (typeof value === "number") {
        return value * 2;
    } else {
        return "Error: Please provide a number";
    }
}

console.log(doubleNumber(5));     // 10
console.log(doubleNumber("5"));   // Error message
```

### Exercise 4.2: Ternary Operator

**Goal:** Use ternary for concise conditionals

```javascript
// Simple cases
const age = 25;
console.log(age >= 18 ? "Adult" : "Minor");

const score = 73;
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
console.log(grade);  // "C"

// Real use: Toggle states
let isDarkMode = false;
const buttonText = isDarkMode ? "Light Mode" : "Dark Mode";
console.log("Button: " + buttonText);

// CSS class selection
const isActive = true;
const className = isActive ? "btn-active" : "btn-inactive";
console.log(className);
```

### Exercise 4.3: Increment/Decrement Operators

**Goal:** Use ++ and -- correctly

```javascript
let counter = 0;

// Post-increment (use first, then increment)
console.log(counter++);  // 0, then counter = 1
console.log(counter);    // 1

// Pre-increment (increment first, then use)
console.log(++counter);  // 2
console.log(counter);    // 2

// Decrement
console.log(counter--);  // 2, then counter = 1
console.log(--counter);  // 0

// In loops (next week!)
let i = 0;
while (i < 3) {
    console.log(i);
    i++;  // Increment by 1
}
```

### Exercise 4.4: Nullish Coalescing

**Goal:** Handle null/undefined gracefully

```javascript
// User profile with missing data
const user = {
    name: "Priya",
    bio: null,
    website: undefined,
    age: 0
};

console.log(user.name ?? "Unknown");     // "Priya"
console.log(user.bio ?? "No bio");       // "No bio"
console.log(user.website ?? "Not set");  // "Not set"
console.log(user.age ?? 18);             // 0 (not null/undefined!)

// Compare with ||
console.log(user.age || 18);  // 18 (0 is falsy)
console.log(user.age ?? 18);  // 0 (0 is not null)
```

### Exercise 4.5: Operator Precedence Puzzle

**Goal:** Understand operation order

```javascript
// Predict output BEFORE running!

// 1. Arithmetic first
console.log(2 + 3 * 4);           // 14

// 2. Comparison next
console.log(5 > 3 && 2 < 4);      // true

// 3. Logical operators
console.log(true || false && false);  // true (AND first)

// 4. Ternary last
console.log(true ? 1 : 2 + 3);    // 1 (ternary happens first!)
console.log((true ? 1 : 2) + 3);  // 4

// Complex
const x = 5;
const result = x > 3 ? x * 2 : x + 10;
console.log(result);  // 10
```

### Exercise 4.6: Real-World - Parking Fee Calculator

**Goal:** Apply operators to calculate fees

```javascript
const hours = 5;
const isHandicapped = true;

// Rules:
// First hour: ₹50
// Each additional hour: ₹20
// Handicapped: Free parking

let fee;

if (isHandicapped) {
    fee = 0;
} else if (hours <= 1) {
    fee = 50;
} else {
    fee = 50 + (hours - 1) * 20;
}

// OR using ternary
fee = isHandicapped ? 0 : (hours <= 1 ? 50 : 50 + (hours - 1) * 20);

console.log("=== PARKING FEE ===");
console.log("Hours: " + hours);
console.log("Handicapped: " + isHandicapped);
console.log("Fee: ₹" + fee);
```

### Exercise 4.7: Temperature Converter (Official Experiment 6)

**Goal:** Convert between Celsius and Fahrenheit with bidirectional conversion

**Real-World Context:** Weather apps, scientific instruments, cooking recipes

```javascript
console.log("=== TEMPERATURE CONVERTER ===\n");

// Method 1: Celsius to Fahrenheit
console.log("--- Celsius to Fahrenheit ---");
const celsius = 25;
const fahrenheit = (celsius * 9/5) + 32;

console.log(celsius + "°C = " + fahrenheit + "°F");
console.log("Example: Room temperature (25°C) = " + fahrenheit + "°F");
console.log();

// Method 2: Fahrenheit to Celsius
console.log("--- Fahrenheit to Celsius ---");
const fahrenheitInput = 77;
const celsiusOutput = (fahrenheitInput - 32) * 5/9;

console.log(fahrenheitInput + "°F = " + celsiusOutput.toFixed(2) + "°C");
console.log();

// Function for conversion (with validation)
function celsiusToFahrenheit(c) {
    // Absolute zero is -273.15°C
    if (c < -273.15) {
        return "Error: Temperature below absolute zero!";
    }
    return (c * 9/5) + 32;
}

function fahrenheitToCelsius(f) {
    // Absolute zero is -459.67°F
    if (f < -459.67) {
        return "Error: Temperature below absolute zero!";
    }
    return (f - 32) * 5/9;
}

// Test various temperatures
console.log("--- Temperature Conversions ---");

// Freezing point of water
console.log("0°C = " + celsiusToFahrenheit(0) + "°F (Water freezes)");

// Boiling point of water
console.log("100°C = " + celsiusToFahrenheit(100) + "°F (Water boils)");

// Body temperature
console.log("37°C = " + celsiusToFahrenheit(37).toFixed(1) + "°F (Normal body temp)");

// Room temperature
console.log("20°C = " + celsiusToFahrenheit(20) + "°F (Comfortable room)");

// Hot day
console.log("40°C = " + celsiusToFahrenheit(40) + "°F (Very hot day)");
console.log();

// Reverse conversions
console.log("--- Reverse Conversions ---");
console.log("32°F = " + fahrenheitToCelsius(32) + "°C (Water freezes)");
console.log("98.6°F = " + fahrenheitToCelsius(98.6).toFixed(1) + "°C (Body temp)");
console.log("212°F = " + fahrenheitToCelsius(212) + "°C (Water boils)");
console.log();
```

**Advanced: Weather Advisory System**
```javascript
function getWeatherAdvisory(celsius) {
    let advisory;
    
    if (celsius < -20) {
        advisory = "🥶 Extremely Cold - Stay indoors!";
    } else if (celsius < 0) {
        advisory = "❄️ Freezing - Wear heavy winter clothing";
    } else if (celsius < 10) {
        advisory = "🧥 Cold - Jacket recommended";
    } else if (celsius < 20) {
        advisory = "🌤️ Cool - Light jacket optional";
    } else if (celsius < 25) {
        advisory = "😊 Comfortable - Perfect weather!";
    } else if (celsius < 30) {
        advisory = "☀️ Warm - Light clothing recommended";
    } else if (celsius < 35) {
        advisory = "🌡️ Hot - Stay hydrated";
    } else {
        advisory = "🔥 Very Hot - Avoid outdoor activities!";
    }
    
    const fahrenheit = celsiusToFahrenheit(celsius);
    
    console.log("=== WEATHER ADVISORY ===");
    console.log("Temperature: " + celsius + "°C (" + fahrenheit.toFixed(1) + "°F)");
    console.log("Advisory: " + advisory);
    console.log();
}

// Test different temperatures
getWeatherAdvisory(-25);  // Extremely cold
getWeatherAdvisory(0);    // Freezing
getWeatherAdvisory(15);   // Cool
getWeatherAdvisory(22);   // Comfortable
getWeatherAdvisory(38);   // Very hot
```

**Using Ternary Operators for Temperature Categories:**
```javascript
function categorizeTempWithTernary(celsius) {
    const fahrenheit = (celsius * 9/5) + 32;
    
    // Categorize using ternary operators
    const category = celsius < 0 ? "Freezing" :
                    celsius < 15 ? "Cold" :
                    celsius < 25 ? "Comfortable" :
                    celsius < 35 ? "Hot" : "Very Hot";
    
    const emoji = celsius < 0 ? "❄️" :
                 celsius < 15 ? "🧥" :
                 celsius < 25 ? "😊" :
                 celsius < 35 ? "☀️" : "🔥";
    
    return `${emoji} ${celsius}°C (${fahrenheit.toFixed(1)}°F) - ${category}`;
}

console.log("--- Temperature Categories ---");
console.log(categorizeTempWithTernary(-5));
console.log(categorizeTempWithTernary(10));
console.log(categorizeTempWithTernary(20));
console.log(categorizeTempWithTernary(30));
console.log(categorizeTempWithTernary(40));
console.log();
```

**Practice Challenges:**
```javascript
// Challenge 1: Create a function that handles invalid inputs
function safeConvertToFahrenheit(input) {
    if (typeof input !== "number") {
        return "Error: Please provide a number";
    }
    if (input < -273.15) {
        return "Error: Below absolute zero";
    }
    return (input * 9/5) + 32;
}

console.log(safeConvertToFahrenheit(25));      // Valid: 77
console.log(safeConvertToFahrenheit("25"));    // Error: type
console.log(safeConvertToFahrenheit(-300));    // Error: absolute zero

// Challenge 2: Create a bidirectional converter
function convertTemperature(value, fromUnit) {
    if (fromUnit === "C") {
        return {
            celsius: value,
            fahrenheit: (value * 9/5) + 32,
            kelvin: value + 273.15
        };
    } else if (fromUnit === "F") {
        const celsius = (value - 32) * 5/9;
        return {
            celsius: celsius,
            fahrenheit: value,
            kelvin: celsius + 273.15
        };
    } else {
        return "Error: Invalid unit. Use 'C' or 'F'";
    }
}

const temp1 = convertTemperature(25, "C");
console.log("25°C =", temp1);
// Output: { celsius: 25, fahrenheit: 77, kelvin: 298.15 }

const temp2 = convertTemperature(77, "F");
console.log("77°F =", temp2);
// Output: { celsius: 25, fahrenheit: 77, kelvin: 298.15 }
```

**Real-World Application: Weather App Display**
```javascript
// Simulate weather data from API
const cities = [
    { name: "Mumbai", temp: 32 },
    { name: "Delhi", temp: 38 },
    { name: "Shimla", temp: 15 },
    { name: "Manali", temp: 5 }
];

console.log("=== WEATHER DASHBOARD ===");
cities.forEach(city => {
    const fahrenheit = (city.temp * 9/5) + 32;
    const advisory = city.temp < 10 ? "Cold ❄️" :
                    city.temp < 25 ? "Pleasant 😊" :
                    city.temp < 35 ? "Warm ☀️" : "Hot 🔥";
    
    console.log(`${city.name}: ${city.temp}°C (${fahrenheit.toFixed(1)}°F) - ${advisory}`);
});
```

**Key Formulas to Remember:**
```
Celsius to Fahrenheit: F = (C × 9/5) + 32
Fahrenheit to Celsius: C = (F - 32) × 5/9
Celsius to Kelvin: K = C + 273.15
```

**Common Temperature Reference Points:**
```javascript
console.log("=== REFERENCE TEMPERATURES ===");
console.log("Absolute Zero: -273.15°C = " + celsiusToFahrenheit(-273.15).toFixed(2) + "°F");
console.log("Water Freezes: 0°C = " + celsiusToFahrenheit(0) + "°F");
console.log("Room Temperature: 20°C = " + celsiusToFahrenheit(20) + "°F");
console.log("Body Temperature: 37°C = " + celsiusToFahrenheit(37).toFixed(1) + "°F");
console.log("Water Boils: 100°C = " + celsiusToFahrenheit(100) + "°F");
```

---

### Exercise 4.8: Student Status Checker

**Goal:** Combine multiple operators

```javascript
const name = "Rohan";
const gpa = 3.5;
const attendance = 0.95;
const feePaid = true;

// Status rules:
// GPA >= 3.0 AND attendance >= 90% AND fee paid = Active
// Otherwise = Inactive

const isActive = (gpa >= 3.0) && (attendance >= 0.90) && feePaid;
const status = isActive ? "✓ Active" : "✗ Inactive";

console.log("=== STUDENT STATUS ===");
console.log("Name: " + name);
console.log("GPA: " + gpa);
console.log("Attendance: " + (attendance * 100) + "%");
console.log("Fee Paid: " + feePaid);
console.log("Status: " + status);
```

---

## 🎓 Summary

| Operator | Purpose | Example | Result |
|----------|---------|---------|--------|
| `typeof` | Get type | typeof "5" | "string" |
| `?:` | Conditional value | true ? "A" : "B" | "A" |
| `++` | Increment | x++ | x+1 |
| `??` | Nullish default | null ?? "default" | "default" |
| `?.` | Safe property access | obj?.prop | undefined if null |

---

## 📝 Day 4 Assignment

**Task 1:** Create `day4_unary_special.js` with:
- 10 typeof examples
- 5 ternary operator examples
- 3 nullish coalescing examples
- 2 optional chaining examples

**Task 2:** Build a "Temperature Advisory System":
```javascript
- Input: temperature in Celsius
- Output: "Too Cold" (< 10), "Comfortable" (10-25), "Too Hot" (> 25)
Use ternary operators
```

**Submission:** GitHub + Google Classroom

---

**Next:** Day 5 - Mini Project & Week Review
