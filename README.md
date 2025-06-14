# **19. Класс Array в C#: основные свойства и методы**

Класс `Array` - это базовый класс для всех массивов в .NET, предоставляющий статические методы и свойства для работы с массивами любого типа.

---

## **1. Основные свойства**

| Свойство            | Тип       | Описание                                                                 |
|---------------------|-----------|--------------------------------------------------------------------------|
| `Length`            | `int`     | Общее количество элементов во всех измерениях массива                    |
| `Rank`              | `int`     | Количество измерений массива (1 для одномерного, 2 для двумерного и т.д.)|
| `IsReadOnly`        | `bool`    | Возвращает `true`, если массив доступен только для чтения                |
| `IsFixedSize`       | `bool`    | Всегда `true` для массивов (они имеют фиксированный размер)              |
| `LongLength`        | `long`    | Длина массива как 64-битное целое (для очень больших массивов)           |

**Пример:**
```csharp
int[,] matrix = new int[3, 4];
Console.WriteLine(matrix.Length);  // 12 (3*4)
Console.WriteLine(matrix.Rank);    // 2 (двумерный)
```

---

## **2. Основные методы**

### **2.1. Создание массивов**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Array.CreateInstance(Type, int)` | Создает одномерный массив указанного типа и размера                   |
| `Array.CreateInstance(Type, int[])` | Создает многомерный массив                                         |

**Пример:**
```csharp
Array arr = Array.CreateInstance(typeof(int), 5);  // Массив из 5 int
```

### **2.2. Доступ к элементам**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `GetValue(index)`              | Возвращает значение элемента по индексу                                  |
| `SetValue(value, index)`       | Устанавливает значение элемента по индексу                               |

**Пример:**
```csharp
Array numbers = new int[] {1, 2, 3};
numbers.SetValue(10, 1);  // [1, 10, 3]
Console.WriteLine(numbers.GetValue(1));  // 10
```

### **2.3. Поиск элементов**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `IndexOf(Array, object)`       | Возвращает индекс первого вхождения элемента                            |
| `BinarySearch(Array, object)`  | Бинарный поиск в отсортированном массиве                                |
| `Find<T>(T[], Predicate<T>)`   | Возвращает первый элемент, удовлетворяющий условию                      |

**Пример:**
```csharp
int[] nums = {10, 20, 30};
int index = Array.IndexOf(nums, 20);  // 1
int pos = Array.BinarySearch(nums, 30);  // 2
int firstEven = Array.Find(nums, x => x % 2 == 0);  // 10
```

### **2.4. Сортировка и изменение порядка**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Sort(Array)`                  | Сортирует элементы массива                                              |
| `Reverse(Array)`               | Изменяет порядок элементов на обратный                                  |

**Пример:**
```csharp
int[] arr = {3, 1, 4};
Array.Sort(arr);  // [1, 3, 4]
Array.Reverse(arr);  // [4, 3, 1]
```

### **2.5. Копирование массивов**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Copy(Array, Array, int)`      | Копирует указанное количество элементов                                 |
| `ConstrainedCopy(...)`         | Гарантирует целостность данных при ошибке                               |

**Пример:**
```csharp
int[] src = {1, 2, 3};
int[] dest = new int[3];
Array.Copy(src, dest, src.Length);  // dest = [1, 2, 3]
```

### **2.6. Изменение размера**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Resize<T>(ref T[], int)`      | Изменяет размер одномерного массива                                     |

**Пример:**
```csharp
int[] numbers = {1, 2, 3};
Array.Resize(ref numbers, 5);  // [1, 2, 3, 0, 0]
```

### **2.7. Преобразование типов**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `ConvertAll<TInput,TOutput>`   | Преобразует массив одного типа в другой                                 |

**Пример:**
```csharp
string[] strArr = {"1", "2", "3"};
int[] intArr = Array.ConvertAll(strArr, int.Parse);  // [1, 2, 3]
```

