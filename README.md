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

```
