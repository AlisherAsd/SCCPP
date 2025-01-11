# SCCPP
### Simple Code CPP
##### Записи при подготовке к экзамену ПМИ курса simple code по С++. 



-----------------------
# База с++ (указатели, ссылки, стринги, память)
-----------------------



#46
```
    // Несколько указателей могут ссылаться на адрес одной переменной
    int a = 5;
    int *pa = &a;
    int *pa2 = &a;
    *pa = 2; // *pa / *pa2 / a = 2
```

#47
```
    int size = 5;
    int arr[size] = {1, 2, 3, 4, 5};
    for (int i = 0; i < size; i++) cout << arr[i];
    int *pArr = arr;
    for (int i = 0; i < size; i++) cout << pArr[i];
    for (int i = 0; i < size; i++) cout << *(pArr + i);
```
#48
```
void foo(int *a) {
    (*a)++;
}
    int a = 5;
    foo(&a);
```
#49
```
void foo(int *a, int *b) {
    int tmp = *a;
    *a = *b; 
    *b = tmp;
}
    int a = 5, b = 1;
    foo(&a, &b);
```
#50
```
    int a = 5;
    int *pa = &a; // указатель
    int &aRef = *pa;
    int *ppa = &aRef;
    // и ссылка и указатель хранят адрес переменной, но у ссылки нет * и арифметики
    // int *ppt = nullptr; // ok
    // int &ppt; // ne ok
    *ppa = 12;
```
#51/52
```
template<typename T>
void foo(T &a, T &b) {
    T tmp = a;
    a = b;
    b = tmp;
}
    int a = 5;
    int b = 2;
    foo(a, b);
```
#53/54
```
int *pa = new int;
    *pa = 5;
    delete pa;
    pa = nullptr;
```
#55
```
    int size = 10;
    int *arr = new int[size];
    delete [] arr;
    arr = nullptr;
```
#56
```
    int rows = 5;
    int cols = 5;
    int **arr = new int*[rows];
    for (int i = 0; i < rows; i++) arr[i] = new int[cols];
    for (int i = 0; i < rows; i++) delete [] arr[i];
    delete [] arr;  
```
#59
```
void push_back(int *&arr, int &size, const int value) {
    int *newarr = new int[size + 1];
    for (int i = 0; i < size; i++) newarr[i] = arr[i];
    newarr[size] = value;
    arr = newarr;
}
    int size = 2;
    int *arr = new int[size];
    arr[0] = 2;
    arr[1] = 5;
    push_back(arr, size, 10);

```
#60/61/62
```
    string s = "Hello World!"; // массив чаров
    char s3 [] = "Hello World";
    const char *s4 = "Hello world";
    double a = 33.3; 
    char s2 = (char)a; // явное преобразование
```
#63
```
int strlen(const char *str) {
    int count = 0;
    while (true)
    {
        if (str[count] == '\0') break;
        else {
            count++;
        }
    }
    return count;
}
    cout << strlen(s4);
```
#64
```
    string s = "Hello ";
    string s2 = "World";
    string result = strcat_s(s, s2);
    result = s + s2;
```
#65
```
string foo() {
    return "foo(){}";
}

void ShowInfo(string (*foo)()) { // Указатель на функцию
    cout << foo();
}
    ShowInfo(foo());

```
#66
```
#define PI 3.14 // макрос
#define tab "/t"
```
#67
```
#define FOO(x, y)((x) + (y))
FOO(3, 4);
```
#68
```
#define DEBUG

#ifdef DEBUG
    cout <<"DEBUG";
#else
    cout <<"NOT DEBUG";
#endif
```
#69
```
    (5 > 2) ? (cout << "True") : (cout << "False");
    (5 > 2) ? (cout << "True") : (5 > 3) ? (cout << "True") : (cout << "False");
```




-----------------------
# ООП
-----------------------




