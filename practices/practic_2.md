# PRACTICE 2

при перегрузке функций можно словить ошибку компиляции(но ее сначала надо найти)

## operators

```cpp
Coord: x, y
Coord operator+(const Coord &f,const Coord &s){
    Coord new_c;
    new_c->x = f->x + s->x;
    //y
    return new_c
}

Coord operator+(const Coord& other){
    new_c->x = this->x + other->x
    return new_c
}
```

= += -= ++ -- -> [] () - обычно внутри класса  

## operator new

new: 
1) выделяет память 
2) вызывает конструктор
delete:
1) вызывает деструктор
2) очистка памяти

выделение памяти = operator new, и ее можно переопределить!(вне класса онли)  
delete аналогично  

1) new Coord() - база
2) new(std::nothrow) Coord(); - без исключений
3) new Coord[5] - 5 конструкторов + 5 деструкторов
4) placement new
```cpp
// *buffer
buffer = new(buffer) Coord(); //показываем куда выделено, то есть new сама не выделяет
buffer->Coord(); //вызываем десктруктор
delete buffer;
```
---
```cpp
Coord* operator new(size s){
    ptr = malloc(s)
    if (ptr == NULL){
        throw std::bad_alloc;
    }
}

Coord* operator new(size s) noexcept{ //эта функция никогда не будет бросать исключения
}

try{
    return ::operator new(s);
}
catch{
    return nullptr;
}
```
---
bool operator==() =default; - страндартная реализация
## most vexing parsing
example:
```cpp
struct Timer{};
struct TimeK{
    explict TimeK(Timer timer){...}
};

main(){
    TimeK time_k(Timer()); //может быть либо создание конткрутора Timer(), либо объявление функции time_k(func)
}//TimeK time_k(Timer()), любое из {{}}

// OR

int x();// либо конструктор х, либо функция х

// РЕШЕНИЕ
int x{}; //ТОЛЬКО конструктор
```

## mutable
```cpp
MyClass:
    int x;
    mutable void print() const{ //!!!!!!!!
        x = ...;
        printf("%d", x); 
    }
```