### **2.8. Инициализация**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Clear(Array, index, length)`  | Устанавливает элементы в значения по умолчанию                          |
| `Fill<T>(T[], T)`             | Заполняет массив указанным значением (C# 8.0+)                          |

**Пример:**
```csharp
int[] arr = {1, 2, 3};
Array.Clear(arr, 0, arr.Length);  // [0, 0, 0]
Array.Fill(arr, 5);  // [5, 5, 5]
```

### **2.9. Проверки**
| Метод                          | Описание                                                                 |
|--------------------------------|--------------------------------------------------------------------------|
| `Exists<T>(T[], Predicate<T>)` | Проверяет, существует ли элемент, удовлетворяющий условию               |
| `TrueForAll<T>(...)`           | Проверяет, все ли элементы удовлетворяют условию                        |

**Пример:**
```csharp
int[] nums = {1, 2, 3};
bool hasEven = Array.Exists(nums, x => x % 2 == 0);  // true
bool allEven = Array.TrueForAll(nums, x => x % 2 == 0);  // false
```

---

## **3. Примеры использования**

### **3.1. Работа с многомерными массивами**
```csharp
int[,] matrix = new int[2, 3];
Console.WriteLine(matrix.GetLength(0));  // 2 (строки)
Console.WriteLine(matrix.GetLength(1));  // 3 (столбцы)
```

### **3.2. Сортировка и поиск**
```csharp
string[] names = {"Bob", "Alice", "Tom"};
Array.Sort(names);  // ["Alice", "Bob", "Tom"]
int index = Array.BinarySearch(names, "Bob");  // 1
```

### **3.3. Фильтрация**
```csharp
int[] numbers = {10, 25, 30, 45};
int[] evens = Array.FindAll(numbers, x => x % 2 == 0);  // [10, 30]
```

---

## **4. Сравнение с методами экземпляра**
Некоторые методы доступны как статические (`Array.Sort()`), так и через экземпляр:

| Статический метод       | Метод экземпляра          |
|-------------------------|--------------------------|
| `Array.Sort(arr)`       | `arr.Sort()` (не существует) |
| `Array.Reverse(arr)`    | `arr.Reverse()` (LINQ)   |
| `Array.IndexOf(arr, x)` | `Array.IndexOf(arr, x)`  |

**Важно:** Некоторые функциональности доступны только через статические методы класса `Array`.

---

## **5. Итоговая таблица наиболее полезных методов**

| Категория       | Важные методы                          | Пример использования                  |
|-----------------|----------------------------------------|---------------------------------------|
| **Создание**    | `CreateInstance`                       | `Array.CreateInstance(typeof(int), 5)`|
| **Доступ**      | `GetValue`, `SetValue`                 | `arr.SetValue(10, 0)`                 |
| **Поиск**       | `IndexOf`, `BinarySearch`, `Find`      | `Array.IndexOf(arr, "Alice")`         |
| **Сортировка**  | `Sort`, `Reverse`                      | `Array.Sort(names)`                   |
| **Копирование** | `Copy`, `ConstrainedCopy`              | `Array.Copy(src, dest, 3)`            |
| **Изменение**   | `Resize`, `Clear`, `Fill`              | `Array.Fill(arr, 0)`                  |
| **Проверки**    | `Exists`, `TrueForAll`                 | `Array.Exists(nums, x => x > 10)`     |
| **Преобразование** | `ConvertAll`                        | `Array.ConvertAll(strArr, int.Parse)` |


# **21. Методы и параметры методов в C#**  

Методы в C# — это блоки кода, которые выполняют определенную задачу. Они помогают структурировать программу, избегать дублирования кода и упрощают его поддержку.  

#### **1. Объявление метода**  
Метод состоит из:  
- **Модификатора доступа** (`public`, `private`, `protected`, `internal`)  
- **Возвращаемого типа** (`void`, `int`, `string`, etc.)  
- **Имени метода** (в стиле `PascalCase`)  
- **Параметров** (в скобках, через запятую)  
- **Тела метода** (в фигурных скобках `{}`)  

**Пример:**  
```csharp
public int Sum(int a, int b) 
{
    return a + b;
}
```  

#### **2. Параметры методов**  
Параметры — это входные данные, которые передаются в метод.  

##### **2.1. Обычные параметры (по значению)**  
- Значение копируется в метод.  
- Изменения внутри метода не влияют на исходную переменную.  

```csharp
void ModifyValue(int x) 
{
    x = 10; // Не изменит переданную переменную
}

int num = 5;
ModifyValue(num);
Console.WriteLine(num); // 5
```  

##### **2.2. Параметры по ссылке (`ref`)**  
- Метод работает с оригинальной переменной.  
- Изменения внутри метода сохраняются.  

```csharp
void ModifyRef(ref int x) 
{
    x = 10;
}

int num = 5;
ModifyRef(ref num);
Console.WriteLine(num); // 10
```  

##### **2.3. Выходные параметры (`out`)**  
- Аналогично `ref`, но переменная не обязана быть инициализирована.  
- Метод **обязан** присвоить значение `out`-параметру.  

```csharp
bool TryParse(string input, out int result) 
{
    return int.TryParse(input, out result);
}

if (TryParse("123", out int number)) 
{
    Console.WriteLine(number); // 123
}
```  

##### **2.4. Параметры с модификатором `in`**  
- Передача по ссылке, но только для чтения.  
- Полезно для больших структур, чтобы избежать копирования.  

```csharp
void Print(in LargeStruct data) 
{
    Console.WriteLine(data.Value); // Можно читать, но не изменять
}
```  

##### **2.5. Массивы параметров (`params`)**  
- Позволяет передавать переменное число аргументов.  

```csharp
int Sum(params int[] numbers) 
{
    return numbers.Sum();
}

int total = Sum(1, 2, 3, 4); // 10
```  

#### **3. Перегрузка методов**  
Можно создавать несколько методов с одним именем, но разными параметрами.  

```csharp
void Print(string text) 
{
    Console.WriteLine(text);
}

void Print(int number) 
{
    Console.WriteLine(number);
}

Print("Hello"); // Вызов первой версии
Print(42);      // Вызов второй версии
```  

#### **4. Необязательные параметры**  
Параметры можно сделать необязательными, задав значение по умолчанию.  

```csharp
void Greet(string name = "Guest") 
{
    Console.WriteLine($"Hello, {name}!");
}

Greet();           // Hello, Guest!
Greet("Alice");    // Hello, Alice!
```  

#### **5. Именованные аргументы**  
Позволяют передавать параметры в любом порядке, указывая их имена.  

```csharp
void ShowInfo(string name, int age) 
{
    Console.WriteLine($"{name}, {age} years old");
}

ShowInfo(age: 25, name: "Bob"); // Bob, 25 years old
```  

### **Заключение**  
- Методы помогают организовывать код.  
- Параметры бывают:  
  - По значению (обычные)  
  - По ссылке (`ref`, `out`)  
  - Только для чтения (`in`)  
  - Переменное количество (`params`)  
- Можно перегружать методы и использовать необязательные/именованные параметры.  

# **22. Требования к параметрам методов в C#**

В C# параметры методов должны соответствовать определенным правилам, чтобы код компилировался и работал корректно. Рассмотрим ключевые требования.

---

## **1. Общие требования**
### **1.1. Уникальность имен параметров**
- В пределах одного метода имена параметров должны быть **уникальными**.
- Нельзя использовать зарезервированные ключевые слова (`int`, `string`, `class` и т. д.) без префикса `@`.

❌ **Некорректно:**
```csharp
void Print(int a, int a) { } // Ошибка: дублирование имени параметра
void Print(int @int) { }     // Допустимо, но не рекомендуется
```

✅ **Корректно:**
```csharp
void Print(int a, int b) { } // OK
```

### **1.2. Совместимость типов**
- Типы параметров должны быть допустимыми в C# (не `void`, за исключением указателей в unsafe-коде).
- Можно использовать:
  - Примитивные типы (`int`, `bool`, `double`).
  - Ссылочные типы (`string`, `object`, классы).
  - Структуры (`DateTime`, `ValueTuple`).
  - Перечисления (`enum`).
  - Массивы, делегаты, generics.

❌ **Некорректно:**
```csharp
void Print(void value) { } // Ошибка: void нельзя использовать как тип параметра
```

✅ **Корректно:**
```csharp
void Print(int number) { }          // Примитив
void Print(string text) { }         // Ссылочный тип
void Print(DateTime date) { }       // Структура
void Print(Action callback) { }     // Делегат
```

---

## **2. Требования к параметрам с модификаторами**
### **2.1. `ref` и `out`**
- Переменная, передаваемая с `ref` или `out`, **должна быть инициализирована** (для `ref`).
- Метод **обязан присвоить значение** `out`-параметру перед выходом.

❌ **Некорректно:**
```csharp
int x;
ModifyRef(ref x); // Ошибка: x не инициализирован для ref

void ModifyRef(ref int value) { }
```

✅ **Корректно:**
```csharp
int x = 0;
ModifyRef(ref x); // OK

void ModifyOut(out int value) 
{
    value = 10; // Обязательное присваивание
}
```

### **2.2. `in` (параметр только для чтения)**
- Параметр передается по ссылке, но **не может быть изменен** внутри метода.
- Полезно для больших структур, чтобы избежать копирования.

❌ **Некорректно:**
```csharp
void Print(in int value) 
{
    value = 10; // Ошибка: параметр in нельзя изменять
}
```

✅ **Корректно:**
```csharp
void Print(in DateTime date) 
{
    Console.WriteLine(date.Year); // Только чтение
}
```

### **2.3. `params` (переменное число аргументов)**
- Должен быть **только один** `params` в методе.
- Должен быть **последним** параметром.
- Допустим только для **одномерных массивов**.

❌ **Некорректно:**
```csharp
void Sum(params int[] nums1, params string[] nums2) { } // Ошибка: два params
void Sum(int x, params int[] nums) { }                 // OK, но x должен быть перед params
```

✅ **Корректно:**
```csharp
void Sum(params int[] numbers) { } // OK
void Print(string format, params object[] args) { } // OK
```

---

## **3. Необязательные параметры**
- Должны иметь **значение по умолчанию**.
- Должны идти **после обязательных параметров** (если они есть).

❌ **Некорректно:**
```csharp
void Greet(string name = "User", int age) { } // Ошибка: необязательный параметр перед обязательным
```

✅ **Корректно:**
```csharp
void Greet(int age, string name = "User") { } // OK
void Log(string message, bool isEnabled = true) { } // OK
```

---

## **4. Перегрузка методов и параметры**
- Методы можно перегружать (создавать несколько версий с одним именем), но **сигнатуры должны отличаться**:
  - Количеством параметров.
  - Типами параметров (но не их именами!).
  - Модификаторами (`ref`, `out`, `in`).

❌ **Некорректно:**
```csharp
void Print(int a) { }
void Print(int b) { } // Ошибка: та же сигнатура
```

✅ **Корректно:**
```csharp
void Print(int a) { }             // Версия 1
void Print(string text) { }        // Версия 2 (другой тип)
void Print(ref int a) { }          // Версия 3 (ref)
void Print(int a, int b) { }       // Версия 4 (другой набор параметров)
```

---

## **5. Именованные аргументы**
- Можно передавать параметры в **любом порядке**, если указать их имена.
- Полезно для методов с множеством необязательных параметров.

✅ **Пример:**
```csharp
void Register(string name, int age = 18, string country = "Russia") { }

Register("Alice", country: "USA"); // age = 18 (по умолчанию), country = "USA"
```

---

## **Итог: основные правила**
1. **Имена параметров** должны быть уникальными в пределах метода.
2. **Типы параметров** должны быть допустимыми (`int`, `string`, `List<T>`, но не `void`).
3. **`ref`/`out`** требуют явной передачи ссылки, `out` обязывает присвоение.
4. **`params`** должен быть последним и только один.
5. **Необязательные параметры** должны идти после обязательных.
6. **Перегрузка методов** возможна только при разных сигнатурах.

# **25. Возвращение значений и оператор `return` в C#**

Оператор `return` используется для возврата значения из метода и завершения его выполнения. В C# все методы, кроме `void`, должны возвращать значение соответствующего типа.

---

## **1. Основные правила**
### **1.1. Методы с возвращаемым значением**
- Если метод объявлен с типом возвращаемого значения (`int`, `string`, `bool` и т. д.), он **обязан** вернуть значение этого типа.
- Компилятор выдаст ошибку, если возможен путь выполнения без `return`.

✅ **Пример корректного метода:**
```csharp
int Add(int a, int b)
{
    return a + b; // Обязательный return
}
```

❌ **Ошибка: не все пути возвращают значение**
```csharp
int Max(int a, int b)
{
    if (a > b)
        return a; // Если условие ложно, return не сработает!
    // Ошибка: не все пути кода возвращают значение
}
```

✅ **Исправленная версия:**
```csharp
int Max(int a, int b)
{
    if (a > b)
        return a;
    return b; // Все пути теперь покрыты
}
```

### **1.2. Методы без возвращаемого значения (`void`)**
- Если метод объявлен как `void`, он **не возвращает** значение.
- Можно использовать `return` для досрочного выхода из метода.

✅ **Пример:**
```csharp
void PrintPositive(int number)
{
    if (number <= 0)
        return; // Выход, если число не положительное

    Console.WriteLine(number);
}
```

---

## **2. Особенности работы `return`**
### **2.1. Возврат нескольких значений через кортежи**
C# позволяет возвращать несколько значений с помощью кортежей:

```csharp
(string, int) GetUserInfo()
{
    string name = "Alice";
    int age = 25;
    return (name, age); // Возврат кортежа
}

// Использование:
var user = GetUserInfo();
Console.WriteLine($"Name: {user.Item1}, Age: {user.Item2}");
```

### **2.2. Возврат ссылочных типов (`ref return`)**
С C# 7.0 можно возвращать **ссылку** на переменную (а не её копию):

```csharp
ref int Find(int[] numbers, int target)
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] == target)
            return ref numbers[i]; // Возвращаем ссылку на элемент массива
    }
    throw new Exception("Not found");
}

// Использование:
int[] arr = { 1, 2, 3 };
ref int x = ref Find(arr, 2);
x = 10; // Изменит массив: { 1, 10, 3 }
```

---

## **3. Возврат `null` и nullable-типы**
- Если метод возвращает ссылочный тип (`string`, `class`), он может вернуть `null`.
- Для **значимых типов** (например, `int`) нужно использовать **nullable-типы** (`int?`).

✅ **Пример:**
```csharp
string? FindName(int id) // "?" означает, что может вернуться null
{
    if (id == 1)
        return "Alice";
    return null; // OK
}

int? ParseInput(string input)
{
    if (int.TryParse(input, out int result))
        return result;
    return null; // OK, потому что int?
}
```

---

## **4. Возврат в асинхронных методах (`async`/`await`)**
- Асинхронные методы возвращают `Task` (если `void`) или `Task<T>` (если есть возвращаемое значение).
- Используется `return` вместе с `await`.

✅ **Пример:**
```csharp
async Task<string> DownloadDataAsync(string url)
{
    using (var client = new HttpClient())
    {
        string result = await client.GetStringAsync(url);
        return result; // Возвращаем string, но обёрнутый в Task<string>
    }
}
```

---

## **5. Исключения и `return`**
Если метод выбрасывает исключение, он может не возвращать значение:

```csharp
int Divide(int a, int b)
{
    if (b == 0)
        throw new DivideByZeroException(); // Прерывает выполнение
    return a / b;
}
```

---

## **6. Best Practices**
1. **Один `return` vs. несколько**:  
   - Раньше рекомендовали один `return` в конце метода.  
   - Сейчас допустимы несколько `return`, если это улучшает читаемость (например, в guard-условиях).  

2. **Именованные возвращаемые значения (C# 7.0+)**:  
   ```csharp
   (string Name, int Age) GetUser() => ("Bob", 30);
   var user = GetUser();
   Console.WriteLine(user.Name); // "Bob"
   ```

3. **Избегайте сложных возвращаемых структур**:  
   - Если метод возвращает много данных, лучше использовать **класс/структуру** вместо кортежа.  

---

## **Итог**
- `return` завершает выполнение метода и возвращает значение.
- Все пути выполнения в не-`void` методах должны возвращать значение.
- Можно возвращать:
  - Примитивы (`int`, `bool`).
  - Ссылочные типы (`string`, объекты).
  - Кортежи (`(int, string)`).
  - Ссылки (`ref int`).
  - `null` (для nullable-типов).
- В `async`-методах используется `Task<T>` + `return`.  

Пример итогового метода:  
```csharp
public (bool Success, string Message) TryParse(string input)
{
    if (string.IsNullOrEmpty(input))
        return (false, "Input is empty");

    return (true, "Parsed successfully");
}
```  

# **28. Свойства (Properties) в C#**

Свойства — это элементы класса, которые предоставляют гибкий механизм для чтения, записи или вычисления значений приватных полей. Они сочетают в себе преимущества полей и методов, обеспечивая контроль доступа к данным.  

---

## **1. Основные понятия**
### **1.1. Зачем нужны свойства?**
- **Инкапсуляция**: Скрывают внутреннее состояние объекта, предотвращая прямой доступ к полям.  
- **Валидация**: Позволяют проверять данные перед записью.  
- **Гибкость**: Можно добавить логику при чтении/записи (например, логгирование).  

### **1.2. Автоматические свойства (Auto-Property)**
Самый простой вариант, если не нужна дополнительная логика:  
```csharp
public string Name { get; set; } // Компилятор создаст скрытое приватное поле
```
- **Только для чтения**:  
  ```csharp
  public int Id { get; } = GenerateId(); // Можно инициализировать в конструкторе
  ```
- **Инициализация при объявлении**:  
  ```csharp
  public DateTime CreatedAt { get; set; } = DateTime.Now;
  ```

---

## **2. Полные свойства (Full Property)**
Используются, когда нужно добавить логику:  
```csharp
private string _name;

public string Name
{
    get { return _name; }
    set 
    { 
        if (string.IsNullOrEmpty(value))
            throw new ArgumentException("Name cannot be empty");
        _name = value; 
    }
}
```
- **Только get (read-only)**:  
  ```csharp
  public string FullName => $"{FirstName} {LastName}"; // Вычисляемое свойство
  ```
- **Только set (write-only)** (редко используется):  
  ```csharp
  private string _secret;
  public string Secret { set => _secret = value; }
  ```

---

## **3. Модификаторы доступа в свойствах**
Можно ограничивать доступ к get/set:  
```csharp
public string Password { get; private set; } // Запись только внутри класса
public int Counter { private get; set; }    // Чтение только внутри класса
```

---

## **4. Свойства и интерфейсы**
В интерфейсах можно объявлять свойства без реализации:  
```csharp
interface IUser
{
    string Name { get; set; }
    int Age { get; }
}

class User : IUser
{
    public string Name { get; set; }
    public int Age { get; } = 18;
}
```

---

## **5. Вычисляемые свойства**
Могут возвращать результат выражения:  
```csharp
public class Rectangle
{
    public double Width { get; set; }
    public double Height { get; set; }
    public double Area => Width * Height; // Нет отдельного поля
}
```

---

## **6. Свойства и INotifyPropertyChanged**
Часто используются в WPF для уведомления об изменении:  
```csharp
public class Person : INotifyPropertyChanged
{
    private string _name;
    public string Name
    {
        get => _name;
        set
        {
            _name = value;
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(Name)));
        }
    }
    public event PropertyChangedEventHandler PropertyChanged;
}
```

---

## **7. Сравнение свойств и полей**
| Критерий            | Поле (`public int X;`) | Свойство (`public int X { get; set; }`) |
|---------------------|-----------------------|------------------------------------------|
| Инкапсуляция        | Нет                   | Да                                       |
| Валидация           | Невозможна            | Возможна                                 |
| Сериализация        | Да                    | Да                                       |
| Привязка данных (WPF)| Нет                   | Да                                       |
| Потребление памяти  | Меньше                | Чуть больше (методы доступа)             |

---

## **8. Best Practices**
1. **Всегда используйте свойства** для публичных данных (даже если это auto-property).  
2. **Избегайте публичных полей** — они нарушают инкапсуляцию.  
3. **Для read-only** используйте `{ get; }` или `{ get; private set; }`.  
4. **Вычисляемые свойства** без побочных эффектов можно делать без backing field.  

---

## **Пример итогового класса**
```csharp
public class User
{
    // Auto-property с инициализацией
    public string Username { get; set; } = "guest";

    // Full property с валидацией
    private int _age;
    public int Age
    {
        get => _age;
        set => _age = value >= 0 ? value : throw new ArgumentException("Age cannot be negative");
    }

    // Read-only computed property
    public string Greeting => $"Hello, {Username}!";

    // Private setter
    public DateTime LastLogin { get; private set; }

    public void Login()
    {
        LastLogin = DateTime.Now;
    }
}
```

---

## **Когда использовать поля?**
Только для **приватных переменных класса**, если:  
- Они не требуют валидации.  
- Не участвуют в привязке данных.  
- Их не нужно сериализовать.  

Пример:  
```csharp
private readonly List<string> _internalCache = new();
```

# **29. Перегрузка методов (Method Overloading) в C#**

**Перегрузка методов** — это возможность создавать несколько методов с **одинаковым именем**, но **разными параметрами** (типом, количеством или порядком). Компилятор определяет, какой метод вызвать, на основе переданных аргументов.

---

## **1. Основные правила перегрузки**
Для перегрузки методы должны отличаться:
1. **Количеством параметров**  
2. **Типами параметров**  
3. **Порядком параметров** (если типы разные)  

❌ **Нельзя перегружать методы**, если разница только в:
- Возвращаемом типе (`int Sum()` vs `double Sum()`).  
- Модификаторах `ref`/`out` (`void Print(ref int)` vs `void Print(out int)` — **ошибка**).  
- Именах параметров (`void Print(string a)` vs `void Print(string b)` — **не перегрузка**).  

---

## **2. Примеры перегрузки методов**

### **2.1. Разное количество параметров**
```csharp
int Sum(int a, int b) => a + b;
int Sum(int a, int b, int c) => a + b + c; // Перегрузка
```

### **2.2. Разные типы параметров**
```csharp
void Print(int number) => Console.WriteLine($"Number: {number}");
void Print(string text) => Console.WriteLine($"Text: {text}"); // Перегрузка
```

### **2.3. Разный порядок параметров**
```csharp
void Show(string name, int age) => Console.WriteLine($"{name}, {age}");
void Show(int age, string name) => Console.WriteLine($"{age}: {name}"); // OK
```

### **2.4. Комбинация параметров**
```csharp
void Display(int a) { }
void Display(double a) { }
void Display(int a, string b) { }
```

---

## **3. Перегрузка и необязательные параметры**
Если добавить необязательные параметры, это **не считается перегрузкой**, но может привести к неоднозначности:

```csharp
void Greet(string name = "User") => Console.WriteLine($"Hello, {name}");
void Greet() => Console.WriteLine("Hello, World!");

Greet(); // ❌ Ошибка: неясно, какой метод вызывать
```

**Решение:** Удалить один из методов или изменить сигнатуру.

---

## **4. Перегрузка и приведение типов**
Компилятор выбирает **наиболее подходящий** метод. Если точного совпадения нет, используется **неявное приведение типов**:

```csharp
void Print(int x) => Console.WriteLine("int");
void Print(double x) => Console.WriteLine("double");

Print(10);   // "int" (точное совпадение)
Print(10.5); // "double" 
Print(10.2f); // "double" (float → double)
```

---

## **5. Перегрузка и модификаторы `params`, `ref`, `in`, `out`**
- `params` можно комбинировать с перегрузкой:
  ```csharp
  void Log(string message) { }
  void Log(params string[] messages) { } // OK
  ```
- `ref` и `out` **не могут** быть основой для перегрузки:
  ```csharp
  void Process(ref int x) { }
  void Process(out int x) { x = 0; } // ❌ Ошибка компиляции
  ```

---

## **6. Best Practices**
1. **Избегайте неочевидных перегрузок** — это может запутать других разработчиков.  
2. **Используйте перегрузку для одинаковой логики**, но с разными входными данными.  
   - Например, `Console.WriteLine()` имеет 19 перегрузок для разных типов.  
3. **Не злоупотребляйте `params`** — если параметров много, лучше использовать объекты или кортежи.  

---

## **7. Пример практического использования**
Допустим, у нас есть класс `Calculator`:

```csharp
public class Calculator
{
    // Сложение двух целых чисел
    public int Add(int a, int b) => a + b;

    // Сложение трех целых чисел
    public int Add(int a, int b, int c) => a + b + c;

    // Сложение чисел с плавающей точкой
    public double Add(double a, double b) => a + b;

    // Сложение массива чисел
    public int Add(params int[] numbers) => numbers.Sum();
}

// Использование:
var calc = new Calculator();
Console.WriteLine(calc.Add(1, 2));          // 3
Console.WriteLine(calc.Add(1.5, 2.3));      // 3.8
Console.WriteLine(calc.Add(1, 2, 3, 4, 5)); // 15
```

---

## **Итог**
- Перегрузка методов позволяет использовать **одно имя** для **разных реализаций**.  
- Главное правило — **разные сигнатуры** (типы/количество/порядок параметров).  
- Не перегружайте методы, если это усложняет код.  
- Используйте для методов, которые делают **похожие операции** с разными типами данных.  

**Пример из .NET:**  
```csharp
// Разные перегрузки метода Substring в классе string
string text = "Hello, World!";
text.Substring(7);    // "World!"
text.Substring(0, 5); // "Hello"
```

# **30. Статические члены и модификатор `static` в C#**

**Статические** члены класса принадлежат **самому классу**, а не его экземплярам. Они существуют в единственном экземпляре и доступны без создания объекта.  

---

## **1. Ключевые особенности `static`**
- **Общая память**: Статические поля хранят одно значение для всех экземпляров класса.  
- **Отсутствие привязки к объекту**: Не требуют создания экземпляра класса.  
- **Ограничения**:  
  - Не могут использовать нестатические члены класса (поля, методы, свойства).  
  - Не имеют доступа к `this`.  

---

## **2. Виды статических членов**
### **2.1. Статические поля**
```csharp
public class Counter
{
    public static int Count = 0; // Общее для всех объектов
    public int InstanceCount = 0;

    public Counter() 
    {
        Count++;        // Увеличивается для всех экземпляров
        InstanceCount++; // Увеличивается только для текущего
    }
}

// Использование:
var c1 = new Counter();
var c2 = new Counter();
Console.WriteLine(Counter.Count); // 2 (общее поле)
Console.WriteLine(c1.InstanceCount); // 1 (поле экземпляра)
```

### **2.2. Статические методы**
```csharp
public class MathUtils
{
    public static int Add(int a, int b) => a + b; // Вызов без создания объекта
}

// Использование:
int sum = MathUtils.Add(5, 3); // 8
```

### **2.3. Статические свойства**
```csharp
public class AppSettings
{
    private static string _version = "1.0";
    public static string Version 
    {
        get => _version;
        set => _version = value;
    }
}

// Использование:
Console.WriteLine(AppSettings.Version); // "1.0"
```

### **2.4. Статические конструкторы**
- Вызываются **один раз** перед первым использованием класса.  
- Не могут иметь параметров.  

```csharp
public class Logger
{
    public static string LogDirectory;

    static Logger() 
    {
        LogDirectory = Path.GetTempPath();
        Console.WriteLine("Статический конструктор вызван");
    }
}

// При первом обращении к классу:
var dir = Logger.LogDirectory; // Сработает статический конструктор
```

### **2.5. Статические классы**
- Нельзя создать экземпляр (`new` запрещен).  
- Могут содержать **только статические члены**.  

```csharp
public static class FileHelper
{
    public static string ReadAllText(string path) => File.ReadAllText(path);
}

// Использование:
string content = FileHelper.ReadAllText("test.txt");
```

---

## **3. Когда использовать `static`?**
✅ **Подходит для**:  
- Утилитарных функций (`Math.Sqrt`, `Console.WriteLine`).  
- Хранения общих данных (настройки, кеш).  
- Реализации паттернов (**Singleton**, Factory).  

❌ **Не подходит для**:  
- Объектов с состоянием (например, экземпляры `User`, `Order`).  
- Когда нужна полиморфность (переопределение через `virtual`/`override`).  

---

## **4. Примеры в .NET**
- **`Math`**: Все методы статические (`Math.Pow`, `Math.Max`).  
- **`Console`**: `Console.WriteLine()`, `Console.ReadKey()`.  
- **`DateTime.Now`**: Статическое свойство.  

---

## **5. Статические члены и потоки (Thread Safety)**
Статические поля **не потокобезопасны** по умолчанию!  

**Пример проблемы:**  
```csharp
public class Counter
{
    public static int Value = 0;

    public static void Increment() 
    {
        Value++; // Небезопасно при многопоточности
    }
}
```

**Решение:** Использовать `lock` или `Interlocked`:  
```csharp
private static object _lockObj = new object();

public static void IncrementSafe() 
{
    lock (_lockObj) 
    {
        Value++;
    }
}
```

---

## **6. Best Practices**
1. **Избегайте глобальных состояний**: Статические поля — аналог глобальных переменных.  
2. **Используйте для неизменяемых данных**: Например, константы (`public const string Name = "App";`).  
3. **Помните о потокобезопасности**: Если статическое поле изменяется, добавляйте синхронизацию.  

---

## **7. Пример: паттерн Singleton**
Статическое поле для хранения единственного экземпляра:  
```csharp
public class Singleton
{
    private static Singleton _instance;

    private Singleton() { } // Приватный конструктор

    public static Singleton Instance 
    {
        get 
        {
            if (_instance == null)
                _instance = new Singleton();
            return _instance;
        }
    }
}

// Использование:
var singleton = Singleton.Instance;
```

---

## **Итог**
- **`static`** — для членов, принадлежащих классу, а не объекту.  
- **Статические методы/поля** — вызов без создания экземпляра.  
- **Статические классы** — только для статических членов.  
- **Осторожно с многопоточностью** — используйте синхронизацию.  

**Пример:**  
```csharp
public static class Geometry
{
    public static double CircleArea(double r) => Math.PI * r * r;
    public static double TriangleArea(double b, double h) => 0.5 * b * h;
}

double area = Geometry.CircleArea(5); // 78.5398...
```

# **31. Рекурсивные функции в C#**

Рекурсивная функция — это функция, которая вызывает **саму себя** напрямую или через другую функцию. Она используется для решения задач, которые можно разбить на **подзадачи того же типа**.

---

## **1. Основные принципы рекурсии**
1. **Базовый случай** (условие выхода) — предотвращает бесконечную рекурсию.
2. **Рекурсивный случай** — вызов функции с измененными параметрами.

---

## **2. Примеры рекурсивных функций**

### **2.1. Факториал числа**
Факториал `n!` = `n * (n-1) * ... * 1`.  
Рекурсивное определение:  
- `0! = 1` (базовый случай),  
- `n! = n * (n-1)!` (рекурсивный случай).  

**Код:**  
```csharp
int Factorial(int n)
{
    if (n == 0) // Базовый случай
        return 1;
    return n * Factorial(n - 1); // Рекурсивный вызов
}

Console.WriteLine(Factorial(5)); // 120
```

### **2.2. Числа Фибоначчи**
Последовательность: `0, 1, 1, 2, 3, 5, 8, ...`  
Рекурсивное определение:  
- `Fib(0) = 0`,  
- `Fib(1) = 1`,  
- `Fib(n) = Fib(n-1) + Fib(n-2)`.  

**Код:**  
```csharp
int Fibonacci(int n)
{
    if (n == 0) return 0;
    if (n == 1) return 1;
    return Fibonacci(n - 1) + Fibonacci(n - 2);
}

Console.WriteLine(Fibonacci(6)); // 8
```
⚠️ **Проблема:** Неэффективность при больших `n` (экспоненциальная сложность `O(2ⁿ)`).  
✅ **Решение:** Мемоизация (кэширование результатов) или итеративный подход.

---

## **3. Глубина рекурсии и переполнение стека**
Рекурсия использует **стек вызовов**, который имеет ограниченный размер (~1 МБ по умолчанию).  
При слишком большой глубине возникает **`StackOverflowException`**.

**Пример опасной рекурсии:**  
```csharp
void InfiniteRecursion()
{
    InfiniteRecursion(); // Бесконечный вызов
}

// InfiniteRecursion(); // ❌ StackOverflowException
```

**Как избежать:**  
- Убедитесь, что есть **базовый случай**.  
- Используйте **итерации** (циклы) для глубокой рекурсии.  

---

## **4. Хвостовая рекурсия**
Оптимизация, при которой рекурсивный вызов — **последняя операция** в функции.  
В C# **не оптимизируется автоматически**, но можно переписать в цикл.  

**Пример (неоптимизированный):**  
```csharp
int Factorial(int n, int acc = 1)
{
    if (n == 0) return acc;
    return Factorial(n - 1, acc * n); // Хвостовой вызов
}
```

**Итеративный аналог:**  
```csharp
int Factorial(int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
        result *= i;
    return result;
}
```

---

## **5. Практические применения рекурсии**
### **5.1. Обход дерева (DFS)**
```csharp
class TreeNode
{
    public int Value;
    public TreeNode Left, Right;
}

void Traverse(TreeNode node)
{
    if (node == null) return; // Базовый случай
    Console.WriteLine(node.Value);
    Traverse(node.Left);  // Рекурсивный обход
    Traverse(node.Right);
}
```

### **5.2. Поиск в глубину (DFS) в графах**
```csharp
void Dfs(Node node, HashSet<Node> visited)
{
    if (visited.Contains(node)) return;
    visited.Add(node);
    foreach (var neighbor in node.Neighbors)
        Dfs(neighbor, visited);
}
```

### **5.3. Алгоритм быстрой сортировки (QuickSort)**
```csharp
void QuickSort(int[] arr, int left, int right)
{
    if (left < right)
    {
        int pivot = Partition(arr, left, right);
        QuickSort(arr, left, pivot - 1);
        QuickSort(arr, pivot + 1, right);
    }
}
```

---

## **6. Плюсы и минусы рекурсии**
✅ **Плюсы:**  
- Упрощает код для задач с **рекурсивной природой** (деревья, графы).  
- Позволяет элегантно выразить **математические определения**.  

❌ **Минусы:**  
- Риск **переполнения стека**.  
- Может быть **медленнее** итеративных решений.  
- Сложнее отлаживать при глубокой вложенности.  

---

## **7. Когда использовать рекурсию?**
- **Да**: Для задач с **рекурсивной структурой** (обход деревьев, комбинаторика).  
- **Нет**: Для линейных вычислений (сумма массива, факториал — лучше циклы).  

---

## **Итог**
1. Всегда определяйте **базовый случай**.  
2. Избегайте **бесконечной рекурсии**.  
3. Для сложных задач используйте **мемоизацию**.  
4. В C# предпочитайте **итерации** при большой глубине рекурсии.  

**Пример:**  
```csharp
// Рекурсивный вывод чисел от N до 1
void CountDown(int n)
{
    if (n == 0) return; // Базовый случай
    Console.WriteLine(n);
    CountDown(n - 1);
}

CountDown(5); // 5, 4, 3, 2, 1
```

# **32. Локальные функции в C#**

Локальные функции — это функции, объявленные внутри другого метода или свойства. Они помогают структурировать код, улучшают читаемость и позволяют избежать дублирования логики **в пределах одного метода**.

---

## **1. Основные особенности**
- **Видимость**: Доступны только внутри метода, где они объявлены.
- **Доступ к переменным**: Могут использовать локальные переменные и параметры родительского метода.
- **Где использовать**: Когда нужна вспомогательная функция, которая не требуется вне контекста текущего метода.

---

## **2. Синтаксис**
Локальная функция определяется внутри другого метода:
```csharp
public void OuterMethod()
{
    int x = 5;

    // Локальная функция
    void InnerFunction()
    {
        Console.WriteLine(x); // Может использовать переменные родительского метода
    }

    InnerFunction(); // Вызов
}
```

---

## **3. Примеры использования**
### **3.1. Простой пример: валидация данных**
```csharp
public void ProcessUserData(string name, int age)
{
    // Локальная функция для проверки возраста
    bool IsAgeValid(int userAge) => userAge >= 0 && userAge < 150;

    if (!IsAgeValid(age))
        throw new ArgumentException("Некорректный возраст");

    Console.WriteLine($"Имя: {name}, Возраст: {age}");
}
```

### **3.2. Рекурсивная локальная функция**
```csharp
public int CalculateFactorial(int n)
{
    if (n < 0)
        throw new ArgumentException("Число должно быть неотрицательным");

    // Локальная рекурсивная функция
    int Factorial(int k) => k <= 1 ? 1 : k * Factorial(k - 1);

    return Factorial(n);
}
```

### **3.3. Использование в LINQ-запросах**
```csharp
public IEnumerable<int> FilterNumbers(List<int> numbers, int threshold)
{
    // Локальная функция для фильтрации
    bool IsAboveThreshold(int num) => num > threshold;

    return numbers.Where(IsAboveThreshold);
}
```

---

## **4. Локальные функции vs. Приватные методы**
| Критерий            | Локальная функция                          | Приватный метод класса                   |
|---------------------|-------------------------------------------|------------------------------------------|
| **Область видимости** | Только внутри метода                      | Доступен всем методам класса             |
| **Доступ к переменным** | Может использовать локальные переменные   | Только через параметры                   |
| **Использование**    | Для логики, актуальной только в одном методе | Для повторного использования в классе   |

---

## **5. Захват переменных (Closure)**
Локальные функции могут захватывать переменные из родительского метода:
```csharp
public void CounterExample()
{
    int count = 0;

    // Локальная функция с захватом переменной
    void Increment() => count++;

    Increment();
    Increment();
    Console.WriteLine(count); // 2
}
```

⚠️ **Осторожно с многопоточностью!**  
Если локальная функция захватывает переменные, это может привести к неожиданному поведению в многопоточной среде.

---

## **6. Статические локальные функции (C# 8.0+)**
Чтобы запретить захват переменных, можно объявить функцию как `static`:
```csharp
public void Example()
{
    int x = 5;

    // Статическая локальная функция НЕ может использовать 'x'
    static int Add(int a, int b) => a + b;

    Console.WriteLine(Add(x, 10)); // 15
}
```

---

## **7. Best Practices**
1. **Используйте для сложной логики внутри метода**, которую нужно изолировать.
2. **Избегайте длинных локальных функций** — если логика большая, вынесите в отдельный метод класса.
3. **Помните о производительности**: Захват переменных создает экземпляр класса-замыкания, что может влиять на память.

---

## **8. Пример: кэширование с локальной функцией**
```csharp
public void ProcessData(List<int> data)
{
    var cache = new Dictionary<int, bool>();

    // Локальная функция с кэшированием
    bool IsPrime(int number)
    {
        if (cache.TryGetValue(number, out bool result))
            return result;

        // Проверка на простоту
        result = number > 1 && Enumerable.Range(2, (int)Math.Sqrt(number) - 1)
                                   .All(i => number % i != 0);
        cache[number] = result;
        return result;
    }

    var primes = data.Where(IsPrime).ToList();
}
```

---

## **Итог**
- **Локальные функции** помогают организовать код внутри метода.
- Могут **захватывать переменные** родительского метода.
- **Статические локальные функции** (C# 8.0+) запрещают захват.
- **Лучше приватных методов**, если логика нужна только в одном месте.

**Когда использовать:**  
✅ Для изоляции сложной логики внутри метода.  
✅ Для рекурсивных вспомогательных вычислений.  
✅ Если нужно избежать дублирования кода в методе.  

**Пример:**  
```csharp
public void PrintFibonacci(int n)
{
    int Fibonacci(int k) => k <= 1 ? k : Fibonacci(k - 1) + Fibonacci(k - 2);

    for (int i = 0; i < n; i++)
        Console.WriteLine(Fibonacci(i));
}
```

# **33. Конструкция `switch` в C#**

Конструкция `switch` позволяет выбирать одно из множества действий на основе значения выражения. В C# `switch` эволюционировал и теперь поддерживает:
- **Классический `switch`** (для примитивных типов и `enum`).
- **`switch` по шаблону (pattern matching)** (C# 7.0+).
- **Выражения `switch`** (C# 8.0+).

---

## **1. Классический `switch`**
Используется для сравнения с константными значениями.

### **Синтаксис:**
```csharp
switch (выражение)
{
    case значение1:
        // Код
        break;
    case значение2:
        // Код
        break;
    default:
        // Код, если нет совпадений
        break;
}
```

### **Пример:**
```csharp
string day = "Monday";

switch (day)
{
    case "Monday":
        Console.WriteLine("Понедельник");
        break;
    case "Tuesday":
        Console.WriteLine("Вторник");
        break;
    default:
        Console.WriteLine("Другой день");
        break;
}
```

### **Особенности:**
- `break` обязателен (кроме `return` или `throw`).
- `default` не обязателен, но рекомендуется.
- Поддерживает `enum`, числа, строки.

---

## **2. `switch` с `when` (условия в `case`)**
В C# 7.0+ можно добавлять условия через `when`:

### **Пример:**
```csharp
int number = 10;

switch (number)
{
    case int n when n > 0 && n < 5:
        Console.WriteLine("Меньше 5");
        break;
    case int n when n >= 5 && n < 10:
        Console.WriteLine("Между 5 и 10");
        break;
    default:
        Console.WriteLine("Другое");
        break;
}
```

---

## **3. Pattern Matching (сопоставление шаблонов)**
C# 7.0+ позволяет использовать более сложные шаблоны.

### **Типы шаблонов:**
- **Константный паттерн** (`case 5:`).
- **Тип-паттерн** (`case int i:`).
- **`var`-паттерн** (`case var x when x > 0:`).
- **Рекурсивные паттерны** (C# 8.0+).

### **Пример:**
```csharp
object obj = "Hello";

switch (obj)
{
    case int i:
        Console.WriteLine($"Это число: {i}");
        break;
    case string s:
        Console.WriteLine($"Это строка: {s}");
        break;
    case null:
        Console.WriteLine("Это null");
        break;
    default:
        Console.WriteLine("Неизвестный тип");
        break;
}
```

---

## **4. Выражения `switch` (C# 8.0+)**
`switch` может возвращать значение (как тернарный оператор).

### **Синтаксис:**
```csharp
var result = выражение switch
{
    шаблон1 => значение1,
    шаблон2 => значение2,
    _ => значение_по_умолчанию
};
```

### **Пример:**
```csharp
int number = 5;

string description = number switch
{
    1 => "Один",
    2 => "Два",
    > 2 and < 10 => "От 3 до 9",
    _ => "Другое"
};

Console.WriteLine(description); // "От 3 до 9"
```

---

## **5. Switch с деконструкцией (C# 9.0+)**
Можно использовать с кортежами и записями (`record`).

### **Пример:**
```csharp
var point = (x: 10, y: 20);

string quadrant = point switch
{
    ( > 0, > 0 ) => "I квадрант",
    ( < 0, > 0 ) => "II квадрант",
    ( < 0, < 0 ) => "III квадрант",
    ( > 0, < 0 ) => "IV квадрант",
    _ => "На оси"
};

Console.WriteLine(quadrant); // "I квадрант"
```

---

## **6. Итоговая таблица возможностей `switch`**

| Версия C# | Возможности |
|-----------|-------------|
| C# 1.0 | Классический `switch` (`int`, `enum`, `string`). |
| C# 7.0 | Pattern Matching, `when`, `var`-паттерны. |
| C# 8.0 | Выражения `switch`, рекурсивные паттерны. |
| C# 9.0 | Деконструкция в `switch`, логические паттерны (`and`, `or`, `not`). |

---

## **7. Best Practices**
1. **Используйте `switch`** вместо длинных `if-else` для множества условий.
2. **Применяйте `when`** для сложных условий.
3. **Выражения `switch`** удобны для возврата значений.
4. **Покрывайте все случаи** или добавляйте `default`.

---

## **Пример: классический `switch` + pattern matching**
```csharp
public string GetDescription(object obj)
{
    switch (obj)
    {
        case 0:
            return "Ноль";
        case int i when i > 0:
            return $"Положительное число: {i}";
        case string s when !string.IsNullOrEmpty(s):
            return $"Строка: {s}";
        case null:
            return "Null";
        default:
            return "Неизвестный объект";
    }
}
```

---

## **Пример: выражение `switch` (C# 8.0+)**
```csharp
public string GetWeatherDescription(int temp) => temp switch
{
    < 0 => "Мороз",
    >= 0 and < 15 => "Холодно",
    >= 15 and < 25 => "Тепло",
    >= 25 => "Жара",
    _ => "Ошибка"
};
```

# **34. Перечисления (`enum`) в C#**

**Перечисление (`enum`)** — это тип данных, который позволяет задать именованные константы для группы связанных значений. Это делает код более читаемым и безопасным, заменяя "магические числа" на понятные имена.

---

## **1. Основы enum**
### **1.1. Создание enum**
```csharp
enum DayOfWeek
{
    Monday,    // 0 (значение по умолчанию)
    Tuesday,   // 1
    Wednesday, // 2
    Thursday,  // 3
    Friday,    // 4
    Saturday,  // 5
    Sunday     // 6
}
```
- Каждый элемент имеет целочисленное значение (начинается с `0`).
- Можно явно указать значения:
  ```csharp
  enum Status
  {
      Active = 1,
      Inactive = 0,
      Pending = 2
  }
  ```

### **1.2. Использование enum**
```csharp
DayOfWeek today = DayOfWeek.Friday;
Console.WriteLine(today); // "Friday"

if (today == DayOfWeek.Friday)
{
    Console.WriteLine("Ура, пятница!");
}
```

---

## **2. Преобразование enum**
### **2.1. Enum → число**
```csharp
int dayNumber = (int)DayOfWeek.Monday; // 0
```

### **2.2. Число → enum**
```csharp
DayOfWeek day = (DayOfWeek)3; // Thursday
```

### **2.3. Enum → строка**
```csharp
string dayName = DayOfWeek.Monday.ToString(); // "Monday"
```

### **2.4. Строка → enum**
```csharp
DayOfWeek day;
if (Enum.TryParse("Tuesday", out day))
{
    Console.WriteLine(day); // Tuesday
}
```

---

## **3. Флаги (битовые enum)**
Перечисления можно использовать для хранения **набора флагов** с атрибутом `[Flags]`.

### **3.1. Пример с флагами**
```csharp
[Flags]
enum Permissions
{
    None = 0,      // 0b0000
    Read = 1,      // 0b0001
    Write = 2,     // 0b0010
    Execute = 4,   // 0b0100
    All = Read | Write | Execute // 0b0111 (7)
}
```

### **3.2. Работа с флагами**
```csharp
Permissions userPermissions = Permissions.Read | Permissions.Write;

// Проверка наличия флага
if (userPermissions.HasFlag(Permissions.Read))
{
    Console.WriteLine("Есть доступ на чтение");
}

// Добавление флага
userPermissions |= Permissions.Execute;

// Удаление флага
userPermissions &= ~Permissions.Write;
```

---

## **4. Дополнительные возможности**
### **4.1. Получение всех значений enum**
```csharp
foreach (DayOfWeek day in Enum.GetValues(typeof(DayOfWeek)))
{
    Console.WriteLine(day);
}
```

### **4.2. Проверка существования значения**
```csharp
bool isValid = Enum.IsDefined(typeof(DayOfWeek), 10); // false (нет дня с номером 10)
```

### **4.3. Получение списка имен**
```csharp
string[] dayNames = Enum.GetNames(typeof(DayOfWeek));
// ["Monday", "Tuesday", ...]
```

---

## **5. Best Practices**
1. **Используйте `enum`** вместо чисел, если возможные значения фиксированы.
2. **Для флагов** применяйте `[Flags]` и степени двойки (`1, 2, 4, 8, ...`).
3. **Проверяйте значения** через `Enum.IsDefined`, если данные приходят извне.
4. **Избегайте "магических чисел"** — всегда обращайтесь к enum по имени.

---

## **6. Пример: обработка статуса заказа**
```csharp
enum OrderStatus
{
    New = 0,
    Processing = 1,
    Shipped = 2,
    Delivered = 3,
    Cancelled = 4
}

OrderStatus status = OrderStatus.Processing;

switch (status)
{
    case OrderStatus.New:
        Console.WriteLine("Заказ создан");
        break;
    case OrderStatus.Processing:
        Console.WriteLine("Заказ в обработке");
        break;
    case OrderStatus.Shipped:
        Console.WriteLine("Заказ отправлен");
        break;
    default:
        Console.WriteLine("Статус неизвестен");
        break;
}
```

---

## **7. Итог**
- **`enum`** делает код понятнее, заменяя числа на имена.
- Поддерживает **флаги** (`[Flags]`) для битовых операций.
- Можно **конвертировать** в строки и числа.
- Полезен для **`switch`**, **аргументов методов** и **состояний объектов**.

**Пример флагов:**
```csharp
[Flags]
enum FileAccess
{
    Read = 1,
    Write = 2,
    ReadWrite = Read | Write
}

var access = FileAccess.ReadWrite;
Console.WriteLine(access.HasFlag(FileAccess.Write)); // true
```

# **35. Лямбда-выражения в C#**  

**Лямбда-выражения** — это краткий способ записи **анонимных функций**, которые можно передавать в методы, хранить в переменных или использовать в LINQ. Они делают код компактнее и выразительнее.  

---

## **1. Основные виды лямбда-выражений**  
В C# есть два типа:  
1. **Лямбда-оператор** (многострочный, с `=> { ... }`).  
2. **Лямбда-выражение** (однострочное, с `=>`).  

### **Примеры:**  
```csharp
// 1. Лямбда-оператор (многострочный)
Action<string> printMessage = (message) => 
{
    Console.WriteLine($"Сообщение: {message}");
};

// 2. Лямбда-выражение (однострочное)
Func<int, int, int> sum = (a, b) => a + b;
```

---

## **2. Синтаксис лямбда-выражений**  
### **2.1. Без параметров**  
```csharp
Action greet = () => Console.WriteLine("Hello!");
greet(); // Hello!
```

### **2.2. С параметрами**  
```csharp
Func<int, int, int> multiply = (x, y) => x * y;
Console.WriteLine(multiply(3, 4)); // 12
```

### **2.3. С одним параметром (скобки можно опустить)**  
```csharp
Func<int, bool> isEven = num => num % 2 == 0;
Console.WriteLine(isEven(4)); // true
```

---

## **3. Захват переменных (Closure)**  
Лямбды могут захватывать переменные из внешней области видимости:  
```csharp
int threshold = 10;
Func<int, bool> isAboveThreshold = x => x > threshold;

Console.WriteLine(isAboveThreshold(15)); // true
threshold = 20;
Console.WriteLine(isAboveThreshold(15)); // false (значение threshold изменилось)
```

⚠️ **Осторожно в многопоточном коде!** Захваченные переменные могут привести к неожиданному поведению.  

---

## **4. Лямбды в LINQ**  
Лямбда-выражения часто используются в LINQ для фильтрации, сортировки и преобразования данных.  

### **Пример с `Where`, `Select`, `OrderBy`:**  
```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };

// Фильтрация
var evenNumbers = numbers.Where(x => x % 2 == 0); // [2, 4]

// Преобразование
var squared = numbers.Select(x => x * x); // [1, 4, 9, 16, 25]

// Сортировка
var sorted = numbers.OrderBy(x => -x); // [5, 4, 3, 2, 1]
```

---

## **5. Лямбды vs. Делегаты vs. Локальные функции**  
| Критерий          | Лямбда-выражение          | Делегат (`Action`, `Func`) | Локальная функция (`void Foo()`) |  
|-------------------|--------------------------|---------------------------|----------------------------------|  
| **Синтаксис**     | `(x) => x * 2`           | `delegate(int x) { ... }`  | `void Foo() { ... }`             |  
| **Захват переменных** | Да (closure)          | Да (если анонимный метод)  | Да                               |  
| **Использование** | В LINQ, событиях         | Устаревший подход          | Для сложной логики внутри метода |  

---

## **6. Лямбды в событиях**  
Лямбды удобны для подписки на события:  
```csharp
button.Click += (sender, args) => Console.WriteLine("Кнопка нажата!");
```

---

## **7. Best Practices**  
✅ **Используйте лямбды:**  
- Для коротких операций (фильтрация, преобразование).  
- В LINQ и событиях.  

❌ **Избегайте:**  
- Сложной логики (лучше вынести в отдельный метод).  
- Длинных лямбд (ухудшает читаемость).  

---

## **8. Примеры**  
### **8.1. Фильтрация списка**  
```csharp
var users = new List<User> { new User("Alice", 25), new User("Bob", 17) };
var adults = users.Where(user => user.Age >= 18); // Alice
```

### **8.2. Сортировка по имени**  
```csharp
var sortedUsers = users.OrderBy(user => user.Name);
```

### **8.3. Группировка**  
```csharp
var groupedByAge = users.GroupBy(user => user.Age > 18 ? "Adult" : "Teen");
```

---

## **Итог**  
- **Лямбда-выражения** — это анонимные функции, которые упрощают код.  
- Используются в **LINQ**, **событиях**, **делегатах**.  
- Могут **захватывать переменные** из внешнего контекста (closure).  
- Лучше подходят для **простых операций**, для сложной логики используйте методы.  

**Пример итогового кода:**  
```csharp
var numbers = new[] { 1, 2, 3, 4, 5 };
var evenSquares = numbers
    .Where(x => x % 2 == 0)
    .Select(x => x * x); // [4, 16]
```

# **36. Классы и объекты в C#**

Классы и объекты — это основа объектно-ориентированного программирования (ООП) в C#. Они позволяют структурировать код, инкапсулируя данные и поведение в логические единицы.

---

## **1. Классы**
**Класс** — это шаблон или чертёж, который определяет:
- **Поля** (данные)
- **Свойства** (контролируемый доступ к полям)
- **Методы** (действия, которые можно выполнять)
- **Конструкторы** (инициализация объекта)
- **События** (уведомления о действиях)

### **1.1. Синтаксис класса**
```csharp
public class Person
{
    // Поля (обычно private)
    private string _name;
    private int _age;

    // Свойства (контролируемый доступ)
    public string Name
    {
        get => _name;
        set => _name = value ?? throw new ArgumentNullException(nameof(value));
    }

    public int Age
    {
        get => _age;
        set => _age = value >= 0 ? value : throw new ArgumentException("Возраст не может быть отрицательным");
    }

    // Конструктор (инициализация объекта)
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Метод
    public void Greet()
    {
        Console.WriteLine($"Привет, меня зовут {Name} и мне {Age} лет!");
    }
}
```

---

## **2. Объекты**
**Объект** — это экземпляр класса, созданный с помощью оператора `new`.

### **2.1. Создание объекта**
```csharp
Person person = new Person("Алексей", 30);
person.Greet(); // Привет, меня зовут Алексей и мне 30 лет!
```

### **2.2. Доступ к членам класса**
```csharp
person.Name = "Иван"; // Установка свойства
Console.WriteLine(person.Age); // Чтение свойства
```

---

## **3. Конструкторы**
Конструктор — это специальный метод, который вызывается при создании объекта.

### **3.1. Виды конструкторов**
- **Конструктор по умолчанию** (без параметров)
- **Параметризованный конструктор**
- **Статический конструктор** (вызывается один раз при первом обращении к классу)

```csharp
public class Car
{
    public string Model { get; }
    public int Year { get; }

    // Конструктор по умолчанию
    public Car()
    {
        Model = "Неизвестно";
        Year = DateTime.Now.Year;
    }

    // Параметризованный конструктор
    public Car(string model, int year)
    {
        Model = model;
        Year = year;
    }

    // Статический конструктор
    static Car()
    {
        Console.WriteLine("Класс Car инициализирован");
    }
}
```

---

## **4. Модификаторы доступа**
| Модификатор  | Доступность                          |
|--------------|--------------------------------------|
| `public`     | Доступно всем                        |
| `private`    | Только внутри класса                 |
| `protected`  | Класс и наследники                   |
| `internal`   | В пределах сборки                    |
| `protected internal` | Класс, наследники или сборка |

---

## **5. Статические члены класса**
Принадлежат классу, а не объекту. Вызываются через имя класса.

```csharp
public class MathHelper
{
    public static double Pi => 3.14159;

    public static int Add(int a, int b) => a + b;
}

// Использование
double pi = MathHelper.Pi;
int sum = MathHelper.Add(5, 3);
```

---

## **6. Наследование**
Класс может наследовать от другого класса, получая его члены.

```csharp
public class Animal
{
    public string Name { get; set; }

    public virtual void MakeSound()
    {
        Console.WriteLine("Звук животного");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Гав-гав!");
    }
}

// Использование
Animal myDog = new Dog { Name = "Бобик" };
myDog.MakeSound(); // Гав-гав!
```

---

## **7. Полиморфизм**
Возможность объектов одного типа вести себя по-разному.

```csharp
public class Shape
{
    public virtual void Draw() => Console.WriteLine("Рисуем фигуру");
}

public class Circle : Shape
{
    public override void Draw() => Console.WriteLine("Рисуем круг");
}

// Использование
Shape shape = new Circle();
shape.Draw(); // Рисуем круг
```

---

## **8. Абстрактные классы и методы**
Нельзя создать экземпляр абстрактного класса. Содержит абстрактные методы, которые должны быть реализованы в наследниках.

```csharp
public abstract class Vehicle
{
    public abstract void Move();
}

public class Car : Vehicle
{
    public override void Move() => Console.WriteLine("Едем по дороге");
}
```

---

## **9. Интерфейсы**
Контракт, который класс может реализовать. В C# 8.0+ могут содержать реализации по умолчанию.

```csharp
public interface IFlyable
{
    void Fly();
}

public class Bird : IFlyable
{
    public void Fly() => Console.WriteLine("Лечу как птица");
}
```

---

## **10. Best Practices**
1. **Инкапсуляция**: Делайте поля `private`, предоставляя доступ через свойства.
2. **SOLID**: Следуйте принципам ООП.
3. **Композиция вместо наследования**: Лучше включать объекты, чем наследовать.
4. **Именование**: Классы — существительные в `PascalCase`, методы — глаголы.

---

## **Итог**
- **Класс** — шаблон, **объект** — его экземпляр.
- **Инкапсуляция**, **наследование**, **полиморфизм** — три кита ООП.
- Используйте **конструкторы** для инициализации.
- **Статические члены** принадлежат классу.
- **Интерфейсы** определяют контракты.

**Пример итогового класса:**
```csharp
public class Book
{
    public string Title { get; }
    public string Author { get; }
    public int Pages { get; }

    public Book(string title, string author, int pages)
    {
        Title = title;
        Author = author;
        Pages = pages;
    }

    public string GetInfo() => $"{Title} by {Author}, {Pages} pages";
}

// Использование
var book = new Book("Война и мир", "Л. Толстой", 1225);
Console.WriteLine(book.GetInfo());
```

# **37. Конструкторы, инициализаторы и деконструкторы в C#**

## **1. Конструкторы**
Конструкторы — специальные методы, вызываемые при создании объекта. Они инициализируют поля и свойства.

### **1.1. Виды конструкторов**
#### **Конструктор по умолчанию**
- Если не определен ни один конструктор, компилятор создаёт пустой конструктор.
- Если есть хотя бы один пользовательский конструктор, конструктор по умолчанию **не создаётся автоматически**.

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    // Конструктор по умолчанию (если не указан явно)
    public Person() { }
}
```

#### **Параметризованный конструктор**
```csharp
public class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}

var person = new Person("Алексей", 30);
```

#### **Статический конструктор**
- Вызывается **один раз** при первом обращении к классу.
- Не может иметь параметров.
- Используется для инициализации статических полей.

```csharp
public class Logger
{
    public static string LogDirectory;

    static Logger()
    {
        LogDirectory = Path.GetTempPath();
    }
}
```

#### **Конструктор копирования**
```csharp
public class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person(Person other)
    {
        Name = other.Name;
        Age = other.Age;
    }
}

var person1 = new Person("Алексей", 30);
var person2 = new Person(person1); // Копия
```

---

## **2. Инициализаторы объектов (Object Initializers)**
Позволяют задавать свойства объекта **после создания** в удобном синтаксисе.

### **2.1. Базовый пример**
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

var person = new Person { Name = "Алексей", Age = 30 };
```

### **2.2. Инициализация коллекций**
```csharp
var people = new List<Person>
{
    new Person { Name = "Алексей", Age = 30 },
    new Person { Name = "Мария", Age = 25 }
};
```

### **2.3. Инициализаторы в анонимных типах**
```csharp
var user = new { Name = "Алексей", Age = 30 };
Console.WriteLine(user.Name);
```

---

## **3. Деконструкторы (Deconstructors)**
Позволяют "разобрать" объект на отдельные переменные.

### **3.1. Реализация деконструктора**
```csharp
public class Person
{
    public string Name { get; }
    public int Age { get; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    public void Deconstruct(out string name, out int age)
    {
        name = Name;
        age = Age;
    }
}
```

### **3.2. Использование деконструктора**
```csharp
var person = new Person("Алексей", 30);

// Вариант 1: Явный вызов Deconstruct
person.Deconstruct(out string name, out int age);

// Вариант 2: Синтаксис деконструкции
var (name, age) = person;

Console.WriteLine($"{name}, {age}"); // Алексей, 30
```

### **3.3. Деконструкция в кортежах**
```csharp
var point = (X: 10, Y: 20);
var (x, y) = point;
Console.WriteLine($"{x}, {y}"); // 10, 20
```

---

## **4. Сравнение конструкторов, инициализаторов и деконструкторов**
| Функция            | Назначение                                                                 | Пример |
|--------------------|----------------------------------------------------------------------------|--------|
| **Конструктор**    | Инициализация объекта при создании                                         | `new Person("Алексей", 30)` |
| **Инициализатор**  | Удобное задание свойств после создания                                     | `new Person { Name = "Алексей" }` |
| **Деконструктор**  | Разбор объекта на отдельные переменные                                     | `var (name, age) = person;` |

---

## **5. Best Practices**
✅ **Конструкторы:**
- Используйте для обязательной инициализации объекта.
- Избегайте сложной логики в конструкторах.

✅ **Инициализаторы:**
- Подходят для гибкого создания объектов.
- Удобны при работе с DTO (Data Transfer Objects).

✅ **Деконструкторы:**
- Полезны для кортежей и распаковки сложных объектов.
- Упрощают работу с `out`-параметрами.

---

## **Итог**
- **Конструкторы** — основа создания объектов.
- **Инициализаторы** — удобный синтаксис для настройки свойств.
- **Деконструкторы** — позволяют "разбирать" объекты на переменные.

**Пример итогового класса:**
```csharp
public class Car
{
    public string Model { get; }
    public int Year { get; }

    // Конструктор
    public Car(string model, int year)
    {
        Model = model;
        Year = year;
    }

    // Деконструктор
    public void Deconstruct(out string model, out int year)
    {
        model = Model;
        year = Year;
    }
}

// Использование
var car = new Car("Tesla", 2023);
var (model, year) = car;
Console.WriteLine($"{model} {year}"); // Tesla 2023
```

# **38. Создание и уничтожение объектов в C#**

В C# работа с объектами включает их создание, использование и освобождение ресурсов. В отличие от языков с ручным управлением памятью (например, C++), в C# используется **автоматическая сборка мусора (Garbage Collection, GC)**, но понимание процесса важно для эффективной работы.

---

## **1. Создание объектов**
Объекты создаются с помощью оператора `new`, который:
1. Выделяет память в **управляемой куче** (managed heap).
2. Вызывает **конструктор** для инициализации объекта.

### **1.1. Простое создание объекта**
```csharp
Person person = new Person("Алексей", 30);
```

### **1.2. Инициализация свойств при создании**
```csharp
var person = new Person 
{ 
    Name = "Алексей", 
    Age = 30 
};
```

### **1.3. Создание массива объектов**
```csharp
Person[] people = new Person[3];
people[0] = new Person("Алексей", 30);
```

---

## **2. Уничтожение объектов и сборка мусора (Garbage Collection)**
В C# **нельзя явно удалить объект**. Память освобождается автоматически **сборщиком мусора** (GC), когда объект становится недостижимым.

### **2.1. Как работает GC?**
1. **Поколения (Generations)**:
   - **Gen 0**: Новые объекты (сборка происходит часто).
   - **Gen 1**: Объекты, пережившие одну сборку.
   - **Gen 2**: Долгоживущие объекты (сборка редкая).
2. **Алгоритм работы**:
   - GC находит недостижимые объекты (на которые нет ссылок).
   - Освобождает память и вызывает **финализаторы** (если есть).

### **2.2. Финализаторы (`finalizer`)**
Финализатор — метод, который вызывается перед удалением объекта GC.  
⚠️ **Не путать с деструкторами в C++!**

```csharp
public class ResourceHolder
{
    // Финализатор (вызывается GC)
    ~ResourceHolder() 
    {
        Console.WriteLine("Финализатор вызван");
    }
}
```

**Проблемы финализаторов:**
- Не вызываются мгновенно (только при сборке мусора).
- Могут не вызваться вообще (если программа завершится).
- Замедляют работу GC.

---

## **3. Освобождение ресурсов: `IDisposable`**
Если объект использует **неуправляемые ресурсы** (файлы, сетевые подключения), нужно реализовать `IDisposable`.

### **3.1. Паттерн `Dispose`**
```csharp
public class FileWriter : IDisposable
{
    private StreamWriter _writer;

    public FileWriter(string path)
    {
        _writer = new StreamWriter(path);
    }

    public void Write(string text)
    {
        _writer.WriteLine(text);
    }

    // Реализация IDisposable
    public void Dispose()
    {
        _writer?.Dispose();
        GC.SuppressFinalize(this); // Отменяет вызов финализатора
    }

    // Финализатор (на случай, если Dispose не вызвали)
    ~FileWriter()
    {
        Dispose();
    }
}
```

### **3.2. Использование `using`**
Автоматически вызывает `Dispose()` даже при исключении.

```csharp
using (var writer = new FileWriter("log.txt"))
{
    writer.Write("Hello, world!");
} // Dispose() вызывается здесь
```

**Синтаксис `using` без скобок (C# 8.0+):**
```csharp
using var writer = new FileWriter("log.txt");
writer.Write("Hello");
// Dispose() вызовется при выходе из области видимости
```

---

## **4. Когда вызывается сборка мусора?**
- **Автоматически**: Когда заканчивается память в Gen 0.
- **Вручную** (не рекомендуется): 
  ```csharp
  GC.Collect(); // Принудительная сборка
  GC.WaitForPendingFinalizers(); // Ожидание финализаторов
  ```

---

## **5. Best Practices**
✅ **Правильное создание объектов**:
- Используйте конструкторы для обязательной инициализации.
- Для гибкости — инициализаторы объектов.

✅ **Освобождение ресурсов**:
- Всегда используйте `using` для `IDisposable`.
- Избегайте финализаторов (только как fallback).

❌ **Чего избегать**:
- Явного вызова `GC.Collect()` (нарушает оптимизации GC).
- Долгих операций в финализаторах.

---

## **6. Пример: работа с файлом**
```csharp
public void ProcessFile(string path)
{
    // using гарантирует вызов Dispose()
    using (var reader = new StreamReader(path))
    {
        string content = reader.ReadToEnd();
        Console.WriteLine(content);
    }
}
```

**Аналог с C# 8.0+:**
```csharp
public void ProcessFile(string path)
{
    using var reader = new StreamReader(path);
    string content = reader.ReadToEnd();
    Console.WriteLine(content);
} // reader.Dispose() вызывается здесь
```

---

## **Итог**
- **Создание**: `new` + конструктор / инициализатор.
- **Уничтожение**: Автоматически (GC) + `IDisposable` для ресурсов.
- **Правила**:
  - Для управляемых объектов — доверяйте GC.
  - Для файлов, подключений — `using` + `IDisposable`.
  - Финализаторы — только как резервный вариант.

# **39. Класс `Program` и метод `Main` в C#**

В C# точка входа в программу — это метод `Main`. Начиная с C# 9.0, появилась упрощённая модель **"Программы верхнего уровня" (Top-Level Statements)**, которая позволяет писать код без явного объявления класса `Program` и метода `Main`.

---

## **1. Классический подход (до C# 9.0)**
### **1.1. Базовая структура**
```csharp
using System;

namespace MyApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

### **1.2. Варианты метода `Main`**
Метод `Main` может быть:
- **`void`** или **`int`** (возвращает код завершения).
- **С параметрами `string[] args`** (аргументы командной строки) или без них.

```csharp
// Возвращает код ошибки
static int Main(string[] args)
{
    if (args.Length == 0)
    {
        Console.WriteLine("Не указаны аргументы!");
        return 1; // Код ошибки
    }
    return 0; // Успешное завершение
}
```

### **1.3. Асинхронный `Main` (C# 7.1+)**
```csharp
static async Task Main(string[] args)
{
    await Task.Delay(1000);
    Console.WriteLine("Hello, async World!");
}
```

---

## **2. Программы верхнего уровня (C# 9.0+)**
Упрощённый синтаксис, где:
- Не нужно объявлять `class Program` и `static void Main`.
- Код пишется **напрямую в файле `.cs`**.
- Аргументы командной строки доступны через магическую переменную `args`.

### **2.1. Простейший пример**
```csharp
// Программа верхнего уровня (C# 9.0+)
Console.WriteLine("Hello, World!");
```

### **2.2. Использование аргументов**
```csharp
if (args.Length > 0)
{
    Console.WriteLine($"Первый аргумент: {args[0]}");
}
else
{
    Console.WriteLine("Аргументы не переданы.");
}
```

### **2.3. Асинхронный код**
```csharp
await Task.Delay(1000);
Console.WriteLine("Hello after delay!");
```

---

## **3. Что происходит "под капотом" в Top-Level Statements?**
Компилятор автоматически генерирует:
1. Класс `Program` с методом `Main`.
2. Оборачивает ваш код в этот метод.

**Пример эквивалентного кода:**
```csharp
// Ваш код:
Console.WriteLine("Hello");

// Во что компилируется:
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello");
    }
}
```

---

## **4. Ограничения Top-Level Statements**
1. **Только один файл** в проекте может содержать такой код.
2. **Нельзя смешивать** с обычными объявлениями классов в одном файле.
   ```csharp
   Console.WriteLine("Hello"); // OK
   
   class MyClass { } // Ошибка!
   ```
3. **Нельзя использовать** в библиотеках (только в приложениях).

---

## **5. Когда что использовать?**
| **Ситуация**                     | **Классический `Main`** | **Top-Level Statements** |
|----------------------------------|------------------------|--------------------------|
| Простые консольные утилиты       | ⚠️ Избыточно          | ✅ Идеально             |
| Большие проекты                  | ✅ Лучше структура     | ⚠️ Не всегда удобно     |
| Работа с аргументами командной строки | ✅ Гибко              | ✅ Удобно (`args`)      |
| Асинхронный код                  | ✅ `async Task Main`   | ✅ `await` напрямую     |

---

## **6. Best Practices**
✅ **Используйте Top-Level Statements** для:
- Небольших скриптов.
- Быстрого прототипирования.
- Обучения (меньше boilerplate-кода).

✅ **Классический `Main`** лучше для:
- Больших приложений.
- Когда нужны явные объявления классов в том же файле.

---

## **7. Пример: консольный калькулятор (Top-Level)**
```csharp
if (args.Length != 2)
{
    Console.WriteLine("Использование: calc <число1> <число2>");
    return;
}

if (!double.TryParse(args[0], out double a) || !double.TryParse(args[1], out double b))
{
    Console.WriteLine("Ошибка: введите числа!");
    return;
}

Console.WriteLine($"Результат: {a + b}");
```

---

## **8. Как вернуться к классическому `Main` в новых проектах?**
1. Создайте проект:  
   ```bash
   dotnet new console --use-program-main
   ```
2. Или измените `.csproj`:  
   ```xml
   <PropertyGroup>
     <OutputType>Exe</OutputType>
     <LangVersion>latest</LangVersion>
     <UseProgramMain>true</UseProgramMain>
   </PropertyGroup>
   ```

---

## **Итог**
- **Классический `Main`** — явное объявление, больше контроля.
- **Top-Level Statements** — минимум кода, удобно для скриптов.
- **Асинхронность** поддерживается в обоих подходах.

**Пример классического `Main` с аргументами:**
```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine($"Привет, {args[0]}!");
    }
}
```

**Пример Top-Level:**
```csharp
Console.WriteLine($"Привет, {args[0]}!");
```

# **40. Структуры (`struct`) в C#**

Структуры — это **типы значений** (value types), которые хранятся в стеке (если не являются частью ссылочного типа). Они похожи на классы, но имеют ключевые отличия и применяются для небольших, неделимых данных.

---

## **1. Основные особенности структур**
- **Тип значения** (не ссылка, как у классов).
- **Хранятся в стеке** (если не встроены в ссылочный тип).
- **Не поддерживают наследование** (кроме интерфейсов).
- **Не могут быть `null`** (кроме `Nullable<T>`).
- **Имеют конструктор по умолчанию**, даже если не объявлен (инициализирует поля нулями).

---

## **2. Синтаксис объявления структуры**
```csharp
public struct Point
{
    // Поля (не могут быть инициализированы при объявлении)
    public int X;
    public int Y;

