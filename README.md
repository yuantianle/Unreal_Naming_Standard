# Unreal Naming Standard
A collection of naming standard used in C++ for Unreal5.

## 1. Copyright

Any source file (.h, .cpp, .xaml) **provided by Epic Games** for public distribution must contain a copyright notice as the first line in the file. (Probably should add our copyright also)
``` c++
// Copyright Epic Games, Inc. All Rights Reserved.
```

## 2. Class (Type) Naming

### 2.0 Basic rule
- Class/Structure names use "Big Camel case" style. 
- There is no underscore between words.
- Name of class should be nouns. So do variables.
``` c++
class Animal;
struct BadApple;
```
- Special class will have a capital word at the front, ref below sections.

### 2.1 Interfaces
Classes that are abstract interfaces are prefixed by I.
``` c++
class IAnalyticsProvider
```

### 2.2 Template classes
Template classes are prefixed by T.
``` c++
class TAttribute
```

### 2.3 Enums calsses
Enums are prefixed by E.
``` c++
enum class EColorBits
{
    ECB_Red,
    ECB_Green,
    ECB_Blue
};
```

### 2.5 Fields(private, public, protect, internal), methods, constructors

### 2.4 No `Auto`
Avoid using `auto`. Always be explicit about the type you are initializing.
```c++
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    // Bad example
    for (auto num : numbers) 
    {
        std::cout << num << " ";
    }

    // Good example 1
    for (int num : numbers) 
    {
        std::cout << num << " ";
    }

    // Good example 2
    for (int i = 0; i <numbers.size(); i++)
    {
        std::cout << numbers[i] << " ";
    }

```


### 2.4 Special inherietance
- Classes that inherit from `UObject` are prefixed by U. 
    ```c++
    class UActorComponent
    ```
- Classes that inherit from `AActor` are prefixed by A.
    ```c++
    class AActor
    ```
- Classes that inherit from `SWidget` are prefixed by S.
    ```c++
    class SCompoundWidget
    ```



## 3. Variable Naming
### 3.0 Basic rule
- Class/Structure names use "Small Camel case" style. 
- There is no underscore between words.
- Name of variables should be nouns.
- No meanless names such as: `a`, `aa`, `sth` etc.
``` c++
int animalNum;
bool bDistinctFlag;
```

### 3.1 Boolean
Boolean variables must be prefixed by b.
``` c++
bool bPendingDestruction
bool bHasFadedIn
```

### 3.2 Out (reference para)
Prefix function parameter names with "out" if:
- The function parameters are passed by reference.
- The function is expected to write to that value.
```c++
bool TryDivide(int numerator, int denominator, double& outResult) 
{
        if (denominator == 0) {
            return false; // Division by zero, return false
        } else {
            OutResult = static_cast<double>(numerator) / denominator;
            return true; // Successful division, return true
        }
    }
```
If the boolean is reuturned from out parameter then the parameter should follow boolean type rule.
```c++
void TryCanDivide(int numerator, int denominator, double& outResult, bool& bOutSuccess) 
{
    if (denominator == 0) {
        OutSuccess = false; // Division by zero, set success to false
    } else {
        OutResult = static_cast<double>(numerator) / denominator;
        OutSuccess = true; // Successful division, set success to true
    }
}
```


## 4. Methods Naming

### 4.1 Function returns boolean
All functions that return a bool should ask a true/false question in their names.
``` c++
bool IsVisible();
bool ShouldClearBuffer();
bool CanWin();
```




## 5. Macro

### 5.1 #define
Macro names should be fully capitalized with words separated by underscores, and prefixed with `UE_`.
```c++
#define UE_AUDIT_SPRITER_IMPORT
```

## 6. Formatting

### 6.1 Braces
 Epic Games has a long standing usage pattern of putting braces on a new line.
```c++
if (TannicAcid < 10)
{
    UE_LOG(LogCategory, Log, TEXT("Low Acid"));
}
else if (TannicAcid < 100)
{
    UE_LOG(LogCategory, Log, TEXT("Medium Acid"));
}
else
{
    UE_LOG(LogCategory, Log, TEXT("High Acid"));
}
```
### 6.2 Switch
Always have a default case. Include a break just in case someone adds a new case after the default. Either include a `break`, or include a `"falls through"` comment in each case. Other code control-transfer commands (`return`, `continue`, and so on) are fine as well.
```c++
switch (condition)
{
    case 1:
        ...
        // falls through
 
    case 2:
        ...
        break;
 
    case 3:
        ...
        return;
 
    case 4:
    case 5:
        ...
        break;
 
    default:
        break;
}
```

## 7. Folder naming

## 8. Game component naming
Material Graph
Blue Print
etc

```
public class GameManager : Singleton<GameManager>
{
    [SerializeField] Transform _landTransform;
    [SerializeField] bool _isPlayerWalking;
    public event Action<int> EventPointsScored;
    public Transform LandTransform { get => _landTransform; }
    
    private int _maxHealth;
    // read-only, returns backing field,equivalent to:public int MaxHealth { get; private set; }
    public int MaxHealth => _maxHealth;

    void SaveInstanceData(int objectIndex)
    {
	_landTransform = new Vector3(objectIndex,0f,0f); 
    }
}

[Serializable]
public struct SpellData
{
    public bool isActiveSkill;
    public float cooldownTime;
}

[Flags]
public enum AttackModes
{
// Decimal
 None = 0,				// 000000
 Melee = 1,				// 000001
 Ranged = 2,				// 000010
 Special = 4,				// 000100
 MeleeAndSpecial = Melee | Special	// 000101
}


```# UnityCodeStyleGuide