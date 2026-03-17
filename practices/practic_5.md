# PRACTIC 5
```cpp
Base* b_ptr = new Base();
c_ptr = (Child*)b_ptr
если new Child то вообще пофиг все ок
если так то все скомпилируется, но если мы обратимся к несуществующему полю/методу то все сломается
```

## **cast ы**
к `void*` все можно!
1) statisc-cast ~ ()
2) dynamic-cast
3) const_cast
4) reinterpret_cast
   
### *static-cast*
* к `void*` 
* `наследник <-> родитель`
* `базовые преобразования`
  
**это все наша отвественность**
```cpp
c_ptr = static_cast<Child*>(b_ptr)
c_ptr = static_cast<Child&>(b_ptr)
```
### *dynamic_cast*
```cpp
Child* c_ptr = dynamic_cast<...>(b_ptr)
if (c_ptr) {...} //преобразование прошло успешно
```
не увлекаемся  
### *const_cast*
```cpp
int x = 8;
const int& y = x;
ура!

а обратно?
int& z = y; //error
int& z = const_cast<int>(y)
ура!
но это фигня( зачем хз
```
### *reinterpret_cast*
тоже фигня  
любая память в любую память  

## подробнее про приведение
`Base -> Child` - ошибка компиляции  
`Child -> Base` - обрезка данных до нужного типа(слайсинг), полиморфизм не будет работать  
```cpp
Child c();
b = c; //нет полиморфизма + все поля из ребенка будет потерты
```

## операторы ввода и вывода (лаба)
> существует istream(cin) и ostream(cout, cerr, clog) - ввод и вывод(любой)  
istream  | ostream  
ifstream | ofstream  
---sstream---

```cpp
istream& operator>>(istream& in, Matrix& m);
ostream& operator<<(ostream& out, const Matrix& m);
```
`const` нет, так как мы можем *поменять поток*  

## **прочитать cppreference рекомендуется**

***fstream***
```cpp
istream& getline(instream, std::string)
```
`>>` пропускает все табы, пробелы, переводы строки и останавливается *перед* пробелом
`cin >> x >> y;` - корректно  

`getline` же считает *все*  

но есть `ingore()/std::ws`, который приказывает игнорировать пробелы

**что такое wchar?** :
- занимает 2 или 4 байта
- это расширенный список символов(юникоды, ютфы и тд)
  
`istream` подразумевает собой cin  
`ifstream` это для файлов  

рассмотрим `[oi]fstream`
```cpp
//text.txt

ifstream in;
in.open("text.txt");

OR

ifstream in("text.txt")
```
```cpp
ifstream in("text.txt") //на чтение
ofstream out("text.txt") // на запись
ifstream in("text.txt", std::ios::binary) //бинарное
ofstream out("text.txt", std::ios::app) //в конец
ifstream in("text.txt", std::ios::trunc) //открыть на чтение, все удалить, для of выполняется автоматически
ofstream out("text.txt", std::ios::app | std::ios::binary | ) //перечисление флагов 
```

```cpp
проверка на открытие
if (in) //OK
if (in.is_open())
...
in.close(); // теоритически не надо, но лучше писать
in.open("text2.txt")
```

`write`, `read`  
`tellg()`, `tellp()` - найти позицию  
`settg()`, `seekp()` - сдвинуть позицию  

### обработка ошибок
`out.rgstate()` - маска, хранящая состояние потока  
включает в себя методы:
- fail() - мягкая ошибка
- good() - все хорошо
- bad() - пизда тварица(обычно от нас не зависит)
- eof() - конец файла  

отвечают на вопрос - true/false  
`if(out) ~ fail||bad`  
по хорошему после каждой записи надо проверять `if(!out)`  
после ошибки флаги нужно вернуть в исходное состояние - `.clear()`, при завершении программы само делается  
```cpp
while (out << x)
    if (out.fail() ~ !out) out.clear()
```

**перегрузка операторов**
`>>` можно использовать для базовых типов внутри переопределение  

**friend** (почитать)
```cpp
class Matrix{
    private:
    int x, y;
    public:
    ofstream .. <<(out, const Matrix& m)
    friend(ofs...<<(..)) разрешает использовать приватные поля матрицы
}
можно делать `friend class M;`, а можно `friend M` и тут хороший вопрос когда что можно