    // Конструктор (должен инициализировать все поля)
    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    // Метод
    public void Print() => Console.WriteLine($"({X}, {Y})");
}
```

---

## **3. Когда использовать структуры?**
✅ **Подходит для**:
- Небольших данных (координаты, цвет, размер).
- Неизменяемых (immutable) типов.
- Часто используемых в вычислениях (например, `Vector3` в Unity).

❌ **Не подходит для**:
- Сложных объектов с логикой.
- Данных, требующих наследования.

---

## **4. Отличия структур от классов**
| Характеристика          | Структура (`struct`)       | Класс (`class`)           |
|-------------------------|----------------------------|---------------------------|
| **Тип**                 | Значение (stack)           | Ссылка (heap)             |
| **Наследование**        | Только интерфейсы          | Полная поддержка          |
| **`null`**              | Только `Nullable<T>`       | Да                        |
| **Конструктор по умолчанию** | Автоматически (нельзя переопределить) | Можно задать |
| **Изменчивость**        | Рекомендуется `readonly`   | Любая                     |

---

## **5. Примеры использования**
### **5.1. Простая структура (координата)**
```csharp
public readonly struct Vector2D
{
    public readonly double X;
    public readonly double Y;

    public Vector2D(double x, double y) => (X, Y) = (x, y);
    public double Magnitude => Math.Sqrt(X * X + Y * Y);
}

