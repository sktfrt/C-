# PRACTIC 6

## манипуляторы (лаба)
`<< std::(ios::?)hex <<` - изменяет состояние потока
> все лежат в `iostream`, `iomanip`  

1) булевы; 1/0 - true/false
2) дробь (знаки после запятой); *floatfield* 
3) hex, oct, dec; *basefield*
4) ввод: `std::ws`, `noskips`
5) setw(n), setfill('*'), left, right; *adjusfield*
6) `(no)showpos`
7) `std::endl`, `std::fflush`

```cpp
std::cout << std::ios::hex << ...;
действует до std::resetflags //или пока мы не поменяем
// потоки всегда одни и те же, мы не создаем новый
```

`std::cout::setf(std::ios::hex)` - выставить в такой то поток такой флаг  
но чтобы поменять аргумент и не получить коллизию `(std::ios::hex, std::basefield)`  
фигня

`setw()` действует только на след вывод, он такой один

```cpp
ostream& operator<<(ostream& o, ostream& (foo*)(ostream& o)){}
```

**laba**
```cpp
bool x;
cin >>read_bool(x) >> ..;

struct read_bool {
    bool x_;
    explicit read_bull(bool x) x_(x) {};

    istream& operator>>(istream& i, read_bool b){
        in.>> b.x;
    }
}
```

```cpp
file << x >>
//слева навправо действует
//так не надо(по ТЗ)
```

*c c++11 есть приколы*  
`put_money()` , `put_time()`, `get_money()`, `get_time()`, `std::cout::imbue()`

## basic_string and vector

## template

в след лабе нужно будет `placement new`  