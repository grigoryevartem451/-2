# Лабораторная работа 2

# тема структуры

## Задача 1 - создать структуру с указателем на функцию

## постановка задачи

Создайте структуру, одно из полей которой является указателем на функцию. Вызовите эту функцию через имя переменной структуры и поле указателя на функцию.

# математическая модель

отсутствует

# код


```c
#include <stdio.h>

struct FunctionStruct {
    int value;
    void (*print_func)(int);
};

void print_number(int x) {
    printf("Значение: %d\n", x);
}

int main() {
    struct FunctionStruct my_struct;
    my_struct.value = 42;
    my_struct.print_func = print_number;
    
    my_struct.print_func(my_struct.value);
    
    return 0;
}
```
## результат 
<img width="217" height="34" alt="image" src="https://github.com/user-attachments/assets/1f65841b-b53b-442c-89cc-fde9729e3719" />




# индетификаторы
| Идентификатор | Тип | Назначение |
|---------------|-----|------------|
| `FunctionStruct` | struct | Структура с указателем на функцию |
| `value` | int | Целочисленное поле структуры |
| `print_func` | void (*)(int) | Указатель на функцию |
| `print_number` | void (int) | Функция для вывода числа |
| `x` | int | Параметр функции print_number |
| `my_struct` | FunctionStruct | Экземпляр структуры |
| `main` | int (void) | Главная функция программы |




# Задача 2 - структура для вектора в трёхмерном пространстве

## постановка задачи

Реализуйте структуру для вектора в 3D пространстве и добавьте следующие функции:

• Скалярное умножение векторов;

• Векторное произведение;

• Модуль вектора;

• Распечатка вектора.

В структуре также должно быть поле для хранения имени вектора.

## математическая модель

#### Структура вектора:
**V** = (x, y, z) ∈ ℝ³

#### Операции:

1. **Скалярное произведение:**
   **V₁** ⋅ **V₂** = x₁x₂ + y₁y₂ + z₁z₂

2. **Векторное произведение:**
   **V₁** × **V₂** = (y₁z₂ - z₁y₂, z₁x₂ - x₁z₂, x₁y₂ - y₁x₂)

3. **Модуль вектора:**
   |**V**| = √(x² + y² + z²)

4. **Печать вектора:**
   **V** = (x, y, z)

# код

```c
#include <stdio.h>
#include <math.h>

struct Vector3D {
    char name[20];
    double x;
    double y;
    double z;
};

double dot_product(struct Vector3D v1, struct Vector3D v2) {
    return v1.x * v2.x + v1.y * v2.y + v1.z * v2.z;
}

struct Vector3D cross_product(struct Vector3D v1, struct Vector3D v2) {
    struct Vector3D result;
    result.x = v1.y * v2.z - v1.z * v2.y;
    result.y = v1.z * v2.x - v1.x * v2.z;
    result.z = v1.x * v2.y - v1.y * v2.x;
    return result;
}

double magnitude(struct Vector3D v) {
    return sqrt(v.x * v.x + v.y * v.y + v.z * v.z);
}

void print_vector(struct Vector3D v) {
    printf("%s: (%.2f, %.2f, %.2f)\n", v.name, v.x, v.y, v.z);
}

int main() {
    struct Vector3D v1 = {"V1", 1.0, 2.0, 3.0};
    struct Vector3D v2 = {"V2", 4.0, 5.0, 6.0};
    
    print_vector(v1);
    print_vector(v2);
    
    printf("Скалярное произведение: %.2f\n", dot_product(v1, v2));
    
    struct Vector3D cross = cross_product(v1, v2);
    strcpy(cross.name, "V1xV2");
    printf("Векторное произведение: ");
    print_vector(cross);
    
    printf("Модуль V1: %.2f\n", magnitude(v1));
    printf("Модуль V2: %.2f\n", magnitude(v2));
    
    return 0;
}
```
## результат
<img width="1083" height="365" alt="image" src="https://github.com/user-attachments/assets/9edba4d1-edd3-411f-b022-535b94d4570b" />

# индетификаторы
| Идентификатор | Тип | Назначение |
|---------------|-----|------------|
| `Vector3D` | struct | Структура для 3D вектора |
| `name` | char[20] | Имя вектора |
| `x` | double | Координата X |
| `y` | double | Координата Y |
| `z` | double | Координата Z |
| `dot_product` | double | Функция скалярного умножения |
| `cross_product` | Vector3D | Функция векторного произведения |
| `magnitude` | double | Функция вычисления модуля |
| `print_vector` | void | Функция распечатки вектора |
| `v1` | Vector3D | Первый вектор |
| `v2` | Vector3D | Второй вектор |
| `result` | Vector3D | Результирующий вектор |
| `v` | Vector3D | Параметр функций |
| `main` | int | Главная функция |