// Использование
var point = new Vector2D(3, 4);
Console.WriteLine(point.Magnitude); // 5
```

### **5.2. Структура с методами**
```csharp
public struct RGBColor
{
    public byte R, G, B;

    public RGBColor(byte r, byte g, byte b) => (R, G, B) = (r, g, b);
    public string ToHex() => $"#{R:X2}{G:X2}{B:X2}";
}

var red = new RGBColor(255, 0, 0);
Console.WriteLine(red.ToHex()); // #FF0000
```

---

## **6. `readonly struct` (C# 7.2+)**
Запрещает изменение полей после создания:
```csharp
public readonly struct ImmutablePoint
{
    public int X { get; }
    public int Y { get; }

    public ImmutablePoint(int x, int y) => (X, Y) = (x, y);
}

var p = new ImmutablePoint(10, 20);
// p.X = 5; // Ошибка: нельзя изменить readonly поле
```

---

## **7. `ref struct` (C# 7.2+)**
- Не может быть упакована (boxing).
- Не может быть полем класса (только стек).
- Используется для оптимизации (например, `Span<T>`).

```csharp
public ref struct StackOnlyStruct
{
    public int Value;
}
```

---

## **8. Лучшие практики**
1. **Делайте структуры небольшими** (≤ 16 байт).
2. **Используйте `readonly struct`** для неизменяемых данных.
3. **Избегайте боксинга** (преобразования в `object`).
4. **Переопределяйте `Equals` и `GetHashCode`** для сравнения.

---

## **9. Пример переопределения методов**
```csharp
public struct Point : IEquatable<Point>
{
    public int X, Y;

