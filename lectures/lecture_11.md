# LECTURE 11

## Initializations
* default - `Type x;` - заполняет фигней
* value - `Type x{};` - заполняет нулевыми байтами/нулем
* direct - `Type(a, b);`
* copy - `Type x = a;`
* list - `Type x{a, b}` or `Type x = {a, b};` - вызов конструктора (a, b) (если есть) || инициализация полей значениями {a, b} по порядку 

* `std::initialazer_list<T>` - специальный шаблонный класс для инициализации контейнеров
```cpp
class ..
public:
    my_container(std::initializer_list<int> l) {...}

my_container c = {1, 2, 3} // hurrey!!
```

`final`, `std::tuple`  
> class template argument deduction

## lambda
`[список захвата](аргументы){тело функции};` - тело может быть сколь угодно большим
```cpp
auto sqr = [](int x){ return x * x; }

std::sort(array.begin(), array.end(), [](int x, int y){ return abs(x) < abs(y); })

int ref = 15;
std::partition(arr.begin(), arr.end(), [ref](int x){ return x < ref; }) //copy
...[&ref] // синтаксис захвата по ссылке, не взятие по ссылке!!!!
...[y = ref * 10] // так можно передать и указатель

[count = 0](int x) mutable{ ++count; return x < 15;} // так как по default поля const

[=](int x){ return a < ref; } // find by value
[&].. // by reference

[](int x) -> int { return x*x; } // showing return type
```

> lambda > func object

## std::function
хотим передавать указатель но функцию, но еще с данныим  
```cpp
std::function<int(int)> sqr = [](int x){ return x * x; }
```

> type erasure

## процессы и потоки
`std::thread`  
лучше узнать размер кэш линии, и отдать первую часть вектора до нее, вторую - после  
еще лучше использовать `srd::transform`  