# LECTURE 4

## наследование
override ~ C#(for virtual)  

down-casting and up-casting(parent = new chuld and child = new (child)parent)

**logger** + warning, trace(вообще все изменения)

если у нас фигня класс, то можно не писать десткрутор(override ~), он сам справится

если есть возможность лучше не использовать указатели

можно присвоить virtual метод нуль, то есть мы не хотим его реализовывать  
получим *абстрактный* класс  
наебали, реализовать можно

```cpp
class Obj{
    public:
    virtual ~Obj() = 0;
}
Obj::~Obj(){}
//просто пустой виртуальный класс
```

### std::variant