    public bool Equals(Point other) => X == other.X && Y == other.Y;
    public override bool Equals(object obj) => obj is Point p && Equals(p);
    public override int GetHashCode() => HashCode.Combine(X, Y);
}

var p1 = new Point { X = 1, Y = 2 };
var p2 = new Point { X = 1, Y = 2 };
Console.WriteLine(p1.Equals(p2)); // True
```

---

## **10. Итог**
- **Структуры** — легковесные типы значений.
- **Используются** для координат, цветов, других простых данных.
- **Отличаются от классов** семантикой копирования и хранением в стеке.
- **Оптимизации**: `readonly struct`, `ref struct`.

**Пример итоговой структуры:**
```csharp
public readonly struct Angle
{
    public double Radians { get; }
    public double Degrees => Radians * (180 / Math.PI);

    public Angle(double radians) => Radians = radians;
}

var angle = new Angle(Math.PI / 2);
Console.WriteLine(angle.Degrees); // 90
```

# **41. Подключение пространств имен по умолчанию в C#**

Начиная с **C# 10**, в проектах можно использовать **глобальные пространства имен (global usings)**, которые автоматически подключаются во всех файлах без явного указания `using`. Это сокращает boilerplate-код.

---

## **1. Глобальные пространства имен (`global using`)**
Позволяют один раз подключить пространство имён для всего проекта.

### **1.1. Как объявить?**
Добавьте в любой `.cs`-файл (обычно в `Program.cs` или отдельный `GlobalUsings.cs`):
```csharp
global using System;
global using System.Collections.Generic;
global using static System.Math; // Можно использовать static-классы
```

### **1.2. Где размещать?**
- **Один файл `GlobalUsings.cs`** (рекомендуется):
  ```csharp
  // GlobalUsings.cs
  global using System;
  global using System.Linq;
  ```
- **Прямо в `Program.cs`** (для небольших проектов).

---

## **2. Пространства имен по умолчанию в .NET 6+**
В **.NET 6+** с шаблоном консольного приложения уже включены часто используемые `global using`:
- `System`
- `System.IO`
- `System.Collections.Generic`
- `System.Linq`
- `System.Net.Http`
- `System.Threading`
- `System.Threading.Tasks`

Проверить можно в `.csproj`:
```xml
<ImplicitUsings>enable</ImplicitUsings>
```

---

## **3. Как отключить implicit usings?**
Если они мешают, измените `.csproj`:
```xml
<PropertyGroup>
    <ImplicitUsings>disable</ImplicitUsings>