# Задача 3 - вычисление комплексной экспоненты

## постановка задачи

<img width="720" height="106" alt="image" src="https://github.com/user-attachments/assets/032dcac8-3312-45c1-bb74-e8d9e7de6706" />

## математическая модель

#### Комплексное число:
**z** = a + bi ∈ ℂ, где:
- a ∈ ℝ - действительная часть
- b ∈ ℝ - мнимая часть
- i - мнимая единица (i² = -1)

#### Комплексная экспонента:
Ряд Тейлора для **e^z**:

**e^z** = Σ_{k=0}^n (z^k / k!) = 1 + z + z²/2! + z³/3! + ... + z^n/n!

#### Вычисление степеней комплексного числа:
**z^k** = (a + bi)^k

#### Вычисление через действительные и мнимые части:
Re(z^k) и Im(z^k) вычисляются рекуррентно через умножение комплексных чисел


# код

```c

#include <stdio.h>
#include <math.h>

struct Complex {
    double real;
    double imag;
};

struct Complex complex_exp(struct Complex z, int n) {
    struct Complex result = {1.0, 0.0};
    struct Complex term = {1.0, 0.0};
    struct Complex z_power = {1.0, 0.0};
    double factorial = 1.0;
    
    for (int i = 1; i <= n; i++) {
        factorial *= i;
        
        struct Complex temp;
        temp.real = z_power.real * z.real - z_power.imag * z.imag;
        temp.imag = z_power.real * z.imag + z_power.imag * z.real;
        z_power = temp;
        
        term.real = z_power.real / factorial;
        term.imag = z_power.imag / factorial;
        
        result.real += term.real;
        result.imag += term.imag;
    }
    
    return result;
}

int main() {
    struct Complex z = {1.0, 1.0};
    int terms = 10;
    
    struct Complex exp_z = complex_exp(z, terms);
    
    printf("e^(%.1f + %.1fi) = %.6f + %.6fi\n", 
           z.real, z.imag, exp_z.real, exp_z.imag);
    
    return 0;
}
```

## результат
<img width="395" height="53" alt="image" src="https://github.com/user-attachments/assets/23e7f492-cce8-45c3-bb12-71e8b257c662" />

## индетификаторы
| Идентификатор | Тип | Назначение |
|---------------|-----|------------|
| `Complex` | struct | Структура для комплексного числа |
| `real` | double | Действительная часть числа |
| `imag` | double | Мнимая часть числа |
| `complex_exp` | Complex | Функция вычисления комплексной экспоненты |
| `z` | Complex | Комплексное число |
| `n` | int | Количество членов ряда |
| `result` | Complex | Результат вычисления |
| `term` | Complex | Текущий член ряда |
| `z_power` | Complex | Текущая степень z |
| `factorial` | double | Значение факториала |
| `i` | int | Счетчик цикла |
| `temp` | Complex | Временная переменная |
| `main` | int | Главная функция программы |
| `terms` | int | Количество членов ряда |
| `exp_z` | Complex | Результат экспоненты |


# Задача 4 - Структура с битовыми полями для даты

## постановка задачи

Используя битовые поля в структуре C, создайте структуру для хранения даты (например, даты рождения).

## математическая модель
#### Битовое представление даты:

**Структура хранения:**
- **День**: 5 бит → диапазон: 0-31 (2⁵ = 32 значения)
- **Месяц**: 4 бита → диапазон: 0-15 (2⁴ = 16 значений)
- **Год**: 12 бит → диапазон: 0-4095 (2¹² = 4096 значений)

#### Формальная модель:
**Date** = {day ∈ [1,31], month ∈ [1,12], year ∈ [0,4095]}

#### Битовая маска:
Общий размер: 5 + 4 + 12 = 21 бит ≈ 3 байта

# код

```c
#include <stdio.h>

struct Date {
    unsigned int day : 5;
    unsigned int month : 4;
    unsigned int year : 12;
};

int main() {
    struct Date birthday = {15, 8, 1990};
    
    printf("Дата рождения: %02u.%02u.%u\n", 
           birthday.day, birthday.month, birthday.year);
    
    printf("Размер структуры: %zu байт\n", sizeof(struct Date));
    
    return 0;
}
```
## резултьтат

<img width="326" height="59" alt="image" src="https://github.com/user-attachments/assets/e430ca73-98ae-4ff8-8fe8-ed3a7b86de73" />

