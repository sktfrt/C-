# EXTRA 15 LECTURE

*по прошлой лекции:* delete нужно делать из плагина  

## разбор тестов💀💀💀

```cpp
T x(y);
T x = y; //тоже конструктор, но не explicit
```

```cpp
MyClass(T a, T b)
    : _a(a), _b(b)
{}
```

```cpp
delete this; //💀
```

`delete` работает с `nullptr`

```cpp
list::~list(){
    delete next;
}
// проблема, что при больших данных будет stackoverflow
```

деструкторы всегда вызываются в обратном порядке

специальные функции - конструкторы, деструкторы, кк, кп и проч

## хвостовая рекурсия(tail call), хвостовая опитимизация(tail call optimization)
```cpp
int fact(int n, int r = 1){
    if (n == 0) return r;
    return fact(n - 1, r * n)
}
//create new stack
```

**godbolt** - phrases + site