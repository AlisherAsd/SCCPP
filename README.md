# SCCPP
Simple Code CPP 
--------------
#46
```
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