#72
```
//Инкапсуляция в программировании — это принцип, согласно которому внутреннее устройство сущностей нужно объединять в специальной «оболочке» и скрывать от вмешательств извне.
//Полиморфизм (polymorphism) — это понятие из объектно-ориентированного программирования, которое позволяет разным сущностям выполнять одни и те же действия.
//Наследование в объектно-ориентированном программировании — это концепция, согласно которой одни классы, называемые родительскими, могут лежать в основе других — дочерних.
```
#73/74/75/76/77/78/79/80
```
class Point
{
private:
    int x;
    int y;
public:
    Point() {
        x = 0;
        y = 0;
    }
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    {
    ~Point() {
        cout << "Destructor" << endl;
    }
    int getX() {
        return x;
    }
    void setX(int x) {
        this.x = x;
    }
    void print() {
        cout << "x: " << x << endl;
        cout << "y: " << y << endl;
    }

}
```
#81
```
// this это константный указатель на адрес памяти объекта
this->x = x;
```
#82
```
// конструктор копирования
class Point {
    Point(const Point &point) { // по ссылке мы получаем доступ к объекту 
        point.x = x;
        point.y = y;
    }
}
```
#83
```
// перегрузка опереторов
// если мы производим действия над самим объектом, нужно иползовать MyClass & operator P() { return *this; }
// если использовать = по дефолту, 2 объекта будут ссылаться на один адрес, то влечет за собой ошибки при  delete
Point& operator = (const Point &point) {
    if (this->data != nullptr) { // очищаем память
        delete data;
    }
    this->data = point.data; // присваиваем новое значение
    return this;
}
```
#84
```
bool operator == (const Point &point) {
    if (this->data == point.data) return true;
    else return false;
}
bool operator != (const Point &point) {
    if (this->data != point.data) return true;
    else return false;
}

```
#85
```
// Point res = a + b; 
Point operator + (const Point & point) { 
    Point tmp; // res
    tmp.x = this->x + point.x; // this - a
    tmp.y = this->y + point.y; // point - b
    return tmp; // return res 
}
```
#86
```
Point & operator ++ () { // ++point
    this->x += 1;
    this->y += 1;
    return *this;
}
Point & operator ++ (int value) { // point++
    this->x += 1;
    this->y += 1;
    return *this;
}
```
#87
```
 int & operator [](int index) {
    return arr[index];
}
```
#88
```
class Point2;
class Point {
    friend void foo(Point &p, Point2 &p2);
}
class Point2 {
    friend void foo(Point &p, Point2 &p2);
}

void foo(Point &p, Point2 &p2) { // foo имеет доступ к обоим класса
    p.x = 1;
    p2.x = 1;
}
```
#89
```
class Point2;
class Point {
    void getPoint2(Point2 &p2) { cout << p2.x << endl }
}
class Point2 {
    friend void Point::getPoint2(Point2 &p2); // Метод из класса point имеет доступ к классу point2
}
```
#90
```
class Point2;
class Point {
    void getPoint2(Point2 &p2) { cout << p2.x << endl }
    void getPoint2_2(Point2 &p2) { cout << p2.x * 2 << endl }
    void getPoint2_2_3(Point2 &p2) { cout << p2.x * 3 << endl }
}
class Point2 {
    friend Point; // Все методы из класса Point будут иметь доступ к полям Point2
}

```
#92-94
```
class Point {
private:
    int data;
    static int count; // инициализация за классом
    static inline int countInline = 0; // инициализация при объявлении
public:
    Point() {
        data = 0;
        count++;
        countInline++;
    }
    void setData(int data) {
        this.data = data;
    }
    // В статических методах нельзя работать с нестатическими полями по this
    static int GetCount() {
        return count;
    }
     static int GetCountInline() {
        return countInline;
    }
    // Но можно работать с полями передоваемого объекта
    static void setDataCount(Point &p) {
        p.setData(count);
    }
}

int Point::count = 0;

void Main() {
    // Обращаться к статическим поляи можно как через объект, так и через класс
    Point a;
    Point::getCount();
    a.getCount();
}

```
#98-99
```
class A
{
public:
    string message = "public"; // доступен всем
private:
    string message2 = "private"; // приватен везде кроме своега класса
protected:
    string message3 = "protected";  // наследуется, но приватен из вне
}

class B : public A;    // public    /   private   / protected
class C : private A;   // private   /   private   / private
class D : protected A; // protected /   private   / protected

```
#100
```
// Порядок вызов конструкторов при наследовании, перед конструктром дочернего класса вызывается контрукор базоваго класса
// Для деструктора, соответсвенно, все наоборот
struct A {
    A() { cout << "Constructor A" << endl; } // Constructor A
    ~A() { cout << "Destructor A" << endl; } // Destructor A
};
struct B : public A {
    B() { cout << "Constructor B" << endl; } // Constructor A, Constructor B
    ~B() { cout << "Destructor B" << endl; } // Destructor B, Destructor A
};
struct C : public B {
    C() { cout << "Constructor C" << endl; } // Constructor A, Constructor B, Constructor C
    ~C() { cout << "Destructor C" << endl; } // Destructor C, Destructor B, Destructor A
};
```
#101-104
```
//  Абстрактный класс определяет интерфейс для переопределения производными классами.
// virtual метод нцжен для того чтобы методы дочернего класса вызываемые по указатнлю базового корректно отрабатывали
class Weapon
{
public:
    virtual void Shoot() = 0;
};
class Gun : Weapon
{
public:
    void Shoot() ovveride {
        cout << "BANG" << endl;
    }
};
class SubMachineGun : public Gun
{
public:
    void Shoot() override { // override нужен для того чтобы компилятор контролировал, корректно ли переопределен метод
        cout << "BANG BANG BANG" << endl;
    }
};

int main() {
    Gun n;
    SubMachineGun s;
    Weapon *pgun = &n;
    Weapon *pgun2 = &s; 
    pgun->Shoot(); // bang 
    pgun2->Shoot(); // bang bang bang | если бы был не виртуальный метод, вызвался бы метод типа указателя, тоесть bang
    return 0;
}
```
#106
```
// Виртуальный деструктор нужен по той же причине что и мктод, если не сделать деструктор виртуальным, при удалениии указателя бозрвого класса, будет удаляться только он, и небудет осовбождаться память для дочерний классов
```
#107
```
class Human {
    int age;
    string name;
    int weight;
    Human(string name) {
        this->name = name;
    }
    Human(string name, int age) : Human(name) {
        this->age = age;
    }
    Human(string name, int age, int weight) : Human(name, age) {
        this->weight = weight;
    }
}
```
#108
```
// Чтобы вызвать виртуаьный метод базавого класса надо использовать
::BasClass::Function(); // BasClass - бозовый класс
```
#109-111
```
// При множественном наследовании контрукторы и дестркторы вызываются также, только в порядке наседования
// Конструторы A B C
// Деструторы C B A
class MarginClasses : public A, public B, public C {} 
```
#112
```
class A {
public:
    void AB() { cout << "A" << endl; };
};
class B {
public:
    void AB() { cout << "B" << endl; };
};
class C : public A, public B {};

int main() {    
    C a;
    // a.AB(); // компилятор не знает к какому методы обратиться
    B *b = &a;
    b->AB(); // B
    a.A::AB(); // A
    return 0;   
}
```
#113
```
Таким образом, абстрактный класс создаёт иерархию наследования, а интерфейсный класс требует, чтобы класс, реализующий интерфейс, содержал реализации всех методов, определённых этим интерфейсом. 
```
#114
```
// Проблема ромба
class Base { 
public: 
    void display() { 
        std::cout << "Base class" << std::endl; 
    } 
}; 
class Derived1 : virtual public Base { 
}; 
class Derived2 : virtual public Base { 
}; 
class Diamond : public Derived1, public Derived2 { 
};

int main() { 
    Diamond diamond; 
    diamond.display();  // Теперь нет неоднозначности, вызывается один экземпляр Base
    diamond.Derived1::display(); // Либо вызывать опр метод
    return 0; 
}

```
#124
```
// enum

enum PCState {
    OOF,
    ON,
    SLEEP
}

class PC {
public:
    PCState getState() { return state; }
    void getState(PCState pcstate) { state = pcstate; }
private:
    PCState state;
};

int main() { 
    PC pc;
    pc.getState(PCState::OOF);
  
    return 0; 
}
```
#125
```
// namespace - пространство имен
// Для того чтобы различать функции итд с одним названием
// в std все дефолтные c++ функции
namespace firtsNS {
    void foo() { cout << "FirstNS"; }
}
namespace secondNS {
    void foo() { cout << "secondNS"; }
}

int main() { 
    firtsNS::foo();
    return 0; 
}
```