</PropertyGroup>
```

---

## **4. Какие пространства включаются по умолчанию?**
Зависит от типа проекта:

| **Тип проекта**       | **Добавляемые `global using`**                          |
|-----------------------|--------------------------------------------------------|
| Консольное приложение | `System`, `System.IO`, `System.Linq` и др. (см. выше)  |
| Веб-API (ASP.NET)     | + `Microsoft.AspNetCore.Mvc`                           |
| Тесты (xUnit/NUnit)   | + `Xunit` / `NUnit.Framework`                          |

Полный список можно посмотреть в SDK:  
[Исходный код ImplicitUsings](https://github.com/dotnet/sdk/blob/main/src/Templates/Microsoft.DotNet.Common.ProjectTemplates/content/ConsoleApplication-CSharp/Company.ConsoleApplication1.csproj)

---

## **5. Примеры**
### **5.1. Без `global using` (старый стиль)**
```csharp
using System;
using System.Linq;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello");
    }
}
```

### **5.2. С `global using` (новый стиль)**
```csharp
// GlobalUsings.cs
global using System;
global using System.Linq;

// Program.cs
Console.WriteLine("Hello"); // System уже подключен
```

### **5.3. С `ImplicitUsings` (в .NET 6+)**
```csharp
// Ничего не подключаем явно
Console.WriteLine("Hello"); // Работает!
var list = new List<string>(); // System.Collections.Generic подключен автоматически
```

---

## **6. Лучшие практики**
✅ **Используйте `global using` для:**
- Часто используемых пространств (`System`, `System.Linq`).
- Собственных библиотек (например, `global using MyApp.Models`).

❌ **Не используйте для:**
- Редко используемых пространств (чтобы не засорять область видимости).
- Пространств с конфликтующими именами (например, `MyLib.System`).

---

## **7. Как добавить свои `global using`?**
1. Создайте файл `GlobalUsings.cs` в проекте.
2. Перечислите нужные пространства:
   ```csharp
   global using MyApp.Core;
   global using static System.Math;
   ```

---

## **8. Итог**
- **`global using`** — подключает пространства для всего проекта.
- **`ImplicitUsings`** — автоматически добавляет стандартные пространства в .NET 6+.
- **Отключается** через `<ImplicitUsings>disable</ImplicitUsings>`.

**Пример `.csproj` с включенными implicit usings:**
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>
</Project>
```

# **46. Константы, поля и структуры для чтения в C#**

В C# существует несколько способов объявления неизменяемых данных: константы (`const`), поля для чтения (`readonly`) и структуры для чтения (`readonly struct`). Каждый из них имеет свои особенности и применяется в разных сценариях.

---

## **1. Константы (`const`)**
Константы — это **неизменяемые значения**, которые вычисляются во время компиляции и встраиваются в код.

### **Особенности:**
- Должны быть инициализированы при объявлении.
- Могут быть только примитивными типами (`int`, `string`, `double`, `bool` и т. д.) или перечислениями (`enum`).
- Нельзя использовать с пользовательскими типами (классами, структурами).

### **Пример:**
```csharp
public class MathConstants
{
    public const double Pi = 3.14159;
    public const string AppName = "MyCalculator";
}

// Использование
double circumference = 2 * MathConstants.Pi * radius;
```

### **Когда использовать?**
✅ Для значений, которые точно не изменятся (математические константы, названия приложений).

---

## **2. Поля для чтения (`readonly`)**
Поля `readonly` можно инициализировать **один раз** — либо при объявлении, либо в конструкторе класса.

### **Особенности:**
- Могут быть любого типа (включая классы и структуры).
- Инициализируются в runtime (а не во время компиляции, как `const`).
- Можно использовать с `static` (тогда инициализируется в статическом конструкторе).

### **Пример:**
```csharp
public class AppSettings
{
    public readonly string DatabaseConnectionString;

    public AppSettings(string connectionString)
    {
        DatabaseConnectionString = connectionString; // Можно задать только в конструкторе
    }
}

// Использование
var settings = new AppSettings("Server=localhost;Database=MyDB");
Console.WriteLine(settings.DatabaseConnectionString);
```

### **Когда использовать?**
✅ Для данных, которые не должны меняться после инициализации (настройки, конфигурации).

---

## **3. Структуры для чтения (`readonly struct`)**
`readonly struct` — это структура, все поля которой автоматически становятся `readonly`.

### **Особенности:**
- Все поля должны быть `readonly` (или свойства без сеттера).
- Гарантирует, что структура **неизменяема** (immutable).
- Оптимизирует работу компилятора (меньше копирований).

### **Пример:**
```csharp
public readonly struct Point
{
    public readonly int X;
    public readonly int Y;

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    // Методы могут быть, но не изменяют состояние
    public double DistanceToOrigin() => Math.Sqrt(X * X + Y * Y);
}

// Использование
var point = new Point(3, 4);
Console.WriteLine(point.DistanceToOrigin()); // 5
```

### **Когда использовать?**
✅ Для легковесных **неизменяемых** данных (координаты, векторы, цвета).

---

## **4. Сравнение `const`, `readonly` и `readonly struct`**
| Характеристика          | `const`                     | `readonly` (поле)         | `readonly struct`         |
|-------------------------|-----------------------------|---------------------------|---------------------------|
| **Когда вычисляется?**  | Во время компиляции         | Во время выполнения       | Во время выполнения       |
| **Типы данных**         | Примитивы, `enum`, `string` | Любые                     | Любые (но все поля `readonly`) |
| **Изменяемость**        | Неизменяем                  | Можно задать в конструкторе | Неизменяема               |
| **Использование**       | Глобальные константы         | Настройки, конфигурации   | Неизменяемые структуры    |

---

## **5. Best Practices**
1. **`const`** — для **математических констант**, **строк-идентификаторов**.
2. **`readonly`** — для **конфигураций**, которые задаются один раз при старте программы.
3. **`readonly struct`** — для **неизменяемых DTO** (Data Transfer Objects), **координат**, **векторов**.
4. **Избегайте** изменяемых структур — они могут привести к неочевидным ошибкам.

---

## **6. Примеры использования**
### **6.1. `const` для глобальных настроек**
```csharp
public static class AppConfig
{
    public const int MaxRetryAttempts = 3;
    public const string LogFilePath = "app.log";
}
```

### **6.2. `readonly` для зависимостей**
```csharp
public class UserService
{
    private readonly IUserRepository _repository;

    public UserService(IUserRepository repository)
    {
        _repository = repository; // Задаётся один раз и не меняется
    }
}
```

### **6.3. `readonly struct` для геометрии**
```csharp
public readonly struct Rectangle
{
    public readonly double Width;
    public readonly double Height;

    public Rectangle(double width, double height)
    {
        Width = width;
        Height = height;
    }

    public double Area => Width * Height;
}
```

---

## **7. Итог**
- **`const`** — для **значений, известных на этапе компиляции**.
- **`readonly`** — для **полей, которые нельзя менять после инициализации**.
- **`readonly struct`** — для **неизменяемых структур данных**.

**Пример итогового кода:**
```csharp
// Константа
public const string AppName = "MyApp";

// Readonly поле
public readonly string ConnectionString;

// Readonly структура
public readonly struct Vector2D
{
    public readonly double X, Y;
    public Vector2D(double x, double y) => (X, Y) = (x, y);
    public double Magnitude => Math.Sqrt(X * X + Y * Y);
}
```

# **47. Null и типы данных в C#**

В C# работа с `null` зависит от типа данных:
- **Ссылочные типы (reference types)** могут быть `null` (например, `string`, `class`).
- **Значимые типы (value types)** обычно не могут быть `null` (например, `int`, `struct`), но есть исключения.

---

## **1. Null и ссылочные типы**
### **1.1. Обычные ссылочные типы**
По умолчанию ссылочные типы (`class`, `string`, массивы) могут принимать значение `null`:
```csharp
string name = null; // OK
Person person = null; // OK, если Person — класс
```

### **1.2. Nullable Reference Types (NRT, C# 8.0+)**
В современных проектах можно включить **строгую проверку на `null`** для ссылочных типов:
1. Активируется в `.csproj`:
   ```xml
   <Nullable>enable</Nullable>
   ```
2. Теперь компилятор выдаёт предупреждения:
   ```csharp
   string name = null; // Warning: "Cannot convert null to non-nullable reference type"
   ```

**Как исправить?**
- Явно указать, что переменная может быть `null`:
  ```csharp
   string? nullableName = null; // OK
   ```
- Проверять перед использованием:
  ```csharp
  if (nullableName != null)
  {
      Console.WriteLine(nullableName.Length);
  }
  ```

---

## **2. Null и значимые типы**
### **2.1. Обычные значимые типы**
Значимые типы (`int`, `double`, `struct`) **не могут быть `null`**:
```csharp
int age = null; // Ошибка!
```

### **2.2. Nullable Value Types (C# 2.0+)**
Чтобы разрешить `null` для значимых типов, используется `Nullable<T>` или краткий синтаксис с `?`:
```csharp
int? nullableAge = null; // Эквивалентно Nullable<int>
DateTime? date = null;
```

**Проверка на `null`:**
```csharp
if (nullableAge.HasValue)
{
    Console.WriteLine($"Age: {nullableAge.Value}");
}
```

**Синтаксис с `??` (null-coalescing operator):**
```csharp
int actualAge = nullableAge ?? 0; // Если null, вернёт 0
```

---

## **3. Операторы для работы с `null`**
### **3.1. Оператор `?.` (null-conditional)**
Позволяет безопасно обращаться к членам объекта:
```csharp
Person? person = null;
int? age = person?.Age; // age = null (без исключения)
```

### **3.2. Оператор `??` (null-coalescing)**
Задаёт значение по умолчанию:
```csharp
string name = nullableName ?? "Unknown";
```

### **3.3. Оператор `??=` (C# 8.0+)**
Присваивает значение, только если переменная `null`:
```csharp
nullableName ??= "Default";
```

---

## **4. Проверка на null в современных версиях C#**
### **4.1. `is null` vs `== null`**
- `is null` работает всегда (даже если перегружен `==`).
- `== null` может быть переопределён в классе.

```csharp
if (person is null) { ... } // Предпочтительный способ
```

### **4.2. `is not null`**
```csharp
if (person is not null) { ... }
```

---

## **5. Примеры**
### **5.1. Безопасное обращение к свойствам**
```csharp
Person? person = GetPerson();
string? city = person?.Address?.City ?? "Unknown";
```

### **5.2. Обработка nullable-числа**
```csharp
int? count = GetCount();
int actualCount = count ?? -1;
```

### **5.3. Проверка в switch**
```csharp
switch (obj)
{
    case null:
        Console.WriteLine("Null");
        break;
    case int i:
        Console.WriteLine($"Number: {i}");
        break;
}
```

---

## **6. Best Practices**
✅ **Для ссылочных типов:**
- Включайте `<Nullable>enable</Nullable>`.
- Используйте `string?` для nullable-строк.
- Проверяйте `null` перед использованием (`is null`, `?.`).

✅ **Для значимых типов:**
- Используйте `int?`, если `null` допустим.
- Применяйте `??` для значений по умолчанию.

❌ **Избегайте:**
- Перегрузки `==` для своих типов (может сломать логику проверки на `null`).
- Использования `null` без необходимости (лучше `Option<T>` в функциональном стиле).

---

## **7. Итог**
- **Ссылочные типы** могут быть `null` (включайте NRT для безопасности).
- **Значимые типы** требуют `Nullable<T>` (`int?`) для поддержки `null`.
- **Операторы `?.`, `??`, `is null`** упрощают работу с `null`.

**Пример итогового кода:**
```csharp
#nullable enable

public class Person
{
    public string Name { get; } // Не может быть null (NRT)
    public string? Address { get; } // Может быть null
}

Person? person = FindPerson();
string city = person?.Address ?? "No address";
```

# **48. Конструкция `try..catch..finally` в C#**

Конструкция `try..catch..finally` используется для обработки исключений в C#. Она позволяет:
1. **Попытаться выполнить код** (`try`).
2. **Перехватить исключение**, если оно возникло (`catch`).
3. **Выполнить обязательный код** (например, освобождение ресурсов) независимо от исключений (`finally`).

---

## **1. Базовый синтаксис**
```csharp
try
{
    // Код, который может вызвать исключение
    File.ReadAllText("nonexistent.txt");
}
catch (FileNotFoundException ex)
{
    // Обработка конкретного исключения
    Console.WriteLine($"Файл не найден: {ex.Message}");
}
catch (Exception ex)
{
    // Общая обработка всех остальных исключений
    Console.WriteLine($"Произошла ошибка: {ex.Message}");
}
finally
{
    // Код, который выполнится в любом случае
    Console.WriteLine("Завершение обработки файла");
}
```

---

## **2. Блок `try`**
- Содержит код, который может вызвать исключение.
- Если исключение происходит, выполнение блока `try` прерывается, и управление передаётся в `catch`.

---

## **3. Блок `catch`**
Перехватывает исключения. Может быть:
- **Конкретным** (ловит исключения определённого типа, например `FileNotFoundException`).
- **Общим** (ловит все исключения через `catch (Exception ex)`).

### **3.1. Фильтрация исключений (C# 6.0+)**
Можно добавить условие через `when`:
```csharp
catch (HttpRequestException ex) when (ex.StatusCode == 404)
{
    Console.WriteLine("Страница не найдена (404)");
}
```

### **3.2. Игнорирование исключения**
Если исключение не нужно обрабатывать, можно просто перехватить:
```csharp
catch (Exception) { } // Не рекомендуется без логирования!
```

---

## **4. Блок `finally`**
- Выполняется **всегда**, даже если:
  - В `try` было исключение.
  - В `catch` было новое исключение.
  - Был выполнен `return` в `try` или `catch`.
- Используется для освобождения ресурсов (закрытие файлов, соединений с БД).

### **Пример с `finally` для закрытия файла**
```csharp
FileStream? file = null;
try
{
    file = File.Open("data.txt", FileMode.Open);
    // Работа с файлом...
}
catch (IOException ex)
{
    Console.WriteLine($"Ошибка ввода-вывода: {ex.Message}");
}
finally
{
    file?.Close(); // Закрываем файл в любом случае
}
```

### **Альтернатива: `using`**
Для объектов, реализующих `IDisposable` (например, файлы, соединения), лучше использовать `using`:
```csharp
using (var file = File.Open("data.txt", FileMode.Open))
{
    // Файл закроется автоматически после выхода из блока
}
```

---

