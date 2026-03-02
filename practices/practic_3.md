# PRACTIC 3

класс в классе нужен только, если мы хотим подчеркнуть, что данный класс нужен только в контексте другого:
```cpp
class Timer{
    class Counter{
        some_method(Timer& timer);
    }
}
```
## enum
вне класса нет смысла реализовывать, только может быть в глобальном плане

```cpp
class Cat{
    enum class Color{
        w; b; c;
    }
}

cat = Cat()
if (cat.color == Cat::Color::w)..
```

## умные указатели
проблема: не помним на что указатель указывает ваще
```cpp
void foo(Matrix* m){
    m1 = m;
    m2 = m;
    delete m1;
    delete m2;
    //Error(
}
```
**teamplate** - vector<int>, vector<Matrix>  
### scoped ptr
```cpp
class scoped_ptr{
    Matrix* data;
    scoped_ptr(){data = new Matrix();}
    ~...(){delete data;}
    Matrix& operator*(){return *data;}
    Matrix& operator->(){...}
}
```
**auto_ptr** ВСЕ!
unique_ptr shared_ptr week_ptr
### unique_ptr
используется с std::move, который в совю очередь нужен для &&

```cpp
u = unique_ptr();
Vector = foo(std::move(u));
//тепреь указатель в Vector, по u уже нельзя!

//kk
unique_ptr(unipue_ptr other){
    data = other.data;
    other.data = nullptr;
}
```

### shared_ptr
хотим несколько значений по одному указателю
```cpp
class shared_ptr{
    private:
        class Storage{
        private:
            int cnt;
            Matrix *data;
        public:
            Storage(){cnt = 0; data = new Matrix();}
            ~..();
            op++;
            op--;
            //kk =delete 😈(ну или просто не писать)
            getCounter();
            getData();
        }
        Storage *s;
    public:
        *;
        ->;
        shared_ptr(shared_ptr& other){
            s = other.s;
            s.incr();
        }
        op= ананлогично
        ~..(){
            s.decr();
            if (getCounter == 0) delete:s.data;
        }
}
```

### конструтор
```cpp
unique_ptr(M * p);
M* p = new ...;
u = unique(p);
// укзаатель кот не входит в счетчик
unique(new M(5)) ?
foo(unique.., ...) contra
может быть висячий указатель
надо
make_unique<M[]>(5)😈 выделили память под 5 матриц 

если
s1 = shared(p)
s2 = shared(p)
плохо! у анс не уыеличивается счетчик, надо через make_
```