------
# Потоки ввода вывода
-----

#115
```
#include<fstream>
// Запись в файл ofstream
int main() { 
    ofstream fout;
    fout.open("file.txt", ofstream::app); // Параметр app - append не обязателен, без него каждая запись убдет стирать прошлые данные
    if (!fout.is_open()) cout << "Err" << endl;
    else {
        fout << "Hello world"; // В текущем каталоге будеи открыт файл либо создан если его нету
    }
    fout.close();
    return 0; 
}
```
#116
```
#include<fstream>

using namespace std;
// Чтение из файла ifstream
int main() { 
    ifstream fin;
    fin.open("file.txt");
    if (!fin.is_open()) cout << "Err" << endl;
    else {
        char ch;
        string s;
        // while (fin.get(ch)) // Поэлементно проходимся по файлу
        // {
        //     cout << ch;
        // }
        while (!fin.eof()) 
        {
            s = "";
            // fin >> s; // Чтени из файла в перменную через пробел
            getline(fin, s); //  Чтени из файла в перменную через строку
            cout << s << endl;
        }
    }
    fin.close();
    return 0; 
}
```
#117
```
#include<iostream>
#include<fstream>

using namespace std;

class Point
{
public:
    int x;
    int y;
    int z;
    Point() { x = y = z = 0;}
    Point(int x, int y, int z) {
        this->x = x;
        this->y = y;
        this->z = z;
    }
    void print() {
        cout << "x: " << x << "\n" << "y: " << y << "\n" << "z: " << z << "\n";
    }

};

int main() { 

    Point point(1, 2, 1);
    // Запись объекта в файл
    ofstream fout;
    fout.open("file.txt");
    if (!fout.is_open()) {
        cout << "Err" << endl;
    } else { 
        fout.write((char*)&point, sizeof(Point)); // запись объекта через преобразование его в чар
    }
    fout.close();

    // Чтение объекта из файла
    ifstream fin;
    fin.open("file.txt");
    if (!fin.is_open()) {
        cout << "Err" << endl;
    } else { 
        Point tmp;
        while (fin.read((char*)&tmp, sizeof(Point))) { // чтение объекта через преобразование его в чар
            tmp.print();
        }
    }
    fout.close();
    return 0; 
}
```
#118
```
int main() {
    fstream fs; // fs  в отличии от if и of можно использовать и для того и для другого
    fs.open("file.txt", fstream::in | fstream::out | fstream::app); // in - чтение, out - запись, app - дописывать
    if (!fs.is_open()) {
        cout << "Err" << endl;
    } else {
        // fs << "Hello world!\n"; // запись в файл
        string s;
        while (!fs.eof()) // пока не конец - endof
        {
            s = ""; 
            fs >> s; // читаем поток в s
            cout << s;
        }
        
    }
    fs.close();
    return 0; 
}
```
#119 
```
// Прегрузка ostream / istream
#include<iostream>
#include<fstream>

using namespace std;

class Point
{
public:
    int x;
    int y;
    int z;
    Point() { x = y = z = 0;}
};

ostream& operator<<(ostream& os, const Point &point) {
    os << point.x << " " << point.y << " " << point.z << "\n";  
    return os;
}

istream& operator>>(istream& is, Point &point) {
    is >> point.x >> point.y >> point.z;  
    return is;
}

int main() { 
    Point p;
    cin >> p;
    cout << p;
    return 0; 
}
```
---
# Обработка исключений
---

