## 2장. 의미 있는 이름

### 2-1) 의미를 분명히 밝혀라
- 좋은 이름을 지으려면 시간이 걸리지만, 절약하는 시간이 훨씬 많다.

#### EX 1 )
```java
int d; // 경과 시간(단위: 날짜)
```
이름 d는 아무런 의미도 드러나지 않는다. 경과 시간이나 날짜라는 느낌이 안 든다.<br>
측정하려는 값과 단위를 표현하려면 다른 이름이 필요하다.
```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModfications;
int fileAgeInDays; 
```

#### EX 2 )
아래 코드를 확인해보자.
```java
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    
    for (int[] x : theList) {
        if (x[0]== 4) {
            list1.add(x);
        }    
    }
    return list1;
}
```
위 코드를 보면 코드가 하는일을 짐작하기 어렵다. <br>
왜일까? 복잡한 문장이 없지만, 코드 맥락이 코드 자체에 명시적으로 드러나지 않는다. <br>
1. theList 에 무엇이 들었는가?
2. theList 에서 0 번째 값이 어째서 중요한가?
3. 값 4는 무슨 의미인가?
4. 함수가 반환하는 리스트 list1을 어떻게 사용하는가?

위와 같은 의문이 든다. 

```java
public List<Cell> getFlaggedCells() {
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for (Cell cell : gameBoard) {
        if(cell.isFlagged()) {
            flaggedCells.add(cell);
        }    
    }
    return flaggedCells;
}
```
지뢰 찾기 게임, 게임판에서 각 칸을 객체 Cell 로 명시적으로 클래스화로 만들고, 배열에서 0번째 값은 칸 상태를 뜻하며, 값 4는 깃발이 꽂힌 상태를 가리킨다.
그 부분을 isFlagged 를 사용하여, 명시적인 함수를 통해 코드를 개선 시켜준다.<br>
이렇게 코드의 단순성은 유지한 상태에서 단순히 이름만 고쳐줬는데, 함수가 하는 일을 이해하기 쉬워진다.

> *의도가 드러나는 이름을 사용하면 코드 이해와 변경이 쉬워진다.*

<br>
<br>

### 2-2) 그릇된 정보를 피하라
- 프로그래머는 코드에 그릇된 단서를 남겨서는 안된다.

여기서 그릇된 단서는 코드 의미를 흐린다는 말이다.
그런 경우가 여러가지가 존재한다.<br>
1. hypotenuse 라는 단어가 직각삼각형의 빗변이다. 그걸 hp로 변수 선언을 한다.
2. 실제 list 가 아니라면, accountList 라고 지정하는 경우.
    - 이럴 경우, accountGroup 또는 Accounts 라 명명한다.
3. 흡사한 이름을 사용하지 않도록 주의한다
   - XYZController, ForEfficientHandlingOfStrings, XYZControllerForEfficientStorageOfStrings 이 이름의 차이를 알겠는가..?
4. 소문자 L 이나 대문자 O 변수를 한꺼번에 사용하는 경우
   - 소문자 L은 1 처럼 보이고, 대문자 O는 숫자 0처럼 보인다.

> *이름만 바꾸면 문제가 깨끗이 풀린다. 괜스레 일거리를 만들 필요가 없다.*

<br>
<br>

### 2-3) 의미 있게 구분하라
- 컴파일러나 인터프리터만 통과하려는 생각으로 코드를 구현하는 프로그래머는 스스로 문제를 일으킨다.

동일한 범위 안에서 다룬 두 개념에 같은 이름을 사용하지 못한다.<br>
그래서, 프로그래머는 한 쪽 이름을 마음대로 바꾸고싶은 유혹에 빠진다.
1. 연속된 숫자를 덧붙이거나 불용어를 추가하는 방식을 사용하는 적절치 못한 상황
2. Product 라는 클래스가 있을 때, 다른 클래스를 ProductInfo, ProductData 라 지을 때,
3. 변수 이름에 variable 이라는 걸 쓰거나, NameString 이라는 변수 명을 사용할 떄...
   - NameString 이 Name 보다 뭐가 나은가..? 그리고 Name 은 보통 String 이다..
4. 어떤 클래스에서 해당 메서드를 찾을 경우, (ex. Customer 클래스에 고객 급여 이력을 찾을 때?)
   - ```java
     getActiveAccount();
     getActiveAccounts();
     getActiveAccountInfo();
     ```
   
