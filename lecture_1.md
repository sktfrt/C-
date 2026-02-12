# LECTURE 1

eel.is - стандарт с++(не нада) // c++ standart draft

---

.cpp .hpp

## отличия от си

`c++
int *pi = ...
int *pc = ...
pi = (int*)pc // можно в с++
void *pv = pc
pi = pc // нельзя
pc = pi
`
---

`c++
// malloc
int *pi = new int 
int *array = new int[N] // sizeof N
//free
delete pi 
delete [] array
`

malloc <==> free
new  <==> delete
new[] <==> delete[]

## ссылки

int& - ссылка(адрес в памяти)

`
int x = ...
int &ref = x;
int &ref2; // error
// переопределения не существует, != NULL

int y = 42;
ref = y; // присвание значения 42, но ссылка все еще на х
`
---
`
int *p = ..;
int &ref = *p; // ref указ на тот же объект
`
---
`
const int &cref = x;
cref = 42; //error

const int y = ...;
int &ref = y; // error
`
---

`
void swap(int &x, int &y){
    int temp = x;
    x = y;
    y = temp;
} // все просто

int a = 3, b = 5;
swap(a, b); // нужно смотреть  на своп, чтобы понять что меняется
`


## перегрузка функций

можно!

`
int max(int a, int b);
int max(int a, int b, int z);

double max(int x, int y) // error, аргументы должны отличаться
`

### name mangling(сборка перегруженных функций линковщиком)

на линукс можно узнать mangled имена 
`bash
readelf -s file.o
`

например
`
int max(int a, int b) // -> _Z3maxii
int max(int a, int b, int z) // _Z3maxiii
`
---
`
extern "C" int max(...) // БЕЗ name mangling
`

## ООП
### Инкапсуляция в с++ (классы)
`
class Array{
    int *data;
    size_t size;

    void set(size_t index, int value); // в си нельзя
    void fill(int value);
}
`

---

`
int *arr = new int[size];
что то
delete[] arr;
`
не очень хорошо, много нужно помнить

лучше
`
class Array{
private: // только в классе
    size_t size;
public:
    Array(size_t, size); // конструктор
    ~Array(); // деструктор

    int get(...);
}
`
---
`
//array.hpp
//реалтзация конструктора:
Array::Array(size_t size){
    this->size = size; // <=> this.size C#
    data = new int[size];
}
// деструктор
Array::~Array{
    delete[] data;
} 
//реализация методов
int Array::get(size_t index){
    return data[index];
}

void Array::set(size_t index, int value){
    data[index] = value;
}
`
---
`
#include <array.h>

void test(){
    Array a(100) // конструктор массива а размера 100
    Array b; // error

    a.data[10] = 42 // error, data is private
    a.set(10, 42) // ok
    // a.~Array делается само
}
`
названия аналогично С#

`
class Array{
    public:
    //inline, можно если очень маленькая
    size_t get_size(){
        return size;
    }
    //перегружать поля нельзя, так же как и поля с функциями
}
`
приватные поля обычно обозначаются mSize или size_ (_size нельзя)
можно перегружать конструкторы
nullptr лучше чем NULL

`
...
Array() // коструктор
...

Array a; //OK, вызов дефолтного
Array a(); //error, объвление функции
`

деструктор нельзя перегрузить

## констр/десткр класса всегда вызывают констр/десткр всех полей