#120-122
```
void test(int val) {
    if (val <= 0) throw runtime_error("Val <= 0"); // передается стринг в catch
    cout << val;
}

void test2(int val) {
    if (val <= 0) throw runtime_error("Val <= 0"); // передается стринг в catch потому что базовый классс ex
    cout << val;
}

int main() { 
    
    try
    {
        test(-1);
        test2(-1);
    }
    catch(const char* ex)
    {
        cout << ex;
    }
    catch(const exception& e) // приимущество такого метода в том, что он может поймать любое исключение
    {
        cout << e.what() << '\n';
    }
    catch(...) { // ловит все подряд, но что именно вызвалоошибку, непонятно
        cout << "Что-то пошло не так.";
    }
    return 0; 
}
```
#123
```
// Разработка собсвенного класса exception
// стандртныц класс имеет только метод what

class MyException : public runtime_error { // наследуемся от runtime_error чтобы иметь метод what()

private:
    int dataState;

public:
    MyException(const char* messag, int val) : runtime_error(messag) { // расщиряем конструктор нашего класса добавляя runtime_error, и наш val
        dataState = val; // сохраняем val в dataState
    }
    int getDataState() const { // теперь помимо метода what () у нас есть метод getDataState()
        return this->dataState;
    }
};

void test(int val) {
    if (val <= 0) throw MyException("val <= 0", val); // используем наш класс MyException 
    cout << val;
}


int main() { 
    
    try
    {
        test(-1);
    }
    catch(const MyException& e) // наш класс имеет как метод what() так и getDataState()
    {
        cout << e.what()  << '\n';
        cout << e.getDataState() << '\n';
    }
    catch(const exception& e) // вызываем базовый класс потому что если его поставить первым он всегда будет пойман
    {
        cout << e.what()  << '\n';
    }
    return 0; 
}
```

