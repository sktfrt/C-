# LECTURE 5

## множественное наследование

если у нас одинаковые поля и методы, то придется явно указвать из какого класса берем  
```cpp
void printPrice(){return Readble::price}
```

**Diamond problem** - а если у нас класс Readble еще наследуется от чего то?  
можно добавить virtual, тогда класс будет один на всех детей
```cpp
public Readble: public virtual IOBase{}
```

## interfaces
полностью виртуальные методы(~ C#)
```cpp
class Hasheble{
    public:
    virtual size_t getHash() = 0;
    virtual ~Hasheble(){}
};
```

## name conflicts
как избежать?  
1) изменить имя(но не очень, подходит только для маленьких проектов)
2) использовать вложеные типы(идеально!)
```cpp
class List{
    struct Node{
        int data;
        Node* next;
    };

    Node* head;
};
```

## namespace
~C#  

```cpp
namespace xml{
    class Node {...};
    class Parser{...};
}

namespace json{
    class Node {...};
    class Parser{...};
}

json::Parser parser("File.json");
```

нельзя создавать объекты, можно использовать в любом колве файлов  

```cpp
можно вместо 
json::Parser parser("File.json"); 
заменить на 
using namespace xml;
тогда 
Parser parser("");
но так не делают
```

**не писать using namespace std;**

можно сделать вложенные namespace-ы  
можно создать для вложенный nspc синоним
```cpp
namespace boost{
    namespace multi{...}
}

namespace bmp = boost::multi;
```
---
**global namespaces**  
*ничего, пустота реал*::method() - обращение к глобальному пространству имен
---

у nmspc можно пропустить имя(aнонимное пространство имен) - это равносильно static в си

```cpp
namespace{
    void helper2()

    class Iternal{};
}
```


```cpp
namespace muLib{
    inline namespace{}
}
передает объекты из него в родительский namespace, но это все ранво разные пространства имен
```

```cpp 
вместо typedef используют using Obj = int;  
```

## стандартная библиотека 

## шаблоны
```cpp
template<typename T>
class scoped_ptr{
    T* count;
}
```