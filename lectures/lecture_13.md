# LECTURE 13

**iterator_traits** -  инфа о итераторах, в общем случае называются *type traits*(с одноименной библиотекой)

есть функции возвращающие *тип*, например `std::make_signed`

**SFINAE** - Substitution Failer Is Not An Error  
`statis long test(...)` - C-variadic, можно ваще чо угодно передать  

`enable_if` - удобное использование sfinae

## concepts

`concept Integral = std::is_integral_v<T>` - булевое выражение, основанное на sfinae и enable_if

```cpp
tamplate <typename t>
concept Comparable = requires (T a, T b){ a < b; }; //requires expression : true ot false

... requires(T a, T b){
    { a < b } -> (return type)
    { a < b } -> std::same_as<bool>;

requires Comparable<T> //requires clause, можно так же написать template <Comparable<T>>
T min(T a, T b)
    return (a < b) ? a : b;
}

requires requires (T x, T y) { x < y;} // чтобы не создавать концепт 
T min(..){..}
```