> *읽는 사람이 차이를 알도록 이름을 지어라.*

<br>
<br>

### 2-4) 발음하기 쉬운 이름을 사용하라
- 사람들은 단어에 능숙하다. 발음하기 어려운 이름으로 지을 경우, 토론조차 하기 어렵고 바보처럼 들리기 십상이다.

#### EX 1)
```java
class DtaRcrd102 {
    private Date genymdhms;
    private Date modyndhms;
    private final String pszqing = "102";
}
```
```java
class Customer {
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
}
```
> *위 두 코드를 비교해보자. 그럼 알 것이다.*

<br>
<br>

### 2-5) 검색하기 쉬운 이름을 사용하라.
- 문자 하나를 사용하는 이름과 상수는 텍스트 코드에서 쉽게 눈에 띄지 않는다는 점이 있다.

#### EX 1 )
```java
for (int j = 0; j < 34; j++) {
    s += (t[j]*4)/5;    
}
```
하.. 위 코드 숨막히네
```java
int realDaysPersIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j = 0; j < NUMBER_OF_TASKS; j++) {
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```
위 코드를 비교 해보자.<br>
사실 아래 코드가 함수가 전체적으로 길어진 건 느껴질 것이다. 하지만 상수 찾기가 얼마나 쉬운지 생각해아라.

<br>
<br>

### 2-6) 인코딩을 피하라
- 유형이나 범위정보까지 인코딩에 넣으면 그만큼 이름을 해독하기 어려워진다.

자바 프로그래머는 변수 이름에 타입을 인코딩할 필요가 없다. 또한, 이제 헝가리식 표기법이나 기타 인코딩 방식이 오히려 방해가 될 뿐이다. <br>
변수, 함수, 클래스 이름이나 타입을 바꾸기가 어려워지며, 읽기도 어려워진다. 그래서 독자를 오도할 가능성이 커진다.

#### EX 1 )
```java
PhoneNumber phoneString;
```
위 같이 타입이 바뀌어도 이름이 바뀌지 않는다.

#### EX 2 )
이제는 멤버 변수에 m_이라는 접두어를 붙힐 필요가 없다.
```java
public class Part {
    private String m_dsc; 
    void setName(String name) {
        m_dsc = name;
    }
}
```
```java
public class Part {
    String description;
    void setDescription(String description) {
        this.description = description;
    }
}
// 게다가 요즘 IDE는 다른색상으로 구분 지어준다.
```

#### EX 3 )
때로는 인코딩이 필요한 경우가 있지만, 제대로하자.<br>
도형을 생성하는 ABSTRACT FACTORY 를 구현할 때, <br>
클래스 명명할 때, 인터페이스 클래스와 구체 클래스를 지을 때 신경써야한다.
```
X
IShapeFactory 와 ShapeFactory ?
O
ShapeFactoryImp 로 하는게 좋다.
```

<br>
<br>

### 2-7) 자신의 기억력을 자랑하지마라.
- 자신이 아는 이름을 변환하지 말아라. 일반적으로 문제 영역이나 해법 영역에서 사용하지 않는 이름을 선택한 것이다. 그러면 문제가 생긴다.
- 문자 하나만 사용하는 변수 이름은 문제가 있다.

> 클래스 이름은 명사나 명사구가 적합하다.<br>
> 메서드 이름은 동사나 동사구가 적합하다.<br>
> 생성자를 중복 정의할 때는 정적 팩토리 메서드를 사용한다.


<br>
<br>

### 2-8) 기발한 이름은 피하라.
> 의도를 분명하고 솔직하게 표현라라.

<br>
<br>

### 2-9) 한 개념에 한 단어를 사용하라.
- 추상적인 개념 하나에 단어 하나를 선택해 이를 고수한다.

예를 들어 각 클래스마다 메서드를 fetch, retrieve, get 를 각기 다르게 부르면 혼란이 온다.
마찬가지로, 동일 코드 기반에 controller, manager, driver 를 섞어 쓰면 혼란스럽다.
> 일관성 있게 작성하자.

<br>
<br>

### 2-10) 말장난을 하지마라
- 한 단어를 두가지 목적을 사용하지 마라.