# индетификаторы
| Идентификатор | Тип | Назначение |
|---------------|-----|------------|
| `Date` | struct | Структура для хранения даты с битовыми полями |
| `day` | unsigned int : 5 | Поле для дня месяца (5 бит) |
| `month` | unsigned int : 4 | Поле для месяца (4 бита) |
| `year` | unsigned int : 12 | Поле для года (12 бит) |
| `birthday` | Date | Переменная типа Date |
| `main` | int | Главная функция программы |



# Задача 5 - реализация двусвязного списка

## постановка задачи

Реализуйте структуру и функции для создания и наполнения двусвязного списка, а также функции для его обхода и
распечатки:

• Прямой обход списка с выводом значений;

• Обратный обход списка с выводом значений.

## математическая модель

#### Двусвязный список:
**List** = (head, tail) где:
- head ∈ Node ∪ {NULL}
- tail ∈ Node ∪ {NULL}

#### Узел списка:
**Node** = (data, next, prev) где:
- data ∈ T (произвольный тип)
- next ∈ Node ∪ {NULL}
- prev ∈ Node ∪ {NULL}

#### Инварианты:
1. ∀ node ∈ List: node.next.prev = node (кроме head)
2. ∀ node ∈ List: node.prev.next = node (кроме tail)
3. head.prev = NULL
4. tail.next = NULL

#### Операции:
- **append(L, x)**: добавление элемента x в конец списка L

- **traverse_forward(L)**: обход от head к tail
  
- **traverse_backward(L)**: обход от tail к head


# код

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Node {
    void *data;
    struct Node *next;
    struct Node *prev;
};

struct List {
    struct Node *head;
    struct Node *tail;
};

struct List* create_list() {
    struct List *list = (struct List*)malloc(sizeof(struct List));
    list->head = NULL;
    list->tail = NULL;
    return list;
}

void append(struct List *list, void *data, size_t data_size) {
    struct Node *new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = malloc(data_size);
    memcpy(new_node->data, data, data_size);
    new_node->next = NULL;
    new_node->prev = list->tail;
    
    if (list->tail != NULL) {
        list->tail->next = new_node;
    }
    list->tail = new_node;
    
    if (list->head == NULL) {
        list->head = new_node;
    }
}

void print_forward(struct List *list, void (*print_func)(void*)) {
    struct Node *current = list->head;
    printf("Прямой обход: ");
    while (current != NULL) {
        print_func(current->data);
        current = current->next;
    }
    printf("\n");
}

void print_backward(struct List *list, void (*print_func)(void*)) {
    struct Node *current = list->tail;
    printf("Обратный обход: ");
    while (current != NULL) {
        print_func(current->data);
        current = current->prev;
    }
    printf("\n");
}

void print_int(void *data) {
    printf("%d ", *(int*)data);
}

void print_string(void *data) {
    printf("%s ", (char*)data);
}

int main() {
    struct List *int_list = create_list();
    int a = 10, b = 20, c = 30;
    append(int_list, &a, sizeof(int));
    append(int_list, &b, sizeof(int));
    append(int_list, &c, sizeof(int));
    
    print_forward(int_list, print_int);
    print_backward(int_list, print_int);
    
    struct List *str_list = create_list();
    char *s1 = "Hello", *s2 = "World", *s3 = "!";
    append(str_list, s1, strlen(s1) + 1);
    append(str_list, s2, strlen(s2) + 1);
    append(str_list, s3, strlen(s3) + 1);
    
    print_forward(str_list, print_string);
    print_backward(str_list, print_string);
    
    return 0;
}
```

## результат

<img width="336" height="91" alt="image" src="https://github.com/user-attachments/assets/117fde6e-4a30-4592-b854-0926108915af" />


# индетификаторы

| Идентификатор | Тип | Назначение |
|---------------|-----|------------|
| `Node` | struct | Структура узла двусвязного списка |
| `data` | void* | Указатель на произвольные данные |
| `next` | struct Node* | Указатель на следующий узел |
| `prev` | struct Node* | Указатель на предыдущий узел |
| `List` | struct | Структура двусвязного списка |
| `head` | struct Node* | Указатель на первый узел списка |
| `tail` | struct Node* | Указатель на последний узел списка |
| `create_list` | struct List* | Функция создания нового списка |
| `append` | void | Функция добавления элемента в список |
| `print_forward` | void | Функция прямого обхода списка |
| `print_backward` | void | Функция обратного обхода списка |
| `print_int` | void | Функция печати целого числа |
| `print_string` | void | Функция печати строки |
| `int_list` | struct List* | Список целых чисел |
| `str_list` | struct List* | Список строк |


# Автор Григорьев Артём
группа ПОО
1 КУРС