## **5. Вложенные `try..catch`**
Можно комбинировать несколько блоков:
```csharp
try
{
    try
    {
        // Код, который может вызвать исключение
    }
    catch (FormatException ex)
    {
        Console.WriteLine("Ошибка формата");
    }
}
catch (Exception ex)
{
    Console.WriteLine("Общая ошибка");
}
```

---

## **6. Создание своих исключений**
Можно выбрасывать исключения через `throw`:
```csharp
if (age < 0)
{
    throw new ArgumentException("Возраст не может быть отрицательным");
}
```

### **Кастомные исключения**
```csharp
public class InvalidOrderException : Exception
{
    public InvalidOrderException(string message) : base(message) { }
}

throw new InvalidOrderException("Недопустимый заказ");
```

---

## **7. Best Practices**
✅ **Рекомендуется:**
- Ловить **конкретные исключения**, а не просто `Exception`.
- Использовать `finally` или `using` для освобождения ресурсов.
- Логировать исключения (например, через `ILogger`).

❌ **Не рекомендуется:**
- Пустые блоки `catch` (скрывают ошибки).
- Ловить исключения, которые не можешь обработать.

---

## **8. Пример: обработка деления на ноль**
```csharp
try
{
    int a = 10;
    int b = 0;
    int result = a / b; // DivideByZeroException
}
catch (DivideByZeroException ex)
{
    Console.WriteLine("Деление на ноль запрещено!");
}
finally
{
    Console.WriteLine("Вычисление завершено");
}
```

---

## **9. Итог**
- `try` — код, который может вызвать исключение.
- `catch` — обработка исключений (можно несколько блоков).
- `finally` — код, который выполнится в любом случае.
- `throw` — генерация исключений.

**Пример итогового кода:**
```csharp
try
{
    var data = File.ReadAllText("config.json");
    Console.WriteLine(data);
}
catch (FileNotFoundException)
{
    Console.WriteLine("Файл не найден!");
}
catch (Exception ex)
{
    Console.WriteLine($"Неизвестная ошибка: {ex.Message}");
}
finally
{
    Console.WriteLine("Программа завершена");
}
```

# **49. Блок `catch` и фильтры исключений в C#**

