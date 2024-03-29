## 📌 열거형

열거형은 연관된 항목들을 묶어서 표현할 수 있는 타입입니다.

enum은 타입이므로 대문자 카멜케이스를 사용하여 이름을 정의합니다.

각 case는 소문자 카멜케이스로 정의합니다.

각 case는 그 자체가 고유의 값입니다.

### 📐 열거형 기본

```swift
enum 이름 {
    case 이름1
    case 이름2
    case 이름3, 이름4, 이름 5
    ...
}
```

### 📐 열거형 예제

```swift
enum Weekday{
    case mon	// 한 개씩 만듬
    case tue
    case wed, thu, fri, sat, sun	// 연속해서 만듬
}

var day: Weekday = Weekday.mon	// 열거형 case를 나타내는 방법 (= 열거형이름 케이스이름)
day = .tue	// 위에 처럼 나타내주고 축약하여 나타내도 됨 (= 케이스이름)

print(day)

switch day {	// switch 구문에 열거형 타입 사용가능.
    case .mon, .tue, .wed, .thu:
    	print("평일입니다")
    case Weekday.fri:
    	print("불금 파티")
    case .sat, .sun:
    	print("주말")
}
```

[코드 설명]

Weekday를 열거형으로 만들어주었습니다.

case를 한 개씩 만들어줘도 되고, 아니면 연속해서 만들어줘도 됩니다.

열거형의 케이스를 나타내는 문법은 var day: Weekday = Weekday.mon으로 나타내 주었습니다.

열거형 케이스를 나타내는 방법은 [var 변수이름: 열거형이름 = 열거형이름.케이스이름] 으로 나타내줄 수 있습니다.

열거형의 케이스를 나타내줬다면 day = .tue 이런 식으로 축약할 수 있습니다.

축약하여 나타내주려면 [var 변수이름: 열거형이름 = 열거형이름.케이스이름] 꼭 이런식으로 나타내주고 사용해야합니다.

열거형은 Switch 구문에서 많이 사용이 됩니다.

열거형에서 Switch 구문에서 사용법은 switch 열거형변수이름 {...}을 해주고 case 부분에서는 .열거형케이스이름을 써주면 됩니다.

위와 같이 열거형에서 사용한 case를 사용하여 줬다면 상관 없겠지만 case가 없는 경우에는 default를 꼭 정의해 줘야 합니다.

Switch 구문 사용법은 [05) Swift 조건문, 반복문](https://velog.io/@jkang4531/05-Swift-%EC%A1%B0%EA%B1%B4%EB%AC%B8-%EB%B0%98%EB%B3%B5%EB%AC%B8)에서 설명하였습니다.


## 📌 원시 값

열거형의 각 항목은 자체로도 하나의 값이지만 항목의 원시 값도 가질 수 있습니다.

원시 값은 특정 타입으로 지정된 값을 가질 수 있다는 뜻입니다. 

C 언어의 enum처럼 정수값을 가질 수도 있습니다.

특정 타입의 값을 원시 값으로 가지고 싶다면 열거형 이름 오른쪽에 타입을 명시해 주면 됩니다.

원시 값을 사용하고 싶다면 rawValue라는 프로퍼티를 사용하면 됩니다.

case 별로 각각 다른 값을 가져야 합니다.


### 📐 원시 값 예제

정수 값 사용

```swift
enum Fruit: Int {
    case apple = 0
    case grape = 1
    case peach		// 정수를 명시해주지 않아도 자동으로 1씩 증가합니다.
}

print("Fruit.peach.rawValue == \(Fruit.peach.rawValue)")
// Fruit.peach.rawValue == 2
```

정수 타입 뿐만 아니라 다른 타입 사용

Hashable 프로토콜을 따르는 모든 타입이 열거형의 원시 값으 타입으로 지정될 수 있습니다.

```swift
enum School: String {
    case elementary = "초등"
    case middle = "중등"
    case high = "고등"
    case university
}

print("School.middle.rawValue == \(School.middle.rawValue)")
// School.middle.rawValue == 중등

print("School.university.rawValue == \(School.university.rawValue)")
// School.university.rawValue == university
```

## 📌 원시 값 초기화

원시 값은 rawValue를 통해 초기화 할 수 있습니다.

rawValue가 case에 해당하지 않을 수 있으므로 rawValue를 통해 초기화 한 인스턴스는 옵셔널 타입입니다.

위에서 정수 값 사용 예시로 코드를 사용하겠습니다.

```swift
// let apple: Fruit = Fruit(rawValue: 0)
let apple: Fruit? = Fruit(rawValue: 0)

if let orange: Fruit = Fruit(rawValue: 5) {
	print("rawValue 5에 해당하는 케이스는 \(orange)입니다")
} else {
	print("rawValue 5에 해당하는 케이스가 없습니다")
} // rawValue 5에 해당하는 케이스가 없습니다.
```

[코드 설명]

Fruit로 만든 열거형에는 0, 1, 2 밖에 없습니다.

주석으로 처리된 [let apple: Fruit = Fruit(rawValue: 0)]을 일반 타입으로 할당해 주려고 하면 오류가 발생합니다.

그 이유는 일반 타입이 아니라 옵셔널 타입이기 때문입니다.

case가 없으면 생성이 되지 않을 수도 있기 때문에 nil이 나올 수도 있습니다.

옵셔널 타입으로 다시 정의해 주고 if let으로 안전하게 꺼내서 사용 가능합니다.

## 📌 메서드

Swift의 열거형은 메서드도 추가해줄 수 있습니다.

```swift
enum Month{
	case dec, jan, feb
    case mar, apr, may
    case jun, jul, aug
    case sep, oct, nov 
    
    func printMessage() {
    	switch self {
        case .mar, .apr, .may:
        	print("봄")
        case .jun, .jul, .aug:
        	print("여름")
        case .sep, .oct, .nov:
        	print("가을")
        case .dec, .jan, .feb:
        	print("겨울")
        }
    }
}

Month.mar.printMessage()

```
