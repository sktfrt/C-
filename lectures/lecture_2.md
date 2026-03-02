# LECTURE 2

## copy constructor
- сделать в лоб Array copy();
```
Array a(10);
Array b = a; //проблема! теперь и a и b указывают на одно и то же место в памяти
```
```
...
public:
...
Array(const Array& other){
    //copy
}
Array a(10);
Array b = a; 
```
---
передача функции по значению или return это тоже кк
```
Array makeArr(){
    ...
    return a; //вызов кк
}

void print(Array a){
    ....
}

Array a(10);
print(a) // вызов кк
```
---
```
public:
Array(Array other); //бесконечная рекурсия
```

## Оператор присваивания(copy assignment)
```
...
public:
Array operator = (const Array& other);
}

Array& Array::operator = (const Array& other){
    //copy
}
```
a = b = c <=> a = (b = c)
---
кк это оп без проверки и удаления даты
```
void print(Array arr){ ... }
print(10) // неявное преобразование size_t -> Array

Array a = 10 // ~ Array a(10)

Arrat foo(){
    ...
    return 10; // тоже неявное преобразование
}
```
хотим запретить!!!!!!!!!!!!!!!
```cpp
class Array {
    public:
    explicit Array(size_t size);
    ...
};

Array(10) // вызов констркутора
Array a = 10 //error
print(10)//error
Array foo(){
    ...
    return 10; //error
}
```
---
```cpp
Array makeArr(){
    ...
    return Array(10);
}
```
функция заводит на стеке место под возвращаемое занчение и передает его адрес, помле копирует. 
Хотим без копирования
```
//RVO
Array make(){
    Array array(10);
    ...
    return array
}
```
все равно плохо, хотим не создавать копию 
(URVO обязателен)
NRVO

## конструктор полей
есть по умолчанию но ничо не делает
```cpp
class Vecor(){
    Vector(float a, floan b);
};

class RigidBody{
    RogotBody(Vector a)// error! нет дефолтного конструктора
}
```
лечим
```
RigidBody(float a) : position(0.f, 0.f, 0.f) // объявляем
,rotation() //??
```
**в теле конструктора все поля уже созданы и проиницилизированы**

## const
```
const char[] a // baza
const *char[] a = "Hello"; // делаем память конст
char[] b = "Hello"; //error
```
---
все конст поля нужно проинилизировать как и в примере с вектором
---
```cpp
size_t get_size() const {
    return size;
}
//пишем когда ничо не меняем
```
---
```
const Array array(10);
//можно вызывать только конст методы
```
const class делает все поля по умолчанию конст
## mutable
озаначает что поле можно менять  из конст методов
```
class Array{
    mutable Array values;
    ...
    const Array& get() const {
        чото меняем 
        ок!
    }
}
```

## операторы
### + - += ..
- операторы можно перегружать(только если переменная класс)
определим оператор млоение для длинной арифметики
```cpp
BigInt opeartor+(const BigInt& a, const BigInt& b){
    ....
}
BigInt a, b;
BigInt c = a + b; //operator+(a, b), a.operator+(b)
```
---
```cpp
BigInt a = 10, b = 20;
a + b; // ok
a + 3; // ok
3 + a; //error в реализации как метод, в свободной функции окей
```
при возможности лучше свободные функции
- оператор доступа по индексу
```
int operator[](size_t index) const {return data[index]}
&int operator[](size_t index) {return data[index]}
```
---
можно в С++23
```
float& operator[](size_t row, size_t col){...}
arr[3, 4] = 3.1312312321f // до С++23 это оператор ,
---
как перегрузить опертор ++?
```cpp
operator++() // prefix
operator++(int) //postfix{
    //this->operator++();
    Bigint copy(*this);
    ++(*this);
    return copy;
}
```
### < > =
релизуем <, ==, а остальные через них
**spaceship operator <=> - возвращает особый тип из 3х значений(больше меньше равно)**
### оператор приведения
```cpp
operator double() const { // с explicit позволяет только явное приведение
    ...
}

BigInt x = 10;
x = pow(x, 1000);
double(x);
```

### operator bool
```cpp
explicit operator bool() const {
    return (*this) != 0;
}
```