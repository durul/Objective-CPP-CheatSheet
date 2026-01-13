## Objective-C++ Cheat Sheet


![Gemini_Generated_Image_ec2ll9ec2ll9ec2l](https://github.com/user-attachments/assets/b81b861a-7dd9-4557-80d4-67d62ff89f9c)




This is not meant to be a beginner's guide or a detailed discussion about Objective-C++; it is meant to be a quick reference to common, high level topics covering the hybrid use of Objective-C and C++.

- This document is based on the original [Objective-C CheatSheet](https://github.com/iwasrobbed/Objective-C-CheatSheet).
- Apple Objective-C Programming Guide [https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html]
- Objective-C++ allows you to mix C++ code with Objective-C code, enabling you to use C++ classes, templates, and STL within your iOS/macOS projects.

**File Extension**: Objective-C++ files use the `.mm` extension instead of `.m` for implementation files. Header files typically remain `.h` but can also be `.hpp`.

**Note**: Objective-C++ is useful when you need to integrate C++ libraries, use C++ features like templates and STL containers, or leverage existing C++ codebases in your Apple platform projects.

For advanced Objective-C++ topics:

- [Apple's Objective-C++ Documentation](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Introduction/Introduction.html)
- [C++ Reference](https://en.cppreference.com/)

### Table of Contents

- [Getting Started](#getting-started)
- [Commenting](#commenting)
- [Data Types](#data-types)
- [C++ Features in Objective-C++](#c-features-in-objective-c)
- [Constants](#constants)
- [Operators](#operators)
- [Declaring Classes](#declaring-classes)
- [Mixing C++ and Objective-C Classes](#mixing-c-and-objective-c-classes)
- [Preprocessor Directives](#preprocessor-directives)
- [Compiler Directives](#compiler-directives)
- [Literals](#literals)
- [Methods](#methods)
- [Properties and Variables](#properties-and-variables)
- [Naming Conventions](#naming-conventions)
- [Blocks and Lambdas](#blocks-and-lambdas)
- [Control Statements](#control-statements)
- [Enumeration](#enumeration)
- [Extending Classes](#extending-classes)
- [Error Handling](#error-handling)
- [STL Containers](#stl-containers)
- [Smart Pointers](#smart-pointers)
- [Passing Information](#passing-information)
- [User Defaults](#user-defaults)
- [Common Patterns](#common-patterns)
- [Threading and Concurrency](#threading-and-concurrency)
- [Memory Management with ARC](#memory-management-with-arc)
- [Wrapping C++ Libraries](#wrapping-c-libraries)
- [Common Pitfalls](#common-pitfalls)
- [Debugging Tips](#debugging-tips)

## Getting Started

### Creating Your First Objective-C++ File

**Step 1: Rename or Create .mm File**

```bash
# In Xcode, simply rename your .m file to .mm
# Or create a new file with .mm extension
MyClass.m  →  MyClass.mm
```

**Step 2: Basic Objective-C++ File Structure**

```objcpp
// MyFirstClass.mm
#import <Foundation/Foundation.h>
#include <iostream>
#include <vector>
#include <string>

@interface MyFirstClass : NSObject
- (void)sayHello;
- (void)demonstrateCpp;
@end

@implementation MyFirstClass

- (void)sayHello {
    // Objective-C style
    NSLog(@"Hello from Objective-C!");
    
    // C++ style
    std::cout << "Hello from C++!" << std::endl;
}

- (void)demonstrateCpp {
    // Using STL vector
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    
    for (int num : numbers) {
        NSLog(@"Number: %d", num);
    }
    
    // Using std::string
    std::string cppString = "C++ String";
    NSString *nsString = [NSString stringWithUTF8String:cppString.c_str()];
    NSLog(@"Converted: %@", nsString);
}

@end
```

**Step 3: Xcode Build Settings (if needed)**

```
// In Build Settings, ensure:
// 1. C++ Language Dialect: C++17 or later (recommended)
// 2. C++ Standard Library: libc++ (LLVM C++ standard library)
```

### When to Use Objective-C++

| Use Case | Example |
|----------|----------|
| Integrating C++ libraries | OpenCV, Boost, game engines |
| Performance-critical code | Audio/video processing |
| Cross-platform shared code | Core logic in C++ |
| Using STL containers | std::vector, std::map |
| Template metaprogramming | Generic algorithms |

### Project Structure Recommendation

```
MyApp/
├── Sources/
│   ├── Objective-C/           # Pure Objective-C (.m)
│   │   └── AppDelegate.m
│   ├── Objective-CPP/         # Mixed code (.mm)
│   │   ├── CppBridge.h        # Public ObjC interface
│   │   └── CppBridge.mm       # C++ implementation
│   └── Cpp/                   # Pure C++ (.cpp)
│       ├── Engine.hpp
│       └── Engine.cpp
└── Headers/
    └── PublicHeaders.h        # Only Objective-C types!
```

[Back to top](#objective-c-cheat-sheet)

## Commenting

Comments in Objective-C++ work the same as in both C++ and Objective-C:

```objcpp
// This is an inline comment (C++ style)

/* This is a block comment
   and it can span multiple lines. */

// You can also use it to comment out code
/*
- (SomeOtherClass *)doWork
{
    // Implement this
}
*/
```

Using `pragma` to organize your code:

```objcpp
#pragma mark - Use pragma mark to logically organize your code

// Declare some methods or variables here

#pragma mark - They also show up nicely in the properties/methods list in Xcode

// Declare some more methods or variables here
```

[Back to top](#objective-c-cheat-sheet)

## Data Types

### C++ Primitives in Objective-C++

Objective-C++ inherits all C/C++ primitive types plus Objective-C types.

#### Boolean Types

```objcpp
// C++ bool type
bool cppBool = true;    // or false

// Objective-C BOOL type
BOOL objcBool = YES;    // or NO

// Note: bool and BOOL are NOT the same type!
// bool is 1 byte, BOOL is typically signed char (8 bits)
```

#### Integers with C++ Fixed-Width Types

```objcpp
#include <cstdint>

// C++11 fixed-width integer types
std::int8_t   a = 127;
std::uint8_t  b = 255;
std::int16_t  c = 32767;
std::uint16_t d = 65535;
std::int32_t  e = 2147483647;
std::uint32_t f = 4294967295;
std::int64_t  g = 9223372036854775807LL;
std::uint64_t h = 18446744073709551615ULL;

// size_t for sizes
std::size_t arraySize = 100;
```

#### Floating Point with C++ Types

```objcpp
// Standard floating point types
float aFloat = 72.0345f;
double aDouble = -72.0345;
long double aLongDouble = 72.0345e7L;

// C++11 additions (if supported)
// float, double, long double sizes remain the same
```

### Objective-C Primitives (Still Available)

```objcpp
id delegate = self.delegate;              // Dynamic object type
Class aClass = [UIView class];            // Class type
Method aMethod = class_getInstanceMethod(aClass, aSelector);
SEL someSelector = @selector(someMethodName);
IMP theImplementation = [self methodForSelector:someSelector];
BOOL isBool = YES;                        // Objective-C boolean
```

### C++ Reference Types

```objcpp
// References (C++ feature)
int original = 42;
int& reference = original;  // reference is an alias for original
reference = 100;            // original is now 100

// Const references
const std::string& constRef = someString;  // Cannot modify through constRef
```

### Auto Type Deduction (C++11)

```objcpp
// auto keyword for type deduction
auto intValue = 42;                        // int
auto doubleValue = 3.14;                   // double
auto stringValue = @"Hello";               // NSString*
auto cppString = std::string("Hello");     // std::string
auto vector = std::vector<int>{1, 2, 3};   // std::vector<int>
```

### Enum & Bitmask Types

```objcpp
// C++11 strongly typed enums (recommended in Objective-C++)
enum class UITableViewCellStyle : int {
    Default,
    Value1,
    Value2,
    Subtitle
};

// Usage
UITableViewCellStyle style = UITableViewCellStyle::Default;

// Traditional Objective-C enums still work
typedef NS_ENUM(NSInteger, RPViewState) {
    RPViewStateLoading,
    RPViewStateLoaded,
    RPViewStateError
};

// Bitmask with NS_OPTIONS
typedef NS_OPTIONS(NSUInteger, RPBitMask) {
    RPOptionNone      = 0,
    RPOptionRight     = 1 << 0,
    RPOptionBottom    = 1 << 1,
    RPOptionLeft      = 1 << 2,
    RPOptionTop       = 1 << 3
};
```

[Back to top](#objective-c-cheat-sheet)

## C++ Features in Objective-C++

### Templates

```objcpp
// Template function
template<typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

// Usage
int maxInt = maximum(10, 20);
double maxDouble = maximum(3.14, 2.71);

// Template class
template<typename T>
class Container {
private:
    T value;
public:
    Container(T v) : value(v) {}
    T getValue() const { return value; }
    void setValue(T v) { value = v; }
};

// Usage
Container<int> intContainer(42);
Container<std::string> stringContainer("Hello");
```

### Namespaces

```objcpp
// Define a namespace
namespace MyApp {
    namespace Utils {
        int calculate(int x, int y) {
            return x + y;
        }

        class Helper {
        public:
            static void log(const std::string& message);
        };
    }
}

// Usage
int result = MyApp::Utils::calculate(5, 3);
MyApp::Utils::Helper::log("Message");

// Using directive
using namespace MyApp::Utils;
int result2 = calculate(10, 20);
```

### Range-Based For Loops (C++11)

```objcpp
#include <vector>
#include <string>

std::vector<int> numbers = {1, 2, 3, 4, 5};

// Range-based for loop
for (int num : numbers) {
    NSLog(@"Number: %d", num);
}

// With references to avoid copying
std::vector<std::string> names = {"Alice", "Bob", "Charlie"};
for (const auto& name : names) {
    NSLog(@"Name: %s", name.c_str());
}
```

### Move Semantics (C++11)

```objcpp
#include <utility>
#include <vector>

// Move constructor usage
std::vector<int> createVector() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    return vec;  // Move semantics applied automatically
}

// Explicit move
std::vector<int> source = {1, 2, 3};
std::vector<int> destination = std::move(source);  // source is now empty
```

### constexpr (C++11)

```objcpp
// Compile-time constants
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

constexpr int fact5 = factorial(5);  // Computed at compile time

// constexpr variables
constexpr double PI = 3.14159265358979323846;
constexpr int MAX_BUFFER_SIZE = 1024;
```

[Back to top](#objective-c-cheat-sheet)

## Constants

### C++ Style Constants

```objcpp
// constexpr for compile-time constants (preferred in C++)
constexpr int kMaxRetries = 3;
constexpr double kAnimationDuration = 0.3;

// const for runtime constants
const std::string kAPIEndpoint = "https://api.example.com";

// Static const in class
class Config {
public:
    static constexpr int MaxConnections = 10;
    static const std::string AppName;  // Define in .mm file
};
```

### Objective-C Style Constants (Still Valid)

```objcpp
// Objective-C string constants
NSString *const kRPShortDateFormat = @"MM/dd/yyyy";

// Extern for header files
extern NSString *const kRPShortDateFormat;

// Static for file-local constants
static NSString *const kRPPrivateConstant = @"private";
```

### inline Variables (C++17)

```objcpp
// Inline variables can be defined in headers
inline constexpr int kBufferSize = 256;
inline const char* kVersionString = "1.0.0";
```

[Back to top](#objective-c-cheat-sheet)

## Operators

All C/C++ and Objective-C operators are available in Objective-C++.

### C++ Specific Operators

|     Operator     |           Purpose            |
| :--------------: | :--------------------------: |
|        ::        |       Scope resolution       |
|       .\*        | Pointer-to-member (objects)  |
|       ->\*       | Pointer-to-member (pointers) |
|       new        |  Dynamic memory allocation   |
|      delete      | Dynamic memory deallocation  |
|      new[]       |       Array allocation       |
|     delete[]     |      Array deallocation      |
|      typeid      |     Type identification      |
|   dynamic_cast   |       Safe downcasting       |
|   static_cast    |      Compile-time cast       |
| reinterpret_cast |        Low-level cast        |
|    const_cast    |    Remove const qualifier    |

```objcpp
// Scope resolution
std::cout << "Hello" << std::endl;

// new and delete
int* ptr = new int(42);
delete ptr;

int* arr = new int[10];
delete[] arr;

// Type casting
Base* basePtr = new Derived();
Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
```

[Back to top](#objective-c-cheat-sheet)

## Declaring Classes

### Objective-C++ Class with C++ Members

MyClass.h

```objcpp
#import <Foundation/Foundation.h>
#include <string>
#include <vector>
#include <memory>

@class SomeOtherClass;

// Forward declare C++ types if needed
namespace MyNamespace {
    class CppHelper;
}

extern NSString *const kRPErrorDomain;

@interface MyClass : NSObject

// Public properties
@property (readonly, nonatomic, strong) NSString *name;

// Class methods
+ (instancetype)sharedInstance;

// Instance methods
- (void)processWithCppString:(const std::string&)cppString;
- (std::vector<int>)getNumbers;

@end
```

MyClass.mm (Note the .mm extension!)

```objcpp
#import "MyClass.h"
#include <iostream>
#include <algorithm>

NSString *const kRPErrorDomain = @"com.myApp.errors";

// C++ helper class (private implementation)
class CppProcessor {
private:
    std::vector<int> data;

public:
    void addNumber(int num) {
        data.push_back(num);
    }

    std::vector<int> getSortedData() const {
        std::vector<int> sorted = data;
        std::sort(sorted.begin(), sorted.end());
        return sorted;
    }
};

@interface MyClass () {
    // C++ instance variables
    std::string _cppName;
    std::unique_ptr<CppProcessor> _processor;
}

@property (readwrite, nonatomic, strong) NSString *name;

@end

@implementation MyClass

#pragma mark - Init & Dealloc

- (instancetype)init {
    if (self = [super init]) {
        _processor = std::make_unique<CppProcessor>();
        _cppName = "Default";
    }
    return self;
}

// Note: C++ members are automatically destroyed
// No need to call delete for unique_ptr

#pragma mark - Class Methods

+ (instancetype)sharedInstance {
    static MyClass *instance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        instance = [[self alloc] init];
    });
    return instance;
}

#pragma mark - Instance Methods

- (void)processWithCppString:(const std::string&)cppString {
    _cppName = cppString;
    self.name = [NSString stringWithUTF8String:cppString.c_str()];

    // Use C++ features
    std::cout << "Processing: " << cppString << std::endl;
}

- (std::vector<int>)getNumbers {
    _processor->addNumber(42);
    _processor->addNumber(17);
    _processor->addNumber(99);
    return _processor->getSortedData();
}

@end
```

[Back to top](#objective-c-cheat-sheet)

## Mixing C++ and Objective-C Classes

### C++ Class Wrapping Objective-C Object

```objcpp
#import <Foundation/Foundation.h>

class ObjCWrapper {
private:
    NSMutableArray* _array;  // Objective-C object in C++ class

public:
    ObjCWrapper() {
        _array = [[NSMutableArray alloc] init];
    }

    ~ObjCWrapper() {
        // Under ARC, no need to release
        // Under MRC, [_array release];
    }

    void addObject(NSString* str) {
        [_array addObject:str];
    }

    NSUInteger count() const {
        return [_array count];
    }

    NSString* objectAtIndex(NSUInteger index) const {
        return [_array objectAtIndex:index];
    }
};
```

### Objective-C Class Wrapping C++ Object

```objcpp
#include <memory>
#include <string>

// C++ class
class Engine {
private:
    std::string name;
    int horsepower;

public:
    Engine(const std::string& n, int hp) : name(n), horsepower(hp) {}

    std::string getName() const { return name; }
    int getHorsepower() const { return horsepower; }

    void start() {
        std::cout << "Engine " << name << " started!" << std::endl;
    }
};

// Objective-C class wrapping C++ class
@interface Car : NSObject

@property (nonatomic, readonly) NSString *engineName;
@property (nonatomic, readonly) int horsepower;

- (instancetype)initWithEngineName:(NSString *)name horsepower:(int)hp;
- (void)startEngine;

@end

@implementation Car {
    std::unique_ptr<Engine> _engine;
}

- (instancetype)initWithEngineName:(NSString *)name horsepower:(int)hp {
    if (self = [super init]) {
        std::string cppName = [name UTF8String];
        _engine = std::make_unique<Engine>(cppName, hp);
    }
    return self;
}

- (NSString *)engineName {
    return [NSString stringWithUTF8String:_engine->getName().c_str()];
}

- (int)horsepower {
    return _engine->getHorsepower();
}

- (void)startEngine {
    _engine->start();
}

@end
```

### String Conversion Utilities

```objcpp
// NSString to std::string
NSString *nsString = @"Hello, World!";
std::string cppString = [nsString UTF8String];

// std::string to NSString
std::string cppStr = "Hello from C++";
NSString *nsStr = [NSString stringWithUTF8String:cppStr.c_str()];

// Safe conversion with nil check
NSString* safeConvert(const std::string& str) {
    return str.empty() ? @"" : [NSString stringWithUTF8String:str.c_str()];
}

std::string safeConvert(NSString* str) {
    return str ? [str UTF8String] : "";
}
```

[Back to top](#objective-c-cheat-sheet)

## Preprocessor Directives

Same as Objective-C, plus C++ specific ones:

|     Directive     | Purpose                                                |
| :---------------: | ------------------------------------------------------ |
|     #include      | Include C/C++ header files                             |
|      #import      | Include Objective-C header files (won't include twice) |
| #if \_\_cplusplus | Check if compiling as C++                              |
|  #ifdef **OBJC**  | Check if compiling Objective-C/Objective-C++           |

```objcpp
// Conditional compilation for C++ vs C
#if __cplusplus
    // C++ specific code
    #include <vector>
    #include <string>
#endif

// Conditional for Objective-C
#ifdef __OBJC__
    #import <Foundation/Foundation.h>
#endif

// Combined check for Objective-C++
#if defined(__cplusplus) && defined(__OBJC__)
    // Objective-C++ specific code
#endif

// C++ version check
#if __cplusplus >= 201703L
    // C++17 or later
#elif __cplusplus >= 201402L
    // C++14
#elif __cplusplus >= 201103L
    // C++11
#endif
```

[Back to top](#objective-c-cheat-sheet)

## Compiler Directives

All Objective-C directives work in Objective-C++:

```objcpp
@class SomeClass;           // Forward declaration
@interface                  // Class declaration
@implementation            // Class implementation
@protocol                  // Protocol declaration
@property                  // Property declaration
@synthesize / @dynamic     // Property synthesis
@try / @catch / @throw     // Exception handling
@autoreleasepool           // Memory management
```

[Back to top](#objective-c-cheat-sheet)

## Literals

### Objective-C Literals (Still Available)

```objcpp
NSString *str = @"Hello";
NSNumber *num = @42;
NSNumber *pi = @3.14;
NSNumber *yes = @YES;
NSArray *arr = @[@"one", @"two", @"three"];
NSDictionary *dict = @{@"key": @"value"};
```

### C++ Literals

```objcpp
// String literals
const char* cStr = "C string";
std::string cppStr = "C++ string";

// Raw string literals (C++11)
std::string rawStr = R"(This is a "raw" string
with newlines and special chars: \n \t)";

// User-defined literals (C++11)
using namespace std::string_literals;
auto s = "Hello"s;  // std::string literal

// Numeric literals with separators (C++14)
int million = 1'000'000;
double pi = 3.141'592'653;
```

[Back to top](#objective-c-cheat-sheet)

## Methods

### Objective-C Methods (Same Syntax)

```objcpp
// Instance method
- (void)doSomething {
    // Implementation
}

// Method with C++ parameters
- (void)processVector:(const std::vector<int>&)vec {
    for (int num : vec) {
        NSLog(@"Number: %d", num);
    }
}

// Method returning C++ type
- (std::string)getCppString {
    return "Hello from Objective-C++";
}
```

### C++ Member Functions

```objcpp
class Calculator {
public:
    // Regular member function
    int add(int a, int b) {
        return a + b;
    }

    // Const member function
    int getValue() const {
        return value;
    }

    // Static member function
    static Calculator* createDefault() {
        return new Calculator();
    }

    // Virtual function
    virtual void display() {
        std::cout << "Calculator" << std::endl;
    }

    // Override in derived class
    // void display() override { ... }

    // Pure virtual (abstract)
    virtual void mustImplement() = 0;

private:
    int value = 0;
};
```

### Lambda Expressions (C++11) vs Blocks

```objcpp
// Objective-C Block
void (^objcBlock)(int) = ^(int x) {
    NSLog(@"Block received: %d", x);
};
objcBlock(42);

// C++ Lambda
auto cppLambda = [](int x) {
    std::cout << "Lambda received: " << x << std::endl;
};
cppLambda(42);

// Lambda with capture
int multiplier = 10;
auto multiplyLambda = [multiplier](int x) {
    return x * multiplier;
};

// Lambda capturing all by reference
auto captureAllRef = [&]() {
    multiplier *= 2;  // Modifies original
};

// Lambda capturing all by value
auto captureAllVal = [=]() {
    return multiplier;  // Copy of multiplier
};
```

[Back to top](#objective-c-cheat-sheet)

## Properties and Variables

### Properties with C++ Types

```objcpp
@interface DataManager : NSObject

// You cannot use C++ types directly in @property
// Workaround: Use methods or wrap in Objective-C types

// This WON'T work:
// @property (nonatomic) std::vector<int> numbers;  // ERROR!

// Workaround 1: Methods
- (std::vector<int>)numbers;
- (void)setNumbers:(std::vector<int>)numbers;

// Workaround 2: Store as instance variable
@end

@implementation DataManager {
    std::vector<int> _numbers;  // C++ ivar
    std::map<std::string, int> _cache;
}

- (std::vector<int>)numbers {
    return _numbers;
}

- (void)setNumbers:(std::vector<int>)numbers {
    _numbers = std::move(numbers);
}

@end
```

### C++ Class Members

```objcpp
class DataHandler {
private:
    // Private members
    std::vector<int> data;
    std::string name;

protected:
    // Protected members (accessible in derived classes)
    int protectedValue;

public:
    // Public members
    static int instanceCount;

    // Getter/Setter
    const std::string& getName() const { return name; }
    void setName(const std::string& n) { name = n; }
};

// Initialize static member
int DataHandler::instanceCount = 0;
```

[Back to top](#objective-c-cheat-sheet)

## Naming Conventions

### Objective-C Naming Conventions

```objcpp
// Classes: CapitalCase with prefix
@interface RPDataManager : NSObject
@interface UIViewController : UIResponder

// Methods: camelCase, descriptive
- (void)loadDataFromServer;
- (NSString *)stringByAppendingPath:(NSString *)path;

// Properties: camelCase
@property (nonatomic, strong) NSString *userName;
@property (nonatomic, readonly) NSInteger itemCount;

// Constants: k prefix or UPPERCASE
static NSString *const kAPIEndpoint = @"https://api.example.com";
extern NSString *const RPErrorDomain;

// Enums: Prefix + CapitalCase
typedef NS_ENUM(NSInteger, RPLoadingState) {
    RPLoadingStateIdle,
    RPLoadingStateLoading,
    RPLoadingStateCompleted
};
```

### C++ Naming Conventions

```objcpp
// Classes: CapitalCase (PascalCase)
class DataProcessor {
public:
    // Methods: camelCase or snake_case (project dependent)
    void processData();
    void process_data();  // Alternative style
    
    // Member variables: m_ prefix or trailing underscore
    int mCount;           // m prefix style
    int count_;           // trailing underscore style
    
    // Constants: kPrefix or UPPER_SNAKE_CASE
    static constexpr int kMaxBufferSize = 1024;
    static constexpr int MAX_BUFFER_SIZE = 1024;
};

// Namespaces: lowercase or CapitalCase
namespace myapp {
namespace utils {
    void helperFunction();
}
}

// Template parameters: T, U, or descriptive CapitalCase
template<typename T>
template<typename ElementType>

// Enums: CapitalCase for enum class
enum class Color {
    Red,
    Green,
    Blue
};
```

### Mixed Naming Best Practices

```objcpp
// When mixing Objective-C and C++:

// 1. Use Objective-C style in @interface
@interface RPImageProcessor : NSObject
- (void)processImageWithCompletion:(void (^)(UIImage *))completion;
@end

// 2. Use C++ style for C++ classes
class ImageFilter {
public:
    void applyFilter(const std::string& filterName);
private:
    std::vector<float> coefficients_;
};

// 3. Keep consistent within each language context
@implementation RPImageProcessor {
    std::unique_ptr<ImageFilter> _filter;  // C++ member in ObjC class
}
@end
```

[Back to top](#objective-c-cheat-sheet)

## Blocks and Lambdas

### Objective-C Blocks

```objcpp
// Block as local variable
void (^simpleBlock)(void) = ^{
    NSLog(@"Block executed");
};

// Block with parameters and return
int (^addBlock)(int, int) = ^int(int a, int b) {
    return a + b;
};

// Block as method parameter
- (void)performWithCompletion:(void (^)(BOOL success))completion {
    // Do work
    completion(YES);
}
```

### C++ Lambdas

```objcpp
#include <functional>

// Lambda syntax: [capture](params) -> return_type { body }

// Simple lambda
auto simple = []() {
    std::cout << "Simple lambda" << std::endl;
};

// Lambda with parameters
auto add = [](int a, int b) -> int {
    return a + b;
};

// Capture modes
int x = 10;
int y = 20;

auto captureByValue = [x, y]() { return x + y; };        // Copy x and y
auto captureByRef = [&x, &y]() { x++; y++; };           // Reference to x and y
auto captureAllByValue = [=]() { return x + y; };        // Copy all
auto captureAllByRef = [&]() { x++; y++; };             // Reference all
auto mixedCapture = [=, &x]() { x = y; };               // Copy all, ref x

// Mutable lambda (can modify copies)
auto mutableLambda = [x]() mutable {
    x++;  // Modifies the copy
    return x;
};

// Generic lambda (C++14)
auto genericAdd = [](auto a, auto b) {
    return a + b;
};
int sum1 = genericAdd(1, 2);
double sum2 = genericAdd(1.5, 2.5);

// Using std::function
std::function<int(int, int)> funcObj = [](int a, int b) {
    return a + b;
};
```

### Converting Between Blocks and Lambdas

```objcpp
// Lambda to Block (requires careful handling)
auto lambda = [](int x) { return x * 2; };
int (^block)(int) = ^(int x) { return lambda(x); };

// Block inside lambda
void (^objcBlock)(void) = ^{ NSLog(@"Hello"); };
auto lambdaCallingBlock = [objcBlock]() {
    objcBlock();
};
```

[Back to top](#objective-c-cheat-sheet)

## Control Statements

### Standard Control Statements

```objcpp
// If-else (same as C/C++/Objective-C)
if (condition) {
    // code
} else if (otherCondition) {
    // code
} else {
    // code
}

// For loop
for (int i = 0; i < 10; i++) {
    // code
}

// Range-based for (C++11)
std::vector<int> nums = {1, 2, 3, 4, 5};
for (int num : nums) {
    // code
}

for (const auto& item : container) {
    // Read-only access
}

for (auto& item : container) {
    // Modifiable access
}

// While and Do-While
while (condition) {
    // code
}

do {
    // code
} while (condition);

// Switch
switch (value) {
    case 1:
        // code
        break;
    case 2:
    case 3:
        // code for 2 or 3
        break;
    default:
        // default code
        break;
}
```

### Fast Enumeration (Objective-C)

```objcpp
NSArray *items = @[@"one", @"two", @"three"];
for (NSString *item in items) {
    NSLog(@"%@", item);
}
```

### If-Init Statement (C++17)

```objcpp
// Variable declaration inside if
if (auto result = someFunction(); result != nullptr) {
    // Use result
}

// With switch
switch (auto value = getValue(); value) {
    case 1:
        // ...
        break;
}
```

[Back to top](#objective-c-cheat-sheet)

## Enumeration

### Block-Based Enumeration (Objective-C)

```objcpp
NSArray *people = @[@"Bob", @"Joe", @"Penelope"];
[people enumerateObjectsUsingBlock:^(NSString *name, NSUInteger idx, BOOL *stop) {
    NSLog(@"Person: %@", name);
    if ([name isEqualToString:@"Joe"]) {
        *stop = YES;  // Stop enumeration
    }
}];
```

### STL Algorithm-Based Enumeration

```objcpp
#include <algorithm>
#include <vector>

std::vector<int> nums = {1, 2, 3, 4, 5};

// std::for_each
std::for_each(nums.begin(), nums.end(), [](int n) {
    std::cout << n << " ";
});

// std::find
auto it = std::find(nums.begin(), nums.end(), 3);
if (it != nums.end()) {
    std::cout << "Found: " << *it << std::endl;
}

// std::find_if
auto even = std::find_if(nums.begin(), nums.end(), [](int n) {
    return n % 2 == 0;
});

// std::count_if
int count = std::count_if(nums.begin(), nums.end(), [](int n) {
    return n > 2;
});
```

[Back to top](#objective-c-cheat-sheet)

## Extending Classes

### C++ Inheritance

```objcpp
// Base class
class Animal {
protected:
    std::string name;

public:
    Animal(const std::string& n) : name(n) {}
    virtual ~Animal() = default;  // Virtual destructor for polymorphism

    virtual void speak() const = 0;  // Pure virtual
    std::string getName() const { return name; }
};

// Derived class
class Dog : public Animal {
private:
    std::string breed;

public:
    Dog(const std::string& n, const std::string& b)
        : Animal(n), breed(b) {}

    void speak() const override {
        std::cout << "Woof!" << std::endl;
    }

    std::string getBreed() const { return breed; }
};

// Multiple inheritance
class Flyable {
public:
    virtual void fly() = 0;
};

class Bird : public Animal, public Flyable {
public:
    Bird(const std::string& n) : Animal(n) {}

    void speak() const override {
        std::cout << "Tweet!" << std::endl;
    }

    void fly() override {
        std::cout << "Flying..." << std::endl;
    }
};
```

### Objective-C Categories (Same as Before)

```objcpp
// UIImage+ResizeCrop.h
@interface UIImage (ResizeCrop)
- (UIImage *)croppedImageWithSize:(CGSize)size;
- (UIImage *)resizedImageWithSize:(CGSize)size;
@end

// UIImage+ResizeCrop.mm
@implementation UIImage (ResizeCrop)

- (UIImage *)croppedImageWithSize:(CGSize)size {
    // Use C++ if needed
    std::cout << "Cropping image..." << std::endl;
    // Implementation
    return nil;
}

- (UIImage *)resizedImageWithSize:(CGSize)size {
    // Implementation
    return nil;
}

@end
```

[Back to top](#objective-c-cheat-sheet)

## Error Handling

### Objective-C Exception Handling

```objcpp
@try {
    // Code that might throw
    [self riskyOperation];
}
@catch (NSException *exception) {
    NSLog(@"Exception: %@", exception.reason);
}
@finally {
    // Always executed
}
```

### C++ Exception Handling

```objcpp
#include <stdexcept>
#include <string>

// Throwing exceptions
void riskyFunction(int value) {
    if (value < 0) {
        throw std::invalid_argument("Value cannot be negative");
    }
    if (value > 100) {
        throw std::out_of_range("Value out of range");
    }
}

// Catching exceptions
try {
    riskyFunction(-5);
}
catch (const std::invalid_argument& e) {
    std::cerr << "Invalid argument: " << e.what() << std::endl;
}
catch (const std::exception& e) {
    std::cerr << "Exception: " << e.what() << std::endl;
}
catch (...) {
    std::cerr << "Unknown exception" << std::endl;
}

// Custom exception class
class MyException : public std::exception {
private:
    std::string message;

public:
    MyException(const std::string& msg) : message(msg) {}

    const char* what() const noexcept override {
        return message.c_str();
    }
};
```

### noexcept Specifier (C++11)

```objcpp
// Function that won't throw
void safeFunction() noexcept {
    // If this throws, std::terminate is called
}

// Conditional noexcept
void maybeThrows() noexcept(false) {
    // Might throw
}

// Check if noexcept at compile time
static_assert(noexcept(safeFunction()), "safeFunction should be noexcept");
```

[Back to top](#objective-c-cheat-sheet)

## STL Containers

### Vector

```objcpp
#include <vector>

std::vector<int> numbers;
numbers.push_back(1);
numbers.push_back(2);
numbers.push_back(3);

// Initializer list (C++11)
std::vector<int> nums = {1, 2, 3, 4, 5};

// Access
int first = nums[0];
int second = nums.at(1);  // With bounds checking
int last = nums.back();

// Iteration
for (const auto& num : nums) {
    std::cout << num << " ";
}

// Size operations
size_t size = nums.size();
bool empty = nums.empty();
nums.reserve(100);  // Reserve capacity
nums.resize(10);    // Resize

// Insert and erase
nums.insert(nums.begin(), 0);        // Insert at beginning
nums.erase(nums.begin());            // Erase first element
nums.erase(nums.begin(), nums.end()); // Clear

// With Objective-C objects
std::vector<NSString*> strings;
strings.push_back(@"Hello");
strings.push_back(@"World");
```

### Map

```objcpp
#include <map>
#include <string>

std::map<std::string, int> ages;
ages["Alice"] = 30;
ages["Bob"] = 25;
ages.insert({"Charlie", 35});

// Access with default
int age = ages["Unknown"];  // Creates entry with 0

// Check if exists
if (ages.find("Alice") != ages.end()) {
    // Found
}

if (ages.count("Bob") > 0) {
    // Exists
}

// Iterate
for (const auto& [name, age] : ages) {  // C++17 structured bindings
    std::cout << name << ": " << age << std::endl;
}

// Pre-C++17
for (const auto& pair : ages) {
    std::cout << pair.first << ": " << pair.second << std::endl;
}
```

### Unordered Containers (Hash-based)

```objcpp
#include <unordered_map>
#include <unordered_set>

std::unordered_map<std::string, int> hashMap;
hashMap["key1"] = 100;
hashMap["key2"] = 200;

std::unordered_set<int> hashSet = {1, 2, 3, 4, 5};
hashSet.insert(6);
```

### Other Containers

```objcpp
#include <set>
#include <list>
#include <deque>
#include <queue>
#include <stack>
#include <array>

// Set (ordered, unique)
std::set<int> orderedSet = {3, 1, 4, 1, 5};  // Contains: 1, 3, 4, 5

// List (doubly-linked)
std::list<int> linkedList = {1, 2, 3};
linkedList.push_front(0);

// Deque (double-ended queue)
std::deque<int> deque = {1, 2, 3};
deque.push_front(0);
deque.push_back(4);

// Queue (FIFO)
std::queue<int> queue;
queue.push(1);
queue.push(2);
int front = queue.front();
queue.pop();

// Stack (LIFO)
std::stack<int> stack;
stack.push(1);
stack.push(2);
int top = stack.top();
stack.pop();

// Array (fixed size)
std::array<int, 5> arr = {1, 2, 3, 4, 5};
```

[Back to top](#objective-c-cheat-sheet)

## Smart Pointers

### unique_ptr

```objcpp
#include <memory>

// Create unique_ptr
std::unique_ptr<MyClass> ptr = std::make_unique<MyClass>();
ptr->doSomething();

// Transfer ownership
std::unique_ptr<MyClass> ptr2 = std::move(ptr);  // ptr is now nullptr

// Array version
std::unique_ptr<int[]> arrPtr = std::make_unique<int[]>(10);
arrPtr[0] = 42;

// Custom deleter
auto customDeleter = [](MyClass* p) {
    std::cout << "Custom delete" << std::endl;
    delete p;
};
std::unique_ptr<MyClass, decltype(customDeleter)> customPtr(new MyClass(), customDeleter);
```

### shared_ptr

```objcpp
#include <memory>

// Create shared_ptr
std::shared_ptr<MyClass> ptr1 = std::make_shared<MyClass>();

// Copy (increases reference count)
std::shared_ptr<MyClass> ptr2 = ptr1;
std::cout << "Reference count: " << ptr1.use_count() << std::endl;  // 2

// Automatic cleanup when all references are gone
{
    std::shared_ptr<MyClass> ptr3 = ptr1;
}  // ptr3 destroyed, but object still alive

ptr1.reset();  // ptr1 releases, count = 1
ptr2.reset();  // ptr2 releases, object destroyed
```

### weak_ptr

```objcpp
#include <memory>

std::shared_ptr<MyClass> shared = std::make_shared<MyClass>();
std::weak_ptr<MyClass> weak = shared;

// Check if object still exists
if (auto locked = weak.lock()) {
    // Object is alive, use locked
    locked->doSomething();
} else {
    // Object was destroyed
}

// Check without locking
if (!weak.expired()) {
    // Object still exists
}
```

### Smart Pointers with Objective-C Objects

```objcpp
// Note: Don't use smart pointers with Objective-C objects under ARC!
// ARC manages Objective-C object lifetimes automatically.

// For non-ARC code only:
struct ObjCRelease {
    void operator()(NSObject* obj) {
        [obj release];
    }
};

// This is generally NOT recommended. Use ARC instead.
```

[Back to top](#objective-c-cheat-sheet)

## Passing Information

### Delegate Pattern (Same as Objective-C)

```objcpp
// Protocol declaration
@protocol DataManagerDelegate <NSObject>
- (void)dataManager:(id)manager didLoadData:(NSArray *)data;
@optional
- (void)dataManager:(id)manager didFailWithError:(NSError *)error;
@end

// Class with delegate
@interface DataManager : NSObject
@property (nonatomic, weak) id<DataManagerDelegate> delegate;
- (void)loadData;
@end
```

### Callback Functions (C++ Style)

```objcpp
#include <functional>

// Using std::function for callbacks
class NetworkManager {
public:
    using SuccessCallback = std::function<void(const std::string&)>;
    using ErrorCallback = std::function<void(int errorCode)>;

    void fetchData(SuccessCallback onSuccess, ErrorCallback onError) {
        // Perform network request
        if (success) {
            onSuccess(responseData);
        } else {
            onError(errorCode);
        }
    }
};

// Usage
NetworkManager manager;
manager.fetchData(
    [](const std::string& data) {
        std::cout << "Success: " << data << std::endl;
    },
    [](int error) {
        std::cerr << "Error: " << error << std::endl;
    }
);
```

### NSNotificationCenter (Same as Objective-C)

```objcpp
// Register observer
[[NSNotificationCenter defaultCenter] addObserver:self
                                         selector:@selector(handleNotification:)
                                             name:@"CustomNotification"
                                           object:nil];

// Post notification
[[NSNotificationCenter defaultCenter] postNotificationName:@"CustomNotification"
                                                    object:self
                                                  userInfo:@{@"key": @"value"}];

// Remove observer in dealloc
- (void)dealloc {
    [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```

[Back to top](#objective-c-cheat-sheet)

## User Defaults

Same as Objective-C:

```objcpp
// Store value
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
[defaults setObject:@"Value" forKey:@"MyKey"];
[defaults setInteger:42 forKey:@"MyIntKey"];
[defaults setBool:YES forKey:@"MyBoolKey"];
[defaults synchronize];

// Retrieve value
NSString *value = [defaults stringForKey:@"MyKey"];
NSInteger intValue = [defaults integerForKey:@"MyIntKey"];
BOOL boolValue = [defaults boolForKey:@"MyBoolKey"];
```

[Back to top](#objective-c-cheat-sheet)

## Common Patterns

### Singleton (Objective-C++ Style)

```objcpp
// Objective-C singleton with C++ members
@interface SharedManager : NSObject

+ (instancetype)sharedInstance;

- (std::vector<int>)getNumbers;
- (void)addNumber:(int)number;

@end

@implementation SharedManager {
    std::vector<int> _numbers;
    std::mutex _mutex;  // Thread safety
}

+ (instancetype)sharedInstance {
    static SharedManager *instance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        instance = [[self alloc] init];
    });
    return instance;
}

- (std::vector<int>)getNumbers {
    std::lock_guard<std::mutex> lock(_mutex);
    return _numbers;
}

- (void)addNumber:(int)number {
    std::lock_guard<std::mutex> lock(_mutex);
    _numbers.push_back(number);
}

@end
```

### C++ Singleton

```objcpp
class Singleton {
private:
    static Singleton* instance;
    Singleton() = default;  // Private constructor

public:
    // Delete copy constructor and assignment
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton* getInstance() {
        static Singleton instance;  // Thread-safe in C++11
        return &instance;
    }

    void doSomething() {
        std::cout << "Singleton method called" << std::endl;
    }
};

// Usage
Singleton::getInstance()->doSomething();
```

### PIMPL (Pointer to Implementation)

```objcpp
// Header file (public interface)
// MyClass.h
@interface MyClass : NSObject
- (void)doWork;
@end

// Implementation file
// MyClass.mm
#include <memory>

// Private implementation class
class MyClassImpl {
private:
    std::vector<int> data;
    std::string name;

public:
    void processData() {
        // Complex C++ implementation
        std::sort(data.begin(), data.end());
    }

    void addData(int value) {
        data.push_back(value);
    }
};

@implementation MyClass {
    std::unique_ptr<MyClassImpl> _impl;
}

- (instancetype)init {
    if (self = [super init]) {
        _impl = std::make_unique<MyClassImpl>();
    }
    return self;
}

- (void)doWork {
    _impl->addData(42);
    _impl->processData();
}

@end
```

### Observer Pattern with C++

```objcpp
#include <functional>
#include <vector>
#include <algorithm>

class Observable {
public:
    using Observer = std::function<void(int)>;

    void addObserver(Observer obs) {
        observers.push_back(obs);
    }

    void notify(int value) {
        for (const auto& obs : observers) {
            obs(value);
        }
    }

private:
    std::vector<Observer> observers;
};

// Usage
Observable observable;

observable.addObserver([](int value) {
    std::cout << "Observer 1 received: " << value << std::endl;
});

observable.addObserver([](int value) {
    std::cout << "Observer 2 received: " << value << std::endl;
});

observable.notify(42);
```

[Back to top](#objective-c-cheat-sheet)

## Threading and Concurrency

### Grand Central Dispatch with C++

```objcpp
#import <dispatch/dispatch.h>
#include <vector>
#include <string>

@implementation DataProcessor {
    std::vector<std::string> _data;
}

- (void)processInBackground {
    // Capture C++ member by reference carefully!
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        // Background thread - C++ operations
        std::vector<int> results;
        for (int i = 0; i < 1000; i++) {
            results.push_back(i * 2);
        }
        
        dispatch_async(dispatch_get_main_queue(), ^{
            // Main thread - UI updates
            NSLog(@"Processed %zu items", results.size());
        });
    });
}

@end
```

### std::thread with Objective-C

```objcpp
#include <thread>
#include <mutex>
#include <vector>

class ThreadSafeCounter {
private:
    int count = 0;
    std::mutex mtx;

public:
    void increment() {
        std::lock_guard<std::mutex> lock(mtx);
        count++;
    }
    
    int getCount() {
        std::lock_guard<std::mutex> lock(mtx);
        return count;
    }
};

@implementation MyThreadedClass {
    ThreadSafeCounter _counter;
    std::vector<std::thread> _threads;
}

- (void)startThreads {
    for (int i = 0; i < 5; i++) {
        _threads.emplace_back([self]() {
            for (int j = 0; j < 100; j++) {
                self->_counter.increment();
            }
        });
    }
}

- (void)waitForCompletion {
    for (auto& t : _threads) {
        if (t.joinable()) {
            t.join();
        }
    }
    NSLog(@"Final count: %d", _counter.getCount());
}

- (void)dealloc {
    [self waitForCompletion];
}

@end
```

### std::async and std::future

```objcpp
#include <future>
#include <chrono>

- (void)asyncExample {
    // Launch async task
    std::future<int> future = std::async(std::launch::async, []() {
        std::this_thread::sleep_for(std::chrono::seconds(2));
        return 42;
    });
    
    // Do other work...
    NSLog(@"Waiting for result...");
    
    // Get result (blocks until ready)
    int result = future.get();
    NSLog(@"Result: %d", result);
}

// Multiple async operations
- (void)parallelProcessing {
    auto task1 = std::async(std::launch::async, []{ return 1 + 1; });
    auto task2 = std::async(std::launch::async, []{ return 2 * 2; });
    auto task3 = std::async(std::launch::async, []{ return 3 * 3; });
    
    int sum = task1.get() + task2.get() + task3.get();
    NSLog(@"Sum: %d", sum);  // 2 + 4 + 9 = 15
}
```

### Thread-Safe Singleton

```objcpp
#include <mutex>

class ThreadSafeManager {
private:
    static std::once_flag initFlag;
    static ThreadSafeManager* instance;
    
    std::mutex dataMutex;
    std::vector<int> data;
    
    ThreadSafeManager() = default;

public:
    static ThreadSafeManager* getInstance() {
        std::call_once(initFlag, []() {
            instance = new ThreadSafeManager();
        });
        return instance;
    }
    
    void addData(int value) {
        std::lock_guard<std::mutex> lock(dataMutex);
        data.push_back(value);
    }
    
    std::vector<int> getData() {
        std::lock_guard<std::mutex> lock(dataMutex);
        return data;  // Return copy for thread safety
    }
};

// Initialize static members in .mm file
std::once_flag ThreadSafeManager::initFlag;
ThreadSafeManager* ThreadSafeManager::instance = nullptr;
```

[Back to top](#objective-c-cheat-sheet)

## Memory Management with ARC

### Understanding ARC + C++ Interaction

```objcpp
// ✅ CORRECT: ARC manages Objective-C objects
@implementation MyClass {
    NSMutableArray *_array;        // ARC managed
    std::vector<int> _numbers;     // C++ automatic storage
    std::unique_ptr<Engine> _engine; // C++ smart pointer
}

// ✅ CORRECT: Smart pointers for C++ heap objects
- (instancetype)init {
    if (self = [super init]) {
        _array = [NSMutableArray new];  // ARC handles this
        _engine = std::make_unique<Engine>();  // Smart pointer handles this
    }
    return self;
}
// No dealloc needed! Both are automatically cleaned up

@end
```

### ❌ Common Memory Mistakes

```objcpp
// ❌ WRONG: Don't use smart pointers with ObjC objects under ARC!
// std::shared_ptr<NSString> badIdea;  // NEVER DO THIS!

// ❌ WRONG: Raw C++ pointers without cleanup
@implementation LeakyClass {
    Engine* _engine;  // Raw pointer - who deletes this?
}
- (instancetype)init {
    if (self = [super init]) {
        _engine = new Engine();  // Memory leak if dealloc not implemented!
    }
    return self;
}
@end

// ✅ CORRECT: Either use smart pointers or implement dealloc
@implementation CorrectClass {
    Engine* _engine;
}
- (instancetype)init {
    if (self = [super init]) {
        _engine = new Engine();
    }
    return self;
}
- (void)dealloc {
    delete _engine;  // Manual cleanup required for raw pointers
}
@end
```

### Prevent Retain Cycles with C++ and Blocks

```objcpp
@implementation NetworkManager {
    std::function<void(NSData*)> _callback;
}

// ❌ WRONG: Strong reference to self in std::function
- (void)setupCallbackWrong {
    _callback = [self](NSData* data) {  // Captures self strongly!
        [self processData:data];  // Retain cycle!
    };
}

// ✅ CORRECT: Use weak reference
- (void)setupCallbackCorrect {
    __weak typeof(self) weakSelf = self;
    _callback = [weakSelf](NSData* data) {
        __strong typeof(weakSelf) strongSelf = weakSelf;
        if (strongSelf) {
            [strongSelf processData:data];
        }
    };
}

@end
```

### C++ Objects in Objective-C Collections

```objcpp
// You cannot store C++ objects directly in NSArray/NSDictionary
// Workaround: Wrap in NSValue or use a wrapper class

// Option 1: NSValue (for POD types)
struct Point { float x, y; };
Point p = {10.0f, 20.0f};
NSValue *pointValue = [NSValue valueWithBytes:&p objCType:@encode(Point)];

// Retrieve
Point retrieved;
[pointValue getValue:&retrieved];

// Option 2: Wrapper class for complex C++ objects
@interface CppWrapper<T> : NSObject
@property (nonatomic, readonly) T* cppObject;
- (instancetype)initWithObject:(T*)object;
@end

// Usage
auto engine = std::make_shared<Engine>();
CppWrapper<Engine> *wrapper = [[CppWrapper alloc] initWithObject:engine.get()];
[array addObject:wrapper];
```

[Back to top](#objective-c-cheat-sheet)

## Wrapping C++ Libraries

### Basic C++ Library Wrapper Pattern

```objcpp
// === ImageProcessor.hpp (Pure C++ header) ===
#pragma once
#include <string>
#include <vector>

namespace imagelib {

class ImageProcessor {
public:
    ImageProcessor();
    ~ImageProcessor();
    
    bool loadImage(const std::string& path);
    void applyFilter(const std::string& filterName);
    std::vector<uint8_t> getProcessedData() const;
    int getWidth() const;
    int getHeight() const;

private:
    struct Impl;
    std::unique_ptr<Impl> pImpl;
};

} // namespace imagelib
```

```objcpp
// === RPImageProcessor.h (Public Objective-C interface) ===
// ⚠️ NO C++ here! Pure Objective-C for compatibility
#import <Foundation/Foundation.h>
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface RPImageProcessor : NSObject

- (BOOL)loadImageAtPath:(NSString *)path;
- (void)applyFilterNamed:(NSString *)filterName;
- (nullable UIImage *)processedImage;

@property (nonatomic, readonly) NSInteger width;
@property (nonatomic, readonly) NSInteger height;

@end

NS_ASSUME_NONNULL_END
```

```objcpp
// === RPImageProcessor.mm (Implementation with C++) ===
#import "RPImageProcessor.h"
#include "ImageProcessor.hpp"
#include <memory>

@implementation RPImageProcessor {
    std::unique_ptr<imagelib::ImageProcessor> _processor;
}

- (instancetype)init {
    if (self = [super init]) {
        _processor = std::make_unique<imagelib::ImageProcessor>();
    }
    return self;
}

- (BOOL)loadImageAtPath:(NSString *)path {
    if (!path) return NO;
    return _processor->loadImage([path UTF8String]);
}

- (void)applyFilterNamed:(NSString *)filterName {
    if (!filterName) return;
    _processor->applyFilter([filterName UTF8String]);
}

- (UIImage *)processedImage {
    auto data = _processor->getProcessedData();
    if (data.empty()) return nil;
    
    NSData *imageData = [NSData dataWithBytes:data.data() 
                                       length:data.size()];
    return [UIImage imageWithData:imageData];
}

- (NSInteger)width {
    return _processor->getWidth();
}

- (NSInteger)height {
    return _processor->getHeight();
}

@end
```

### Handling C++ Callbacks in Objective-C

```objcpp
// C++ library with callback
class DownloadManager {
public:
    using ProgressCallback = std::function<void(float progress)>;
    using CompletionCallback = std::function<void(bool success, const std::string& error)>;
    
    void downloadFile(const std::string& url,
                     ProgressCallback onProgress,
                     CompletionCallback onComplete);
};

// Objective-C wrapper
@interface RPDownloadManager : NSObject

- (void)downloadFileAtURL:(NSString *)url
                progress:(void (^)(float progress))progressBlock
              completion:(void (^)(BOOL success, NSError *error))completionBlock;

@end

@implementation RPDownloadManager {
    std::unique_ptr<DownloadManager> _manager;
}

- (void)downloadFileAtURL:(NSString *)url
                progress:(void (^)(float))progressBlock
              completion:(void (^)(BOOL, NSError *))completionBlock {
    
    // Copy blocks to ensure they survive async operation
    auto progressCopy = [progressBlock copy];
    auto completionCopy = [completionBlock copy];
    
    _manager->downloadFile(
        [url UTF8String],
        // Progress callback
        [progressCopy](float progress) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if (progressCopy) progressCopy(progress);
            });
        },
        // Completion callback  
        [completionCopy](bool success, const std::string& error) {
            dispatch_async(dispatch_get_main_queue(), ^{
                NSError *nsError = nil;
                if (!success && !error.empty()) {
                    nsError = [NSError errorWithDomain:@"DownloadError"
                                                  code:-1
                                              userInfo:@{NSLocalizedDescriptionKey: 
                                                  [NSString stringWithUTF8String:error.c_str()]}];
                }
                if (completionCopy) completionCopy(success, nsError);
            });
        }
    );
}

@end
```

### Swift Interoperability

```objcpp
// To use your Objective-C++ wrapper from Swift:

// 1. Create a bridging header (YourApp-Bridging-Header.h)
#import "RPImageProcessor.h"    // ✅ Only import the .h file!
// #include "ImageProcessor.hpp"  // ❌ NEVER include C++ headers!

// 2. Use from Swift
// let processor = RPImageProcessor()
// processor.loadImage(atPath: "/path/to/image.jpg")
// processor.applyFilter(named: "blur")
// let image = processor.processedImage()
```

[Back to top](#objective-c-cheat-sheet)

## Common Pitfalls

### ❌ Pitfall 1: C++ in Header Files

```objcpp
// ❌ WRONG: C++ types in public header
// MyClass.h
#import <Foundation/Foundation.h>
#include <vector>  // ❌ This breaks pure Objective-C files!

@interface MyClass : NSObject
@property (nonatomic) std::vector<int> numbers;  // ❌ Won't compile in .m files
@end

// ✅ CORRECT: Hide C++ in implementation
// MyClass.h
#import <Foundation/Foundation.h>

@interface MyClass : NSObject
- (void)addNumber:(int)number;
- (NSArray<NSNumber *> *)allNumbers;
@end

// MyClass.mm
#include <vector>

@implementation MyClass {
    std::vector<int> _numbers;  // ✅ C++ hidden in implementation
}
@end
```

### ❌ Pitfall 2: Forgetting .mm Extension

```objcpp
// If you see errors like:
// "Expected ';' after top level declarator"
// "Unknown type name 'std'"
// "Use of undeclared identifier 'vector'"

// Solution: Rename file from .m to .mm!
// MyClass.m  →  MyClass.mm
```

### ❌ Pitfall 3: Mixing Exception Models

```objcpp
// ❌ WRONG: C++ exception escaping to Objective-C
- (void)riskyMethod {
    std::vector<int> v;
    int x = v.at(100);  // throws std::out_of_range!
    // This will crash if not caught!
}

// ✅ CORRECT: Catch C++ exceptions at the boundary
- (BOOL)safeMethod:(NSError **)error {
    try {
        std::vector<int> v;
        int x = v.at(100);
        return YES;
    } catch (const std::exception& e) {
        if (error) {
            *error = [NSError errorWithDomain:@"CppError" 
                                         code:-1 
                                     userInfo:@{NSLocalizedDescriptionKey: 
                                         [NSString stringWithUTF8String:e.what()]}];
        }
        return NO;
    }
}
```

### ❌ Pitfall 4: String Encoding Issues

```objcpp
// ❌ WRONG: Assuming UTF-8 always works
std::string cppStr = [nsString UTF8String];  // Crashes if nsString is nil!

// ✅ CORRECT: Always check for nil
std::string safeConvert(NSString *nsString) {
    if (!nsString) return "";
    const char *utf8 = [nsString UTF8String];
    return utf8 ? std::string(utf8) : "";
}

// ✅ CORRECT: Handle non-UTF8 strings
std::string convertAny(NSString *nsString) {
    if (!nsString) return "";
    NSData *data = [nsString dataUsingEncoding:NSUTF8StringEncoding 
                          allowLossyConversion:YES];
    return std::string((const char *)[data bytes], [data length]);
}
```

### ❌ Pitfall 5: C++ Object Lifecycle in ObjC

```objcpp
// ❌ WRONG: C++ constructor not called!
@implementation MyClass {
    std::string name;  // Default constructed to empty string ✅
    Engine* engine;    // NOT initialized! Contains garbage! ❌
}

- (instancetype)init {
    if (self = [super init]) {
        // engine is uninitialized garbage here!
    }
    return self;
}

// ✅ CORRECT: Always initialize C++ pointers
@implementation MyClass {
    std::string name;              // OK - default constructed
    Engine* engine = nullptr;      // ✅ Explicit initialization
    std::unique_ptr<Engine> safe;  // ✅ Smart pointer - auto nullptr
}
```

### ❌ Pitfall 6: BOOL vs bool

```objcpp
// ❌ WRONG: Assuming BOOL and bool are the same
BOOL objcBool = 256;  // BOOL is signed char, so 256 becomes 0 (NO)!
if (objcBool) { }     // This is FALSE!

bool cppBool = 256;   // bool is true for any non-zero
if (cppBool) { }      // This is TRUE

// ✅ CORRECT: Be explicit
BOOL objcBool = (value != 0) ? YES : NO;
bool cppBool = (value != 0);
```

[Back to top](#objective-c-cheat-sheet)

## Debugging Tips

### LLDB Commands for Objective-C++

```lldb
# Print C++ vector
(lldb) p _numbers
(lldb) p _numbers.size()
(lldb) p _numbers[0]

# Print std::string
(lldb) p _cppString
(lldb) p _cppString.c_str()

# Print std::map
(lldb) p _cache
(lldb) p _cache.size()

# Call C++ methods
(lldb) expr _engine->getStatus()

# Print Objective-C object
(lldb) po self
(lldb) po _array

# Mixed debugging
(lldb) expr [self description]
(lldb) expr _processor->getName().c_str()
```

### Useful Preprocessor Checks

```objcpp
// Check if compiling as Objective-C++
#if defined(__cplusplus) && defined(__OBJC__)
    NSLog(@"Compiling as Objective-C++");
#elif defined(__cplusplus)
    std::cout << "Compiling as C++" << std::endl;
#elif defined(__OBJC__)
    NSLog(@"Compiling as Objective-C");
#else
    printf("Compiling as C\n");
#endif

// Check C++ standard version
#if __cplusplus >= 202002L
    // C++20 features available
#elif __cplusplus >= 201703L
    // C++17 features available
#elif __cplusplus >= 201402L
    // C++14 features available
#elif __cplusplus >= 201103L
    // C++11 features available
#endif
```

### Debug Logging Utility

```objcpp
#ifdef DEBUG
    #define CPP_LOG(msg) std::cout << "[C++] " << msg << std::endl
    #define OBJC_LOG(msg) NSLog(@"[ObjC] %@", msg)
    #define MIXED_LOG(cppPart, objcPart) \
        NSLog(@"[Mixed] %s - %@", (cppPart).c_str(), objcPart)
#else
    #define CPP_LOG(msg)
    #define OBJC_LOG(msg)
    #define MIXED_LOG(cppPart, objcPart)
#endif

// Usage
CPP_LOG("Vector size: " + std::to_string(_data.size()));
OBJC_LOG(@"Array count: " + [@(_array.count) stringValue]);
MIXED_LOG(_engine->getName(), self.description);
```

[Back to top](#objective-c-cheat-sheet)

---

## Key Differences: Objective-C vs Objective-C++

| Feature            | Objective-C     | Objective-C++            |
| ------------------ | --------------- | ------------------------ |
| File Extension     | `.m`            | `.mm`                    |
| C++ Classes        | ❌              | ✅                       |
| Templates          | ❌              | ✅                       |
| Namespaces         | ❌              | ✅                       |
| STL Containers     | ❌              | ✅                       |
| Lambda Expressions | ❌ (use Blocks) | ✅                       |
| Smart Pointers     | ❌              | ✅                       |
| Exception Handling | @try/@catch     | try/catch + @try/@catch  |
| Boolean Type       | BOOL (YES/NO)   | bool + BOOL              |
| String Type        | NSString\*      | std::string + NSString\* |

## Best Practices

1. **Keep C++ in Implementation Files**: Only expose Objective-C interfaces in `.h` files to maintain compatibility with pure Objective-C code.

2. **Use PIMPL**: Hide C++ implementation details using the Pointer to Implementation pattern.

3. **String Conversion**: Create utility functions for NSString ↔ std::string conversion.

4. **ARC Compatibility**: Don't mix smart pointers with Objective-C objects under ARC.

5. **Thread Safety**: Use std::mutex or @synchronized for thread-safe code.

6. **Memory Management**: Let ARC handle Objective-C objects, use smart pointers for C++ objects.

7. **Naming Conventions**:
   - Objective-C: camelCase for methods, CapitalCase for classes
   - C++: follow your project's C++ style guide

[Back to top](#objective-c-cheat-sheet)
