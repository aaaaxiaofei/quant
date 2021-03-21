# C++ 面试题
[现代c++11教程](https://changkun.de/modern-cpp/zh-cn/02-usability/index.html)
## c++11

### Deprecate
- char* p = "hello"
- auto_ptr -> unique_pointer // auto_ptr support copy, and old pointer points to NULL
- register int i = 0; // deprecated but still reserved as key word
- bool++ deprecated

### nullptr
'NULL' equals to '0', or '(void*)0'

### constexpr 
- Initialize array
- Calculate at compile time

### initializer_list
```
#include <initializer_list>
class MagicFoo {
public:
    std::vector<int> vec;
    MagicFoo(std::initializer_list<int> list) {}

int main() {
	MagicFoo magicFoo = {1, 2, 3, 4, 5};
	Foo foo2 {3, 4};
}
```

### tuple
```
#include <tuple>
tuple<int, double, bool, int> tp(1, 2.2, true, 3);

int n = tuple_size<decltype(tp)>::value;
cout << get<0>(tp) << ", "
// Cannot iterate
```

### 类型推导
- auto: cannot be used as int f(auto a, auto b); Cannot use for array `auto arr[10] = {arr}`
- decltype: deduce type is_same<decltype(x), int>::value
```
template<typename T, typename U>
auto add2(T x, U y) -> decltype(x+y){ // After c++14, we can remove delctype
    return x + y;
}
```

### std::bind

### if/switch declare variable
- if (vector<int>::iterator it = ...)

## ================= Class =======================

### override
- virtual: declare that this function can be override by a derived class
- override: show this function is overriding the same function from base class (type check)
- final
	- after member function, means no more override
	- class A final {}; means no more inheritance for class

# Delegating constructors
```
    Base() {
        value1 = 1;
    }
    Base(int value) : Base() { // 委托 Base() 构造函数
        value2 = value;
    }
```

### Constructor
- Magic() = default; // 显式声明使用编译器生成的构造
- Magic& operator=(const Magic&) = delete; // 显式声明拒绝编译器生成构造

### public, protected, private inheritance

### Throw in constructor/destructor
- Can throw in constructor, but make sure to free the memory (smart pointer or call destructor)
- Destructor doesn't allow throw


## ============== Pointers ======================
### Smart Pointers


## ========================= Template ===================

### typename 
- Define the type in template. To replace class.

### template 别名
`using TrueDarkMagic = MagicType<std::vector<T>, std::string>;`

### default template input types
`template<typename T = int, typename U = int>`

### Variadic Templates / parameter pack
```
template<typename ... T>
auto sum(T ... t) {
    return (t + ...);
}
```

## =================== Container ====================

### Vector release unused memory
- shrink_to_fit()

### std::array
Fixed size. Not like vector, don't waste extra memory. can use stl sort etc

### forward_list (no size() function)

## ==================== Lambda =========================




## ======================== Other =======================
### extern
- extern c: c++编译C代码
- Declare gloable variable in header, defined later in a source


### Cast
static_cast、reinterpret_cast、const_cast

### Overloading vs Overriding
- Overloading allows different methods to have the same name, but different signatures
- Overriding: overriding is a feature that allows us to have a same function in child class which is already present in the parent class
	- Why cannot change overriding return type: Overriding essentially means that either the Base class method or the Derived class method will be called at run-time depending on the actual object pointed by the pointer. It implies that:i.e: Every place where the Base class method can be called can be replaced by call to Derived class method without any change to calling code.

### enum
强枚举类型，
enum class new_enum : unsigned int {}

### noexcept
虽然noexcept修饰的函数通过std::terminate的调用来结束程序的执行的方式可能会带来很多问题，比如无法保证对象的析构函数的正常调用，无法保证栈的自动释放等，但很多时候，“暴力”地终止整个程序确实是很简单有效的做法。

### static 