예를 들어, add 메서드를 기존 값 두 개를 더하거나 이어서 새로운 값을 만드는 메서드이다. 새로 작성하는 메서드는 집합에 값 하나를 추가한다. 이 메서드를 add 라는 이름으로 명명해도 괜찮을까?
하지만, 맥락이 다르다. 그러므로, insert 나 append 로 이름을 구분지어 사용하는게 좋다.

> 코드를 최대한 이해하기 쉽게 짜야한다.

<br>
<br>

### 2-11) 해법 영역에서 가져온 이름을 사용하라.
- 코드를 읽을 사람도 프로그래머이다. 그러므로 전산용어, 알고리즘 이름, 패턴 이름, 수학 용어 등을 사용해도 좋다.

<br>
<br>

### 2-12) 문제 영역에서 가져온 이름을 사용하라.
- 우수한 프로그래머는 해법 영역과 문제 영역을 구분할 줄 알아야 한다. 문제 영역 개념과 관련 깊은 코드라면, 문제 영역에서 이름을 가져와야 한다.

<br>
<br>

### 2-13) 의미 있는 맥락을 추가하라.
- 스스로 의미가 분명한 이름이 없지 않다. 하지만, 대다수 이름은 분명하지 못한다.  그래서 클래스, 함수, 이름 공간에 넣어 맥락을 부여 한다. 모든 방법이 실패하면, 마지막 수단으로 접두어를 붙힌다.

#### Ex 1)
```java
firstName, lastName, houseNumber, city, state, zipcode
위 변수는 변수명만 보아도 주소라는 사실을 안다.
```
하지만, 어느 메서드가 state 라는 변수 하나만 사용한다면 ? 변수 state 가 주소 일부라는 사실을 금방 알아차릴까? <br>
이 때, 접두어를 추가해서 쓰면 된다.
```java
addrFirstName, addrLastName, addrState 라 쓰면 맥락이 분명해진다.
```

#### Ex 2)
```java
private void printGuessStatistics(char candidate, int count) {
    String number;
    String verb;
    String pluraModfier;
    
    if (count == 0) {
        number = "no";
        verb = "are";
        pluraModifier = "s";
    }else if (count = 1) {
        number = "1";
        verb = "is";
        pluraModifier = "";
    }else {
        number = Integer.toString(count);
        verb = "are";
        pluraModifier = "s";
    }
    
    String guessMessage = String.format(
            "There %s %s %s%s", verb, number, candidate, pluraModifier
        );
    print(guessMessage);
}
```
기준. 위 아래 코드 비교.
```java
public class GuessStatisticsMessage {
    private String number;
    private String verb;
    private String pluralModifier;
    
    public String make (char candidate, int count) {
        createPluralDependentMessageParts(count);
        return String.format(
                "There %s %s %s%s", verb, number, candidate, pluralModifier
        );
        
        private void createPluralDependentMessageParts(int count) {
            if(count == 0) {
                thereAreNoLetters();
            }else if( count == 1) {
                thereIsOneLetter();
            }else {
                thereAreManyLetters(coubt);
            }
        }

        private void thereAreManyLetters(int count) {
            number = Integer.toString(count);
            verb = "are";
            pluraModifier = "s";
        }
        private void thereIsOneLetter() {
            number = "1";
            verb = "is";
            pluraModifier = "";
        }
        private void thereAreNoLetters() {
            number = "no";
            verb = "are";
            pluraModifier = "s";
        }
    }
}
```

> 두 코드를 보면, 맥락을 개선하면 함수를 쪼개기 쉬워지므로 알고리즘도 좀 더 명확해진다는 것을 알 수 있다.

<br>
<br>

### 2-14) 불필요한 맥락을 없애라
- 예시로 설명을 하고자 한다.
```
1. Gas Station Deluxe 를 GSD 로 클래스 명을 지으면 안된다.
이유는? IDE에서 G를 입력하고 자동 완성 키를 누르면 IDE는 모든 클래스를 열거한다. 즉, IDE를 방해할 필요가 없다.

2. GSD 회계모듈에 MailingAddress 클래스를 추가하면서 GSDAccountAddress로 이름을 변경했는데, 나중에 다른 고객 관리 프로그램에서 고객 주소가 필요하다.
이때, GSDAccountAddress 클래스를 이용해야하나..? 완전 부적절하다.
```

> 불필요한 맥락을 추가하지 않도록 주의해야한다.
