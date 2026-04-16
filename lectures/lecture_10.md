# LECTURE 10

*C++11*

## приведение типов

### static_cast
* **downcasting**
* **к void**
  
### reinterpret_cast
> любая память в любую память
---

    `std::uintptr_t` - тип, который гарантированно хранит место под указатель  
---

### const_cast  
> убрать или добавить `const` 

```cpp
const at() const{};
at() {};
//не хотим будлировать код
//можно
const at() const{};
at() {
    return const_cast<Value&>(const_cast<const map&>(*this).at(key));
}
```
### dynamic_cast
* приведение базовго класса к дочернему   
> при ошибке возвращает либо нулевой указатель, либо `std::bad_cast`  

- работает только для классов с виртуальными методами(использует таблицу виртуальных функций)

> технология `RTTI`

## typeid
* `std::type_info` в `<typeinfo>`
* чтобы достать по конкретному обекту используем `typeid`

*неудобный*

- `std::type_index` - обертка на `type_info`

- `demangle` - читаемое название из `<boost/core/demagle.hpp>` (не в стандартной бибилиотеке)

## rvalue and lvalue
- `lvalue` - можно что то присвоить, имеют адрес в памяти
- `rvalue` - нельзя, какие то времененные значения

## rvalue - ссылки
- `T&&` - rvalue - ссылка
```cpp
Array(Array&& other) : data(other.data), size(other.size){
    other.data = nullptr ; other.size = 0;
}
// у нас - массив, у него nullptr 
Array a3(Array(200)); // Array a3(rvalue&&)
Array& operator=(Array&& other) {...}
```
## move семантика
`consume(static_cast<vector<int>&&> (v))`  
*много писать*

* `std::move` - & -> &&

- `return a;` - автоматический `move`  

## perfect forwarding
* существует `T&&` - universal reference  
* вместе с `std::forward` принмиает неизвестный набор параметров  передать в другую функцию, запоминая `rvalue / lvalue`    

## вывод типов
- `auto` 😈
- `decltype(x)` подставляет вместо себя тип выражения (x)(п*очитать документацию надо*)
```cpp
decltype(10) i = 49; //int
```

## for
```cpp
for (int x : v) {...}
```

*не очевидно*
```cpp
void foo(T&& x){
    x //lvalue
    T a = move(x) //rvalue
}
```