-------
# Шаблоны классов ( Обощенные классы )
------
#127
```
template<typename T, typename T2>
class TeplateClass {
public:
    TeplateClass(T val, T2 val2) {
        value = val;
        value2 = val2;
    }
    void DataTypeSize() {
        cout << "Size " << sizeof(value) << " bytes" << endl;
        cout << "Size " << sizeof(value2) << " bytes" << endl;
    }
protected:
    T value;
    T2 value2;
};

template<typename T, typename T2>
class TypeInfo : public TeplateClass<T, T2> {
public:
    TypeInfo(T val, T val2) : TeplateClass<T, T2>(val, val2) {};
    void TypeName() {
        cout << "Name T: " << typeid(this->value).name() << endl;
        cout << "Name T2: " << typeid(this->value2).name()<< endl;
    }
};

int main() { 
    TeplateClass<int, double> a(5, 2.234234);
    a.DataTypeSize();
    TypeInfo<int, double> b(5, 2.234234);
    b.TypeName();
    return 0; 
}
```
#128
```
// специализация шаблона
template<typename T>
class SClass {
public:
    T value;
    SClass(T val) { value = val; }
    void print() { cout << value << endl; }
};

template<>
class SClass<char> {
public:
    void print(char value) { cout << value << endl; }
};


int main() { 
    SClass<int> a(4);
    SClass<char> b;
    b.print('a');
    return 0; 
}
```
---
# ааа
---
#129
```
// Структурв тоже самое что и классы, только в структуре все поля по умолчанию public, в классе private (по умолчанию)
// Также при наследовании, у struct - public, у класса private (по умолчанию)
```
#130
```
// Умные указатели

```
#
```
```
#
```
```
