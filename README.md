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
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
#51
```

```
