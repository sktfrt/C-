# LECTURE 9

## iterators

для первого элемента за массивом тоже работает арифметика указателей

c end очень удобно работать

## функциональные объекты

класс, у которого перегружен оператор `operator()`  
```cpp
struct add{
    int operator()(int x, int y) const {return x + b;}
};
add func;
int x = func(3, 4);
```

это лучеш чем функции, так как мы имеем доступ к другим данным внутри класса  
есть типы объектов:
*bool называют предикатами*
1) с одним аргументом - унарный
2) с двумя - бинарный 
   
## стандартные алгоритмы (\<algorithm> + \<numeric>)

*мини - алгоритмы*
* `swap` 😈
* `iter_swap(It p, It q)` - поменять то, на что указывают итераторы /история/
* max / min 😈
* `clamp(a, max, min)` - ограничить значение
  
*компараторы*
компараторы можно передать в min/max третьим аргументом  

### *немодифицирующие алгоритмы*
* `count` 😈
* `count_if(begin, end, pred)` - сколько раз встречаются объекты, удовлетоворяющие предикату
* `all_of(begin, end, pred)` - правда лм что все предикат, ~all() in py
* `any_of` ~ any
* `none_of` ~ !all()

*алгоритмы сравнения*  
* equal(It1 begin, It1 end, It2 beegin2) - совпадают ли пос-ти
* `equal(begin, end, begin2, end2)` 
* `pair<> mismatch`
* `lexicographical_compare` - лексикографическое сравнение

*алгоритмы поиска*   
* `find` 😈
* `find_if` - с предикатом
* `min_element` - 😈
* `pair<It, It> minmax_element` 😈
  
### *модифицирующие алгоритмы*
* `fill` - заполнить копиями
* `generate(begin, end, gen)` - заполниьт результатами gen
* `iota` - в \<numeric>, от 1 до дофига
* `copy`, не надо помнить про `memcpy`
* `copy_if` - с предикатором
* `reverse` 😈
* `rotate` - циклический сдвиг
* `transform` - copy с некой операцией

*алгоритмы сортировки*  
* `sort` 😈 гарантия на nlogn
* `stable_sort` - устойчивая
* `partial_sort(begin, middle, end)` - сдвинуть младшие mid - beg эл-ов в начало
* + все версии со своим компаратором
* `lower_bound` - вернет начало куска на копии (while x < our)
* `upper_bound` - вернет конец (while x <= our)

`typename It::value_int` - мамой клянусь, что это не статическая переменная, а поле  

*iterators traits*  
`iterator_traits` - хранит все данные итератора, специализирован для указателей

`auto` - наше все

*алгоритмы на итераторах*  
* `next` - след ит, не меняет it
* `advance`
* `distance`
  
*категории итераторов*  
категории определяют, какие операции ит может выполнять
* `forward` 
* `bidiractional`
* `random access`
добавляем тэг в traits  
*tag dispatching*  

```cpp
It next(It it, int n){
    using traits = std::operator_traits<It>;
    return next(it, n, typename trairs::iterator_category{});
}
```

*прикол*  
```cpp
while (n --> 0){} ~ for (; n > 0; --n)
//  n-->0 == (n--) > 0
```
```cpp
while (n---->)😈
```