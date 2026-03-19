# LECTURE 6

## шаблоны
```cpp
class Array{
    T getT();
}

template<typename T>
Array<T>::getT(..){...}

Array<int> array1;
```
```cpp
можно много параметров
template<typename Key, typename Value>
```
> шаблоны можно использовать и для методов  
  
**все шаблоны будут в .hpp файлах**

```cpp
void copy(T, T){...}

Array<int> a;
Array<string> b;
copy<int, string>(a, b);
//можно не писать <>, но потенциально может быть ошибка
```

> можно вместо `typename` использовать `size_t` например

Проблема - можем случайно перепутать типы
```cpp
template <typename T, template <typename> class Container> // class/typename
контра

Stack<int, Array> stack;
```

> если мы хотим определить конкретную специализацию

```cpp
template <>
Array<bool> {...}

template <size_t N>
struct Vector<float, N>{...}
```

## Ошибки

`std::expected<FILE*, int> fopen` - C-style  

### исключения
`throw <Объект исключения>` (без new)  

```cpp
try{
    ..
}
catch (DivideByZeroWxception& e){..}
```

```cpp
catch{
    ...
    throw;
}
кидаем ошибку дальше в другие блоки
```

