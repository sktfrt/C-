# LECTURE 3
{} - scoup  

```cpp
a = 2;
b = 3;
max(a, b); // до конца мейна
max(2, 3); //до ;

это работает для всех типов данных
```

в плюсах есть параметры функции по умолчанию, они должны быть указаны в хэдере  

**прикол с питоном**
```py
def foo(a = []):
    return a.append(0)

foo() #[0]
foo() #[0, 0]
foo() #[0, 0, 0]

в с++ так не работает
```

## new, delete

через new BigInt[100]; нельзя вызвать не дефолтный конструктор  
то же самое

## RAII(умные указатели)
### scoped_ptr
слишком много delete!
```cpp
scoped_ptr p = new Object(); //обертка на класс
p->doSmth();// сам вызывает delete
```
```cpp
class scoped_ptr:
    scoped_ptr operator= (...) = delete // нельзя реализовывать!

scoped_ptr* scoped_ptr::operator ->(..){return ptr}
// если не указатель, то беск цикл
```
### unique_ptr
нельзя копировать, можно перемещать, можно передаватьвладение, один указатель = один объект
### shared_ptr
можно копировать  
как реализовать?  
храним счетчик ссылок

```std::make_shared``` - делаем shared_ptr от new Object  
## наследование
```cpp
class ColoredButton : public Button{...
    Button::Click(); // вызов метода из родителя
}
```
указатель на ColoredButton равен укзаателю на Button
**button**  
**---------------**  
------|----------|-------  
cap|action |color  
**----------------------**  

**coloredButton**

### virtual
```cpp
class Button{
    public:
    virtual void draw(); //ищет правльный метод среди всех наследников
    virtual ~Button(); //правило
}
```

## public, private, protected
```cpp
...
protected:
    const char* caption_;

для этого класса и всех его наследников
```
---
```cpp
class ColoredButton : public Button{} // все останется так же
class ColoredButton : private Button{} //private <= public, protected
class ColoredButton : protected Button{} // protected <= public
```
---
```cpp 
class A : B == class A : private B
struct A : B == struct A : public B
```