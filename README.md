# SCCPP
Simple Code CPP 
--------------

** База с++ (указатели, ссылки, стринги, память)
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

** ООП
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
