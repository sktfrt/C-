# LECTURE 12

## потоки
**race/data condition**

**mutex**
```cpp
mutex.lock();
++x;
mutex.unlock();
// один поток
```

`std::lock_guard` - lock() в констурторе, unlock() в деструкторе

`std::unique_lock()` - как гард но пизже 

*deadlock* - 💀  
`std::lock(mutex1, mutex2, ....)` - deadlock avoidance  
`std::scoped_lock()` - как lock но пизже

`std::recursive_mutex`  обычно не надо

`std::atomic` - делает тип атомарным
```cpp
std::atomic<int> count = 0;

for (int i = 0; i < 1000; ++i)
    count.fetch_add(1);
```

`std::atomic`:
1) load() 
2) store()
3) exchange()
4) compare_exchange_weak/strong(value) - CAS


`spinlock` - реализация мютексов через атомик

`remove_cv`, `cv_qualified`

`volatile` - лучше не использовать...

## регулярки
`std::regex` - 😈

```cpp
std::regex num("(\d)+");
std::smatch match;
std::regex_search("1234", match, num);
```

## compile time
`static_assert` - assert в compile-time

`constexpr` - переменные или функции могут быть вычеслены в compile-time
`consteval` - фукнция всегда вычисляется в ct
`cosntinit` - переменаая инициализируетяс в ct

## variadic templates
```cpp
template <typename ... Args>
void print(Args ... args);

sizeof...(args);
```

**fold expressions** - `(args + ...)` = `arg0 + (arg1 + (...))`
```cpp
void print(args ...){
    (std::cout << args, ...); // ОПЕРАТОР ЗАПЯТАЯ!!!!!!!!!!!!!!!!
}
```