Блок `catch` в конструкции `try-catch-finally` предназначен для перехвата и обработки исключений. В C# есть несколько способов фильтрации исключений, включая:
1. Перехват по типу исключения
2. Фильтры исключений (с C# 6.0)
3. Несколько блоков `catch` с разными типами исключений

---

## **1. Базовый синтаксис блока `catch`**

```csharp
try
{
    // Код, который может вызвать исключение
}
catch (SpecificException ex)
{
    // Обработка конкретного типа исключения
}
catch (Exception ex)
{
    // Общая обработка всех остальных исключений
}
```

---

## **2. Фильтры исключений (when)**

С C# 6.0 можно использовать условие `when` для дополнительной фильтрации исключений:

```csharp
try
{
    // Код, который может вызвать исключение
}
catch (HttpRequestException ex) when (ex.StatusCode == 404)
{
    Console.WriteLine("Страница не найдена (404)");
}
catch (HttpRequestException ex) when (ex.StatusCode == 500)
{
    Console.WriteLine("Ошибка сервера (500)");
}
```

### **Особенности фильтров:**
- Условие `when` вычисляется **после** перехвата исключения
- Если условие `when` не выполняется, исключение продолжает "всплывать" вверх по стеку
- Не влияет на стек вызовов (в отличие от проверки условия в теле `catch`)

---

## **3. Разница между фильтрами и проверкой в теле catch**

### **3.1. С фильтром (when)**
```csharp
catch (HttpRequestException ex) when (ex.StatusCode == 404)
{
    // Этот блок не изменит стек вызовов
}
```

### **3.2. С проверкой в теле catch**
```csharp
catch (HttpRequestException ex)
{
    if (ex.StatusCode == 404)
    {
        // Этот блок изменит стек вызовов
    }
    else
    {
        throw; // Повторный выброс исключения
    }
}
```

**Ключевое отличие:** фильтры `when` не изменяют стек вызовов, а повторный `throw` - изменяет.

---

## **4. Примеры использования фильтров**

### **4.1. Фильтрация по свойству исключения**
```csharp
try
{
    // Вызов API
}
catch (HttpRequestException ex) when (ex.Message.Contains("timeout"))
{
    Console.WriteLine("Таймаут соединения");
}
```

### **4.2. Фильтрация по внешнему условию**
```csharp
bool shouldLog = true;

try
{
    // Код с возможным исключением
}
catch (Exception ex) when (shouldLog)
{
    Logger.Log(ex);
    throw;
}
```

### **4.3. Комбинация нескольких фильтров**
```csharp
try
{
    // Код
}
catch (IOException ex) when (ex is FileNotFoundException || ex is DirectoryNotFoundException)
{
    Console.WriteLine("Файл или директория не найдены");
}
```

---

## **5. Особенности работы фильтров**

1. **Порядок имеет значение** - обработчики проверяются сверху вниз:
   ```csharp
   catch (Exception ex) { } // Этот блок перехватит ВСЕ исключения
   catch (InvalidOperationException ex) { } // Этот блок никогда не выполнится!
   ```

2. **Фильтры могут вызывать методы** (но осторожно!):
   ```csharp
   catch (Exception ex) when (IsCritical(ex))
   {
       // Обработка только критических ошибок
   }
   ```

3. **Фильтры не ловят исключения из своих условий**:
   ```csharp
   catch (Exception ex) when (CheckCondition(ex)) // Если CheckCondition выбросит исключение - оно НЕ будет поймано
   {
   }
   ```

---

## **6. Best Practices**

✅ **Рекомендуется:**
- Использовать конкретные типы исключений вместо общего `Exception`
- Применять фильтры `when` для сложных условий
- Сохранять порядок от конкретных к общим типам исключений

❌ **Не рекомендуется:**
- Делать сложную логику в условиях `when`
- Использовать фильтры для контроля потока выполнения
- Игнорировать исключения (пустые блоки `catch`)

---

## **7. Пример: обработка разных ошибок API**

```csharp
try
{
    var response = await httpClient.GetAsync("api/data");
    response.EnsureSuccessStatusCode();
}
catch (HttpRequestException ex) when (ex.StatusCode == HttpStatusCode.NotFound)
{
    Console.WriteLine("Ресурс не найден");
}
catch (HttpRequestException ex) when (ex.StatusCode == HttpStatusCode.Unauthorized)
{
    Console.WriteLine("Требуется авторизация");
    await Reauthenticate();
}
catch (HttpRequestException ex) when (ex.Message.Contains("timeout"))
{
    Console.WriteLine("Таймаут запроса");
    await Task.Delay(1000);
    Retry();
}
catch (Exception ex)
{
    Console.WriteLine($"Неизвестная ошибка: {ex.Message}");
    throw;
}
```

---

## **8. Итог**

1. Блок `catch` может фильтровать исключения:
   - По типу (`catch (IOException)`)
   - По условию (`when`)

2. Фильтры `when`:
   - Появились в C# 6.0
   - Не изменяют стек вызовов
   - Могут использовать любые логические условия

3. Порядок обработчиков важен - от конкретных к общим

4. Фильтры исключений делают код чище и точнее обрабатывают ошибки

# **50. Типы исключений и класс Exception в C#**

Исключения в C# представлены иерархией классов, где базовым является класс `System.Exception`. Все исключения наследуются от него, что позволяет создавать универсальные обработчики или специфичные для конкретных ошибок.

---

## **1. Иерархия исключений**
```
System.Object
    └── System.Exception (базовый класс для всех исключений)
        ├── System.SystemException (стандартные системные исключения)
        │   ├── System.IndexOutOfRangeException
        │   ├── System.NullReferenceException
        │   ├── System.InvalidOperationException
        │   ├── System.ArgumentException
        │   │   └── System.ArgumentNullException
        │   │   └── System.ArgumentOutOfRangeException
        │   └── ...
        └── System.ApplicationException (пользовательские исключения)
```

---

## **2. Основные типы исключений**

### **2.1. SystemException (системные исключения)**
Генерируются CLR (Common Language Runtime) при ошибках выполнения:

| Исключение                       | Описание                                                                 |
|----------------------------------|--------------------------------------------------------------------------|
| `NullReferenceException`         | Попытка доступа к члену объекта, который равен `null`                    |
| `IndexOutOfRangeException`       | Выход за границы массива или коллекции                                   |
| `InvalidCastException`           | Неправильное приведение типов                                            |
| `DivideByZeroException`          | Деление на ноль                                                          |
| `OutOfMemoryException`           | Недостаточно памяти                                                      |
| `StackOverflowException`         | Переполнение стека (обычно из-за бесконечной рекурсии)                   |

**Пример:**
```csharp
string text = null;
Console.WriteLine(text.Length); // NullReferenceException
```

### **2.2. ApplicationException (пользовательские исключения)**
Рекомендуется создавать свои классы исключений, наследуясь от `Exception` (не от `ApplicationException`, так как это устаревший подход).

**Пример кастомного исключения:**
```csharp
public class InvalidOrderException : Exception
{
    public InvalidOrderException(string message) : base(message) { }
}
```

---

## **3. Класс Exception: основные члены**
Класс `Exception` содержит полезные свойства для диагностики ошибок:

| Свойство/Метод          | Описание                                                                 |
|-------------------------|--------------------------------------------------------------------------|
| `Message`               | Сообщение об ошибке                                                     |
| `StackTrace`            | Стек вызовов на момент возникновения исключения                         |
| `InnerException`        | Вложенное исключение (если текущее было вызвано другим исключением)      |
| `HelpLink`              | Ссылка на справку по ошибке                                             |
| `Data`                  | Словарь с дополнительными пользовательскими данными (ключ-значение)      |
| `ToString()`            | Полное описание исключения (включая стек вызовов)                        |

**Пример использования:**
```csharp
try
{
    // Код, который может вызвать исключение
}
catch (Exception ex)
{
    Console.WriteLine($"Ошибка: {ex.Message}");
    Console.WriteLine($"Стек вызовов: {ex.StackTrace}");
    if (ex.InnerException != null)
    {
        Console.WriteLine($"Внутреннее исключение: {ex.InnerException.Message}");
    }
}
```

---

## **4. Создание своих исключений**
Рекомендуется наследоваться от `Exception` и реализовать стандартные конструкторы:

```csharp
public class PaymentFailedException : Exception
{
    public decimal Amount { get; }

    // Конструкторы
    public PaymentFailedException(string message, decimal amount) : base(message)
    {
        Amount = amount;
    }

    public PaymentFailedException(string message, decimal amount, Exception inner) 
        : base(message, inner)
    {
        Amount = amount;
    }
}
```

**Использование:**
```csharp
try
{
    ProcessPayment(amount);
}
catch (PaymentFailedException ex)
{
    Console.WriteLine($"Платеж на {ex.Amount} не прошел: {ex.Message}");
}
```

---

## **5. Best Practices**

✅ **Рекомендуется:**
- Использовать конкретные типы исключений (`FileNotFoundException` вместо общего `Exception`).
- Создавать свои исключения для доменных ошибок.
- Включать полезную информацию в `Message` и `Data`.
- Логировать исключения (например, через `ILogger`).

❌ **Не рекомендуется:**
- Использовать исключения для контроля потока выполнения (это антипаттерн).
- Создавать пустые блоки `catch` без обработки.
- Наследоваться от `ApplicationException` (устаревший подход).

---

## **6. Пример: обработка разных исключений**
```csharp
try
{
    var data = File.ReadAllText("config.json");
    var settings = JsonSerializer.Deserialize<Settings>(data);
}
catch (FileNotFoundException ex)
{
    Console.WriteLine("Файл конфигурации не найден");
}
catch (JsonException ex)
{
    Console.WriteLine($"Ошибка формата JSON: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"Неизвестная ошибка: {ex.Message}");
    throw; // Повторно выбрасываем для логирования в верхних слоях
}
```

---

## **7. Итог**
1. Все исключения наследуются от `System.Exception`.
2. **Системные исключения** (`SystemException`) возникают при ошибках выполнения.
3. **Пользовательские исключения** следует создавать от `Exception`.
4. Класс `Exception` содержит полезные свойства (`Message`, `StackTrace` и др.).
5. Фильтруйте исключения по конкретным типам в блоках `catch`.

# **51. Генерация исключений и оператор `throw` в C#**

Оператор `throw` используется для явной генерации исключений в коде. Это ключевой механизм обработки ошибок, позволяющий:
1. Прервать нормальное выполнение программы
2. Сигнализировать о нештатной ситуации
3. Передать информацию об ошибке вверх по стеку вызовов

---

## **1. Базовый синтаксис**

```csharp
throw new Exception("Сообщение об ошибке");
```

---

## **2. Основные способы генерации исключений**

### **2.1. Генерация нового исключения**
Создание и выброс нового экземпляра исключения:

```csharp
if (age < 0)
{
    throw new ArgumentOutOfRangeException(nameof(age), "Возраст не может быть отрицательным");
}
```

### **2.2. Повторный выброс пойманного исключения**
Используется, когда нужно:
- Залогировать исключение
- Частично обработать ошибку
- Передать исключение выше по стеку

```csharp
try
{
    // Код, который может вызвать исключение
}
catch (IOException ex)
{
    Logger.LogError(ex);
    throw;  // Сохраняет оригинальный стек вызовов
}
```

⚠️ **Важно:** `throw ex;` перезаписывает стек вызовов (не рекомендуется)!

---

## **3. Создание пользовательских исключений**

Рекомендуется наследоваться от `Exception`:

```csharp
public class InsufficientFundsException : Exception
{
    public decimal CurrentBalance { get; }
    public decimal RequiredAmount { get; }

    public InsufficientFundsException(decimal current, decimal required)
        : base($"Недостаточно средств. Текущий баланс: {current}, требуется: {required}")
    {
        CurrentBalance = current;
        RequiredAmount = required;
    }
}

// Использование
if (balance < amount)
{
    throw new InsufficientFundsException(balance, amount);
}
```

---

## **4. Когда использовать throw?**

✅ **Правильные случаи:**
- Невозможность выполнить операцию (неверные аргументы, состояние системы)
- Нарушение бизнес-правил (отказ платежа, недостаток прав)
- Ошибки в работе с внешними ресурсами (файлы, БД, API)

❌ **Когда не стоит использовать:**
- Для обычного контроля потока выполнения (это антипаттерн)
- Вместо возврата кодов ошибок (в высокопроизводительных сценариях)

---

## **5. Особенности работы throw**

### **5.1. Выражения throw (C# 7.0+)**
Можно использовать в выражениях:

```csharp
var config = LoadConfig() ?? throw new InvalidOperationException("Конфигурация не загружена");
```

### **5.2. Throw в тернарном операторе**
```csharp
var result = isValid 
    ? Calculate() 
    : throw new ArgumentException("Неверные входные данные");
```

### **5.3. Throw в лямбда-выражениях**
```csharp
var processor = input => input != null 
    ? Process(input) 
    : throw new ArgumentNullException(nameof(input));
```

---

## **6. Best Practices**

1. **Конкретные типы исключений**  
   Используйте наиболее подходящие стандартные или свои исключения.

2. **Информативные сообщения**  
   В сообщении должна быть четкая диагностическая информация:
   ```csharp
   // Плохо:
   throw new Exception("Ошибка");
   
   // Хорошо:
   throw new FileNotFoundException($"Файл {path} не найден");
   ```

3. **Сохранение стека вызовов**  
   Всегда используйте `throw;` вместо `throw ex;` при повторном выбросе.

4. **Добавляйте контекст**  
   Используйте `InnerException` и `Data` для дополнительной информации:
   ```csharp
   throw new ApplicationException("Ошибка обработки", ex);
   ```

5. **Документируйте исключения**  
   Указывайте в XML-документации, какие исключения может выбрасывать метод:
   ```csharp
   /// <exception cref="ArgumentNullException">Если input равен null</exception>
   public void Process(string input)
   {
       if (input == null)
           throw new ArgumentNullException(nameof(input));
       // ...
   }
   ```

---

## **7. Примеры**

### **7.1. Валидация аргументов**
```csharp
public void SetAge(int age)
{
    if (age < 0)
        throw new ArgumentOutOfRangeException(nameof(age), "Возраст не может быть отрицательным");
    
    if (age > 150)
        throw new ArgumentOutOfRangeException(nameof(age), "Недопустимый возраст");
    
    this.age = age;
}
```

### **7.2. Обработка с повторным выбросом**
```csharp
public string ReadConfigFile(string path)
{
    try
    {
        return File.ReadAllText(path);
    }
    catch (IOException ex)
    {
        Logger.LogError($"Ошибка чтения файла {path}", ex);
        throw;  // Передаем исключение дальше
    }
}
```

### **7.3. Бизнес-правило**
```csharp
public void Withdraw(decimal amount)
{
    if (amount <= 0)
        throw new ArgumentException("Сумма должна быть положительной", nameof(amount));
    
    if (amount > Balance)
        throw new InsufficientFundsException(Balance, amount);
    
    Balance -= amount;
}
```

---

## **8. Итог**
1. `throw` — основной механизм генерации исключений
2. Всегда используйте наиболее конкретный тип исключения
3. Сохраняйте стек вызовов при повторном выбросе (`throw;`)
4. Создавайте информативные пользовательские исключения
5. Документируйте возможные исключения в методах

**Итоговый пример:**
```csharp
public class ApiClient
{
    public string GetData(string endpoint)
    {
        if (string.IsNullOrWhiteSpace(endpoint))
            throw new ArgumentException("Endpoint не может быть пустым", nameof(endpoint));
        
        try
        {
            // Вызов API
        }
        catch (HttpRequestException ex)
        {
            throw new ApplicationException($"Ошибка при вызове {endpoint}", ex);
        }
    }
}
```
# **52. Создание классов исключений в C#**

Собственные классы исключений позволяют точно описывать специфичные ошибки вашей предметной области. Они наследуются от базового класса `System.Exception` или его производных.

---

## **1. Базовые правила создания**

1. **Наследование**  
   Все пользовательские исключения должны наследоваться от `Exception` или его потомков.

2. **Стандартные конструкторы**  
   Рекомендуется реализовать 4 стандартных конструктора:
   - Без параметров
   - С сообщением об ошибке
   - С сообщением и внутренним исключением
   - Для сериализации

3. **Смысловые названия**  
   Имена классов должны заканчиваться на `Exception` и четко описывать ошибку.

---

## **2. Шаблон пользовательского исключения**

```csharp
[Serializable]
public class CustomApplicationException : Exception
{
    // Конструкторы
    
    public CustomApplicationException() { }
    
    public CustomApplicationException(string message) 
        : base(message) { }
    
    public CustomApplicationException(string message, Exception inner) 
        : base(message, inner) { }
    
    protected CustomApplicationException(
        SerializationInfo info,
        StreamingContext context) : base(info, context) { }
}
```

---

## **3. Примеры специализированных исключений**

### **3.1. Исключение для бизнес-логики**
```csharp
public class InsufficientFundsException : Exception
{
    public decimal CurrentBalance { get; }
    public decimal RequiredAmount { get; }

    public InsufficientFundsException(decimal current, decimal required)
        : base($"Недостаточно средств. Текущий баланс: {current}, требуется: {required}")
    {
        CurrentBalance = current;
        RequiredAmount = required;
    }
}
```

### **3.2. Исключение для валидации**
```csharp
public class InvalidEntityStateException : Exception
{
    public string EntityType { get; }
    public IReadOnlyDictionary<string, string[]> Errors { get; }

    public InvalidEntityStateException(
        string entityType,
        Dictionary<string, string[]> errors)
        : base($"Некорректное состояние сущности {entityType}")
    {
        EntityType = entityType;
        Errors = errors;
    }
}
```

### **3.3. Исключение для работы с API**
```csharp
public class ApiRequestException : Exception
{
    public int StatusCode { get; }
    public string ResponseContent { get; }

    public ApiRequestException(
        int statusCode,
        string message,
        string responseContent) 
        : base($"API request failed with status {statusCode}: {message}")
    {
        StatusCode = statusCode;
        ResponseContent = responseContent;
    }
}
```

---

## **4. Рекомендации по проектированию**

1. **Добавляйте полезные свойства**  
   Включайте в исключение всю необходимую для диагностики информацию.

2. **Реализуйте сериализацию**  
   Если исключение может передаваться между доменами приложения.

3. **Переопределяйте ToString()**  
   Для удобного логирования:
   ```csharp
   public override string ToString()
   {
       return $"{base.ToString()}, CurrentBalance: {CurrentBalance}";
   }
   ```

4. **Используйте атрибут [Serializable]**  
   Если исключение может пересекать границы AppDomain.

---

## **5. Пример использования**

```csharp
public class PaymentService
{
    public void ProcessPayment(decimal amount)
    {
        if (amount <= 0)
            throw new InvalidPaymentAmountException(amount);
        
        if (!HasSufficientFunds(amount))
            throw new InsufficientFundsException(GetBalance(), amount);
        
        // Логика обработки платежа
    }
}

try
{
    paymentService.ProcessPayment(100);
}
catch (InsufficientFundsException ex)
{
    Console.WriteLine($"Ошибка: {ex.Message}");
    Console.WriteLine($"Доступно: {ex.CurrentBalance}, Требуется: {ex.RequiredAmount}");
}
```

---

## **6. Best Practices**

✅ **Рекомендуется:**
- Создавать отдельные классы для разных типов ошибок
- Включать контекст ошибки в свойства исключения
- Документировать исключения в XML-комментариях
- Наследоваться от наиболее подходящего базового исключения

❌ **Не рекомендуется:**
- Использовать общие исключения типа `ApplicationException`
- Создавать исключения без полезной диагностической информации
- Наследоваться от `SystemException` (зарезервировано для CLR)

---

## **7. Итог**

1. Пользовательские исключения улучшают читаемость кода
2. Должны содержать максимум полезной информации
3. Реализуйте стандартные конструкторы
4. Используйте специализированные исключения для разных сценариев ошибок

**Полный пример:**
```csharp
[Serializable]
public class DatabaseConnectionException : Exception
{
    public string Server { get; }
    public int Port { get; }
    public TimeSpan Timeout { get; }

    public DatabaseConnectionException(
        string server,
        int port,
        TimeSpan timeout,
        Exception inner)
        : base($"Не удалось подключиться к {server}:{port} за {timeout.TotalSeconds} сек", inner)
    {
        Server = server;
        Port = port;
        Timeout = timeout;
    }

    protected DatabaseConnectionException(
        SerializationInfo info,
        StreamingContext context) : base(info, context)
    {
        Server = info.GetString(nameof(Server));
        Port = info.GetInt32(nameof(Port));
        Timeout = TimeSpan.FromTicks(info.GetInt64(nameof(Timeout)));
    }

    public override void GetObjectData(
        SerializationInfo info,
        StreamingContext context)
    {
        base.GetObjectData(info, context);
        info.AddValue(nameof(Server), Server);
        info.AddValue(nameof(Port), Port);
        info.AddValue(nameof(Timeout), Timeout.Ticks);
    }
}
```

# **53. Поиск блока catch при обработке исключений в C#**

Когда в программе возникает исключение, среда выполнения .NET ищет подходящий блок `catch` для его обработки. Этот процесс происходит по определенным правилам.

---

## **1. Алгоритм поиска обработчика исключений**

1. **Исключение возникает** в блоке `try`
2. **Поиск идет снизу вверх** по стеку вызовов:
   - Сначала проверяется текущий метод
   - Затем методы, которые его вызвали
3. **В каждом меторе проверяются** блоки `catch`:
   - Сравнивается тип исключения с указанным в `catch`
   - Выбирается первый подходящий блок

---

## **2. Принцип соответствия типов**

Блок `catch` будет выбран, если:
- Тип исключения **точно совпадает** с указанным в `catch`
- Или тип исключения **является производным** от указанного

```csharp
try
{
    // Код, который может вызвать исключение
}
catch (FileNotFoundException ex)  // 1. Точное совпадение
{
    Console.WriteLine("Файл не найден");
}
catch (IOException ex)           // 2. Базовый класс для FileNotFoundException
{
    Console.WriteLine("Ошибка ввода-вывода");
}
catch (Exception ex)             // 3. Универсальный обработчик
{
    Console.WriteLine("Общая ошибка");
}
```

---

## **3. Порядок блоков catch имеет значение**

Блоки обрабатываются **сверху вниз**. Первый подходящий блок будет выполнен:

```csharp
try
{
    throw new FileNotFoundException();
}
catch (Exception ex)  // Этот блок перехватит ВСЕ исключения
{
    Console.WriteLine("Поймано в Exception");
}
catch (FileNotFoundException ex)  // Этот блок никогда не выполнится!
{
    Console.WriteLine("Поймано в FileNotFoundException");
}
```

**Правильный порядок:**
```csharp
catch (FileNotFoundException ex)  // Сначала специфичные
catch (IOException ex)           // Затем более общие
catch (Exception ex)             // В конце самый общий
```

---

## **4. Фильтры исключений (when)**

С C# 6.0 можно уточнять выбор блока `catch` с помощью условий:

```csharp
try
{
    // Код
}
catch (HttpRequestException ex) when (ex.StatusCode == 404)
{
    Console.WriteLine("Не найдено (404)");
}
catch (HttpRequestException ex) when (ex.StatusCode == 500)
{
    Console.WriteLine("Ошибка сервера (500)");
}
```

**Особенности:**
- Условие проверяется **после** сопоставления типа
- Если условие не выполняется, поиск продолжается

---

## **5. Поведение при отсутствии обработчика**

Если подходящий блок `catch` не найден:
1. Исключение "всплывает" вверх по стеку вызовов
2. Если обработчик так и не найден - программа аварийно завершается
3. В консольных приложениях показывается сообщение об ошибке
4. В GUI-приложениях обычно вызывается глобальный обработчик

---

## **6. Пример полного процесса обработки**

```csharp
void MethodA()
{
    try
    {
        MethodB();
    }
    catch (DivideByZeroException)
    {
        Console.WriteLine("Поймано в MethodA");
    }
}

void MethodB()
{
    try
    {
        MethodC();
    }
    catch (NullReferenceException)
    {
        Console.WriteLine("Поймано в MethodB");
    }
}

void MethodC()
{
    throw new DivideByZeroException();
}
```

**Что произойдет:**
1. Исключение возникает в `MethodC`
2. `MethodC` не имеет `try-catch` - исключение идет в `MethodB`
3. `MethodB` ловит только `NullReferenceException` - исключение идет в `MethodA`
4. `MethodA` успешно обрабатывает исключение

---

## **7. Best Practices**

✅ **Рекомендуется:**
- Располагать блоки `catch` от конкретных к общим
- Использовать фильтры `when` для сложных условий
- Логировать необработанные исключения
- Документировать возможные исключения методов

❌ **Не рекомендуется:**
- Использовать пустые блоки `catch`
- Ловить `Exception` без веской причины
- Подавлять исключения без логирования

---

## **8. Глобальная обработка исключений**

Для перехвата всех необработанных исключений:

**В консольном приложении:**
```csharp
AppDomain.CurrentDomain.UnhandledException += (s, e) => 
{
    Console.WriteLine($"Необработанное исключение: {e.ExceptionObject}");
    Environment.Exit(1);
};
```

**В WPF/WinForms:**
```csharp
Application.DispatcherUnhandledException += (s, e) => 
{
    MessageBox.Show($"Необработанное исключение: {e.Exception.Message}");
    e.Handled = true;
};
```

---

## **9. Итог**

1. Поиск обработчика идет **снизу вверх** по стеку вызовов
2. Блоки `catch` проверяются **сверху вниз**
3. **Фильтры** `when` позволяют уточнять условия
4. **Порядок блоков** `catch` критически важен
5. Всегда обрабатывайте исключения **на нужном уровне** абстракции

**Пример правильной обработки:**
```csharp
try
{
    ProcessFile("data.txt");
}
catch (FileNotFoundException ex)
{
    Console.WriteLine($"Файл не найден: {ex.FileName}");
}
catch (IOException ex) when (ex is DirectoryNotFoundException || 
                           ex is DriveNotFoundException)
{
    Console.WriteLine("Проблема с диском или директорией");
}
catch (Exception ex)
{
    Logger.LogError(ex);
    throw;
}
```

# **54. Замыкания (Closures) в C#**

Замыкание — это функция, которая запоминает и имеет доступ к переменным из внешней области видимости, даже после того, как эта область видимости завершила выполнение. В C# замыкания реализуются через лямбда-выражения и анонимные методы.

---

## **1. Как работают замыкания?**

Когда лямбда-выражение или анонимный метод захватывает переменную из внешней области видимости, компилятор C# создает **неявный класс**, который сохраняет состояние этой переменной.

### **Пример 1: Простое замыкание**
```csharp
Func<int, int> CreateMultiplier(int factor)
{
    // Лямбда-выражение захватывает 'factor' из внешней области
    return x => x * factor;
}

var multiplyBy5 = CreateMultiplier(5);
Console.WriteLine(multiplyBy5(10)); // 50 (10 * 5)
```

**Что происходит под капотом?**  
Компилятор генерирует скрытый класс, который хранит `factor`:

```csharp
class ClosureClass
{
    public int factor;
    public int Method(int x) => x * factor;
}
```

---

## **2. Захват переменных в цикле (важная особенность!)**

Если переменная изменяется в цикле, замыкание захватывает **ссылку на переменную**, а не её значение на момент создания.

### **Пример 2: Ошибка при захвате переменной цикла**
```csharp
var actions = new List<Action>();

for (int i = 0; i < 3; i++)
{
    actions.Add(() => Console.WriteLine(i));
}

foreach (var action in actions)
{
    action(); // Выведет 3, 3, 3 (а не 0, 1, 2!)
}
```

**Почему так происходит?**  
Все лямбды ссылаются на одну и ту же переменную `i`, которая к моменту вызова равна `3`.

### **Решение: создание локальной копии**
```csharp
for (int i = 0; i < 3; i++)
{
    int temp = i; // Каждая итерация создает новую переменную
    actions.Add(() => Console.WriteLine(temp));
}

// Теперь выведет 0, 1, 2
```

---

## **3. Захват изменяемых переменных**

Замыкания могут изменять захваченные переменные:

```csharp
int counter = 0;

Action increment = () => counter++;
increment();
increment();

Console.WriteLine(counter); // 2
```

---

## **4. Замыкания и время жизни объектов**

Захваченные переменные живут **до тех пор, пока существует замыкание**:

```csharp
Func<int> GetCounter()
{
    int count = 0;
    return () => ++count;
}

var counter = GetCounter();
Console.WriteLine(counter()); // 1
Console.WriteLine(counter()); // 2
```

**Почему `count` не уничтожается?**  
Компилятор перемещает `count` в объект-замыкание, который живет, пока существует `counter`.

---

## **5. Замыкания в многопоточности**

Будьте осторожны — захваченные переменные могут привести к состоянию гонки (race condition):

```csharp
int value = 0;
Parallel.For(0, 10, i => value++);
Console.WriteLine(value); // Может вывести меньше 10!
```

**Решение:** используйте `Interlocked` или локальные переменные.

---

## **6. Best Practices**

✅ **Рекомендуется:**
- Использовать замыкания для краткости и выразительности
- В циклах создавать локальные копии переменных
- Документировать сложные замыкания

❌ **Избегайте:**
- Захвата изменяемых переменных в многопоточном коде
- Слишком сложных замыканий (лучше вынести в метод)
- Захвата объектов с большим временем жизни без необходимости

---

## **7. Примеры использования**

### **Фильтрация списка**
```csharp
var threshold = 5;
var numbers = new List<int> { 1, 6, 3, 8 };
var filtered = numbers.Where(x => x > threshold); // Захватывает threshold
```

### **Отложенное выполнение**
```csharp
string message = "Hello";
Task.Run(() => Console.WriteLine(message)); // Захватывает message
```

---

## **8. Итог**

1. Замыкания — это функции, запоминающие внешние переменные
2. В C# реализуются через лямбды и анонимные методы
3. Захватывают **ссылку** на переменную, а не значение
4. Требуют осторожности в циклах и многопоточном коде
5. Компилятор создает скрытые классы для хранения состояния

**Пример замыкания с модификацией:**
```csharp
var generator = CreateGenerator(10);
Console.WriteLine(generator()); // 10
Console.WriteLine(generator()); // 11

Func<int> CreateGenerator(int start)
{
    int current = start;
    return () => current++;
}
```
