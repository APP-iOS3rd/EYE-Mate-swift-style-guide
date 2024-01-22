# EYE-Mate-swift-style-guide
EYE-Mate 구성원들이  Swift 코드를 이해하기 쉽고 명확하게 작성하기 위한 스타일 가이드입니다. 구성원들의 의사결정에 따라 수시로 변경될 수 있습니다.

본 문서에 나와있지 않은 규칙은 아래 문서를 따릅니다.

- [Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/)
- [SE-0005](https://github.com/apple/swift-evolution/blob/main/proposals/0005-objective-c-name-translation.md)

## 목차
- [코드 포매팅](#코드-포매팅)
  - [1. Import 순서](#1-import-순서)
  - [2. 들여쓰기](#2-들여쓰기)
  - [3. 띄어쓰기](#3-띄어쓰기)
  - [4. 줄 바꿈](#4-줄-바꿈)
  - [5. 소괄호](#5소괄호)
- [네이밍](#네이밍)
  - [0. 명확한 이름](#0-명확한-이름)
  - [1. 클래스와 구조체](#1-클래스와-구조체)
  - [2. 함수](#2-함수)
  - [3. 변수와 상수](#3-변수와-상수)
  - [4. 열거형](#4-열거형)
  - [5. 프로토콜](#5-프로토콜)
- [코드 스타일](#코드-스타일)
  - [1. General](#1-general)
  - [2. Access Control](#2-access-control)
  - [3. 사용자 지정 연산자](#3-사용자-지정-연산자)
  - [4. Switch 문과 Enum](#4-switch-문과-enum)
  - [5. Optional](#5-optional)
  - [6. Protocol](#6-protocol)
  - [7. Property](#7-property)
  - [8. Closure](#8-closure)
  - [9. Array](#9.-array)
  - [10. Error Handling](#10.-error-handling)
  - [11. guard 문 사용](#11.-guard-문-사용)
- [주석](#주석)
- [프로그래밍 권장사항](#프로그래밍-권장사항)
- [참고 링크](#참고-링크)

## 코드 포매팅

### 1. Import 순서

- 내장 프레임워크를 먼저 import하고 빈 줄로 구분해 third-party 프레임워크를 import합니다. 

- 모듈 import는 알파벳 순으로 정렬합니다.

✅ Preferred
``` swift
import Foundation
import UIKit

import AdSupport
import AppTrackingTransparency
import RxCocoa
import RxSwift
import SwiftyJSON
```

⛔ Not Preferred
``` swift
import UIKit
import AppTrackingTransparency
import Foundation
import RxSwift
import RxCocoa
import SwiftyJSON
import AdSupport
```
- 사용하지 않는 모듈은 import 하지 않습니다.

✅ Preferred
``` swift
import UIKit

var view: UIView
```
⛔ Not Preferred
``` swift
import Foundation  // not required
import UIKit

var view: UIView
```
### 2. 들여쓰기

- 들여쓰기는 Xcode에서 제공하는 control(^) + i 를 사용합니다. 

✅ Preferred
``` swift
var vaildProductCount: Int {
    allProducts
        .filter { $0.isVaild }
        .count
}
```
⛔ Not Preferred
``` swift
var vaildProductCount: Int {
    allProducts
    .filter { $0.isVaild }
    .count
}
```

### 3. 띄어쓰기

- 클래스 상속, 클래스 프로토콜 채택, 타입 선언, 호출 파라미터, 선언 파라미터, 제네릭 프로토콜 채택, 딕셔너리에서 콜론(:) 사용 시, 오른쪽에만 공백을 하나 둡니다.

✅ Preferred
``` swift
class MyViewController: UIViewController { ... }
extension MyViewController: UITableViewDataSource { ... }
let headerDictionary: [String: String] = [
    "Content-Type": "application/json"
]
someFunction(name: someString)
func myFunction<T, U: SomeProtocol>(firstParam: T, secondParam: U) { ... }
```
⛔ Not Preferred
``` swift
class MyViewController:UIViewController { ... }
extension MyViewController : UITableViewDataSource { ... }
let headerDictionary:[String : String] = [
    "Content-Type":"application/json"
]
someFunction(name : someString)
func myFunction<T, U:SomeProtocol>(firstParam : T, secondParam:U) { ... }
```
- 삼항연산자에서 콜론(:) 사용 시, 양 옆에 공백을 하나 둡니다.

✅ Preferred
``` swift
var dayString = day < 10 ? "0\\(day)" : "\\(day)"
```
⛔ Not Preferred
``` swift
var dayString = day < 10 ? "0\\(day)": "\\(day)"
```

- 배열, 함수, switch-case 등 모든 곳에서 쉼표(,) 사용 시, 오른쪽에만 공백을 하나 둡니다. 

✅ Preferred
``` swift
let array = ["A", "B", "C"]

func testFunc<T, U>(firstParam: T, secondParam: U) { ... } 

someFunction(name: "a", age: 15)

switch number {
case 1, 2, 3:
    // Do something
default:
    break
}

let dict: [String: Int] = [
    "a": 1,
    "b": 2
]
```
⛔ Not Preferred
``` swift
let array = ["A","B" , "C"]

func testFunc<T,U>(firstParam: T , secondParam: U) { ... } 

someFunction(name: "a",age: 15)

switch number {
case 1 , 2,3:
    // Do something
default:
    break
}

let dict: [String: Int] = [
    "a": 1 ,
    "b": 2
]
```  
- 연산자는 양 옆에 공백을 하나 둡니다.

✅ Preferred
``` swift
let answer = 1 + 2 / 3 % (4 * 5)
```
⛔ Not Preferred
``` swift
let answer = 1+2/3%(4*5)
```

- 함수와 클로저 리턴 타입에 사용되는 화살표는 양 옆에 공백을 하나 둡니다.

✅ Preferred
``` swift
func someFunc() -> String { ... }
let completion: () -> Void
```
⛔ Not Preferred
``` swift
func someFunc()->String { ... }
let completion: ()->Void
```
- 일반적으로 함수 선언시, 함수명과 소괄호를 붙혀쓰고, 연산자 오버로딩시 공백을 하나 둡니다.

✅ Preferred
``` swift
func testFunc() {}
func == (lhs: SomeClass, rhs: SomeClass) {}
```
⛔ Not Preferred
``` swift
func testFunc () {}
func ==(lhs: SomeClass, rhs: SomeClass) {}
```
- 한 줄 클로저 등, 중괄호 안쪽은 띄워쓰기를 하나 둡니다.

✅ Preferred
``` swift
numArray
    .filter { $0 % 2 == 0 }
    .map { "\\($0)" }
    .joined(separator: ",")

guard let self = self else { return }
```
⛔ Not Preferred
``` swift
numArray
    .filter {$0 % 2 == 0}
    .map {"\\($0)" }
    .joined(separator: ",")

guard let self = self else { return}
```

### 4. 줄 바꿈
- 빈 줄에는 공백이 포함되지 않도록 하며 모든 파일은 빈 줄로 끝나도록 합니다.

- Xcode 의 Page guide 기준, 120 charactor 을 넘으면 반드시 줄 바꿈 합니다.

[Page guide 켜는 방법](https://iris-numeric-9d0.notion.site/Page-guide-c02799769e524056956a2fe18f7c6356)

- guard let self = self else { return } 은 한 줄로 씁니다.

- if let, guard let 구문이 긴 경우 줄 바꿈하고 한 칸 들여씁니다. 

✅ Preferred
``` swift
guard let self = self else { return }
```
⛔ Not Preferred
``` swift
guard let self = self else { 
    return 
}
```
- 여는 중괄호({) 를 새 줄에 배치하지 않습니다. [1TBS 스타일](https://en.m.wikipedia.org/wiki/Indentation_style#1TBS)을 사용합니다.

✅ Preferred
``` swift
func someMethod() {
    // Do something
}
```
⛔ Not Preferred
``` swift
func someMethod() 
{
    // Do something
}
```
### 5. 소괄호
- if, switch-case, 파라미터, 후행 클로저 등 불필요한 소괄호는 생략합니다.

✅ Preferred
``` swift
if count > 0 { ... }
switch type { ... }
_ = arr.filter { num in num % 2 == 0 }
```
⛔ Not Preferred
``` swift
if (count > 0) { ... }
switch (type) { ... }
_ = arr.filter() { (num) in num % 2 == 0 }
```


## 네이밍
### 0. 명확한 이름
- 가능한 명확하고 모든 의미를 포함하는 이름을 사용합니다.

- 이름이 길어져도 의미가 있는 이름이 타인의 코드를 볼 때 훨씬 빠르고 편합니다.

✅ Preferred
``` swift
class RoundAnimationButton { ... }
func startAnimating() { ... }
let animationDuration: CGFloat
let personImageView: UIImageView
let titleLabel: UILabel
```
⛔ Not Preferred
``` swift
class CustomButton { ... }
class RoundAniBtn { ... }
func srtAnimating() { ... }
let aniDur: CGFloat
let personImage: UIImageView  // image? imageView?
let title: UILabel            // String? label?
```
### 1. 클래스와 구조체
- 클래스와 구조체의 이름에는 UpperCamelCase를 사용합니다.

- 클래스 이름에는 접두사를 붙이지 않습니다.

✅ Preferred
``` swift
class SomeClass {
  // class definition goes here
}

struct SomeStructure {
  // structure definition goes here
}
```
⛔ Not Preferred
``` swift
class someClass {
// class definition goes here
}

struct someStructure {
// structure definition goes here
}
```
### 2. 함수
- 함수 이름에는 lowerCamelCase를 사용합니다.

- 함수 이름 앞에는 되도록이면 get을 붙이지 않습니다.

✅ Preferred
``` swift
func date(from string: String) -> Date?
func anchor(for node: SCNNode) -> ARAnchor?                          
func distance(from location: CLLocation) -> CLLocationDistance        
func track(withTrackID trackID: CMPersistentTrackID) -> AVAssetTrack? 
```
⛔ Not Preferred
``` swift
func getdate(from string: String) -> Date?
func getAnchor(for node: SCNNode) -> ARAnchor?                          
func Getdistance(from location: CLLocation) -> CLLocationDistance        
func Track(withTrackID trackID: CMPersistentTrackID) -> AVAssetTrack? 
```

- Action 함수(유저 인터렉션을 처음 처리하는 함수) 와 ReactorKit.Action의 네이밍은 '주어 + 동사 + 목적어' 형태를 사용합니다.

  - *Tap(눌렀다 뗌- )* 은 UIControlEvents의 `.touchUpInside`에 대응하고, *Press(누름)* 는 `.touchDown`에 대응합니다.

  - will\~은 특정 행위가 일어나기 직전이고, did\~는 특정 행위가 일어난 직후입니다.

  - should\~, is\~, can\~ 은 일반적으로 Bool을 반환하는 함수에 사용합니다.

✅ Preferred
``` swift
func backButtonDidTap() {
  // ...
}
```
⛔ Not Preferred
``` swift
func back() {
  // ...
}

func pressBack() {
  // ...
}
```
- API 를 호출하는 함수는 앞에 HTTP 함수(eg. get, post, put, delete, patch 등)를 붙힙니다.

✅ Preferred
``` swift
static func getAccessToken() -> Observable<Data> { ... }

static func patchShippingAddress() -> Observable<Data> { ... }
```
⛔ Not Preferred
``` swift
static func requestAccessToken() -> Observable<Data> { ... }
static func takeAccessToken() -> Observable<Data> { ... }
static func fetchAccessToken() -> Observable<Data> { ... }

static func updateShippingAddress() -> Observable<Data> { ... }
static func modifyShippingAddress() -> Observable<Data> { ... }
```

### 3. 변수와 상수
- 변수 이름과 상수 이름에는 lowerCamelCase를 사용합니다.

✅ Preferred
``` swift
let maximumNumberOfLines = 3
```
⛔ Not Preferred
``` swift
let MaximumNumberOfLines = 3
let MAX_LINES = 3
```
### 4. 열거형
- enum의 이름에는 UpperCamelCase를 사용합니다.

- enum의 각 case에는 lowerCamelCase를 사용합니다.

✅ Preferred
``` swift
enum Result {
  case .success
  case .failure
}
```
⛔ Not Preferred
``` swift
enum Result {
  case .Success
  case .Failure
}

enum result {
  case .Success
  case .Failure
}
```
### 5. 프로토콜
- 프로토콜의 이름은 [애플의 API 디자인 가이드라인](https://www.swift.org/documentation/api-design-guidelines/#naming)을 참고합니다.

  - 무엇인가 설명하는 프로토콜은 명사로 읽어야 합니다. (e.g. Collection).

  - 기능을 설명하는 프로토콜은 able, ible, ing 접미사를 사용합니다.(e.g. Equatable, ProgressReporting)

  - 어떤 것도 적합하지 않은 경우, Protocol 을 접미사로 사용할 수 있습니다.

- 프로토콜의 이름에는 UpperCamelCase를 사용합니다.

✅ Preferred
``` swift
protocol ImagePresentable { ... }
protocol NotificationUIProtocol { ... }
```
⛔ Not Preferred
``` swift
protocol ImagePresent { ... }
protocol NotificationUIType { ... }
```


- 구조체나 클래스에서 프로토콜을 채택할 때는 콜론(:)과 공백을 넣어 구분하여 명시합니다.

- extension을 통해 채택할 때도 동일하게 적용합니다.

✅ Preferred
``` swift
protocol SomeProtocol {
  // protocol definition goes here
}

struct SomeStructure: SomeProtocol, AnotherProtocol {
  // structure definition goes here
}

class SomeClass: SomeSuperclass, SomeProtocol, AnotherProtocol {
    // class definition goes here
}

extension UIViewController: SomeProtocol, AnotherProtocol {
  // doSomething()
}
```
⛔ Not Preferred
``` swift
protocol someProtocol {
  // protocol definition goes here
}

struct SomeStructure:SomeProtocol, AnotherProtocol {
  // structure definition goes here
}

class SomeClass:SomeSuperclass, someProtocol, AnotherProtocol {
    // class definition goes here
}

extension UIViewController:SomeProtocol, AnotherProtocol {
  // doSomething()
}
```
### 6. 약어
- 약어는 모두 대문자로 표기하고, 약어로 시작하는 경우에만 소문자로 표기합니다.

✅ Preferred
``` swift
  let userID: Int?
  let html: String?
  let websiteURL: URL?
  let urlString: String?
```
⛔ Not Preferred
``` swift
  let userId: Int?
  let HTML: String?
  let websiteUrl: NSURL?
  let URLString: String?
```
### 7. Delegate
- Delegate 메서드는 프로토콜명으로 네임스페이스를 구분합니다. 

✅ Preferred
``` swift
protocol UserCellDelegate {
  func userCellDidSetProfileImage(_ cell: UserCell)
  func userCell(_ cell: UserCell, didTapFollowButtonWith user: User)
}
```
⛔ Not Preferred
``` swift
protocol UserCellDelegate {
  func didSetProfileImage()
  func followPressed(user: User)

  // `UserCell`이라는 클래스가 존재할 경우 컴파일 에러 발생
  func UserCell(_ cell: UserCell, didTapFollowButtonWith user: User)
}
```

## 코드 스타일

### 1. General
- 가능한 `var`보다 `let` 을 선호합니다.

- 한 컬렉션에서 다른 컬렉션으로 변환할 때는 반복문보다 `map`, `filter`, `reduce` 등의 구성을 선호합니다. 이러한 방법을 사용할 때는 side effect가 있는 클로저를 사용하지 않도록 주의하세요.

✅ Preferred
``` swift
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]

let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]
```
⛔ Not Preferred
``` swift
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}
// ["1", "2", "3"]

var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
// [4, 8, 16, 42]
```
- 상수나 변수에서 타입을 추론할 수 있는 경우 타입을 선언하지 않는 것이 좋습니다.

- 함수가 여러 값을 반환하는 경우, `inout` 인수를 사용하는 것보다 튜플을 반환하는 것이 좋습니다(반환하는 값이 명확하지 않은 경우 레이블이 지정된 튜플을 사용하는 것이 가장 좋습니다). 특정 튜플을 두 번 이상 사용하는 경우 `typealias` 사용을 고려하세요. 하나의 튜플에 3개 이상의 항목을 반환하는 경우에는 `struct`나 `class`를 사용하는 것이 좋습니다.

✅ Preferred
```swift
func pirateName() -> (firstName: String, lastName: String) {
    return ("Guybrush", "Threepwood")
}

let name = pirateName()
let firstName = name.firstName
let lastName = name.lastName
```
⛔ Not Preferred
```swift
func pirateName(firstName: inout String, lastName: inout String) {
    firstName = "Guybrush"
    lastName = "Threepwood"
}

var firstName = ""
var lastName = ""
pirateName(&firstName, &lastName)
```
- 클래스에서 Delegate/Protocol을 생성할 때 [순환 참조(Retain Cycle)](https://hyunndyblog.tistory.com/154)에 주의하세요. 일반적으로 이러한 프로퍼티는 `weak`로 선언해야 합니다.

- [Escaping Closure](https://jusung.github.io/Escaping-Closure/)에서 직접 `self`를 호출할 때는 순환 참조(Retain Cycle)가 발생할 수 있으므로 주의하세요. 이 경우, [capture list](https://showcove.medium.com/swift-closure-capture-lists-1-277d2e60dc2d)를 사용하세요.
``` swift
myFunctionWithEscapingClosure() { [weak self] (error) -> Void in
    // you can do this

    self?.doSomething()

    // or you can do this

    guard let strongSelf = self else {
        return
    }

    strongSelf.doSomething()
}
```
- Labeled break를 사용하지 마세요.

⛔ Not Preferred
```swift
outerloop: for i in 1...3{
  innerloop: for j in 1...3 {
    if j == 3 {
      break outerloop
    }
      print("i = \(i), j = \(j)")
  }
}
```
- 제어 흐름(Control Flow) 조건식에 괄호를 넣지 마세요.

✅ Preferred
``` swift
if x == y {
    /* ... */
}
```
⛔ Not Preferred
``` swift
if (x == y) {
    /* ... */
}
```
- 가능하면 `enum` 타입을 작성하지 말고 단축형을 사용하세요.

✅ Preferred
``` swift
imageView.setImageWithURL(url, type: .person)
```
⛔ Not Preferred
``` swift
imageView.setImageWithURL(url, type: AsyncImageView.Type.person)
```
- 일반적으로 `enum`과 달리 클래스 메서드에서는 컨텍스트를 추론하기가 더 어렵기 때문에 클래스 메서드에는 단축형을 사용하지 마세요.

✅ Preferred
``` swift
imageView.backgroundColor = UIColor.white
```
⛔ Not Preferred
``` swift
imageView.backgroundColor = .white
```
- 꼭 필요한 경우가 아니라면 `self.`를 쓰지 않는 것이 좋습니다.

- 메서드를 작성할 때는 메서드를 재정의할 것인지 아닌지를 염두에 두세요. 그렇지 않은 경우 `final`로 표시하되, 테스트 목적으로 메서드를 덮어쓰지 않도록 주의하세요. 일반적으로 `final` 메서드를 사용하면 컴파일 시간이 단축되므로 해당되는 경우 이를 사용하는 것이 좋습니다. 그러나 라이브러리에서 `final` 키워드를 적용할 때는 로컬 프로젝트에서 `non-final`을 `final`로 변경하는 것과는 달리 라이브러리에서 `non-final`을 `final`로 변경하는 것은 간단하지 않으므로 특히 주의하세요.

- 블록 뒤에 `else`, `catch` 등과 같은 문을 사용할 때는 이 키워드를 블록과 같은 줄에 넣습니다. 여기에서도 1TBS 스타일을 따르고 있습니다. `if/else` 및 `do/catch` 코드의 예는 아래와 같습니다.
``` swift
if someBoolean {
    // do something
} else {
    // do something else
}

do {
    let fileContents = try readFile("filename.txt")
} catch {
    print(error)
}
```
- 클래스의 인스턴스가 아닌 클래스와 연관된 함수나 프로퍼티를 선언할 때는 `class`보다 `static`을 사용하세요. 서브클래스에서 해당 함수나 프로퍼티를 재정의하는 기능이 특별히 필요한 경우에만 `class`를 사용하되, 대신 `protocol` 사용을 고려하세요.

- 인수를 받지 않고, side effect가 없으며, 일부 객체나 값을 반환하는 함수가 있다면 함수 대신 계산된 프로퍼티를 사용하는 것이 좋습니다.

### 2. Access Control

- [Access Control](https://joycestudios.tistory.com/15) 키워드가 필요한 경우 먼저 작성합니다.

✅ Preferred
``` swift
private static let myPrivateNumber: Int
```
⛔ Not Preferred
``` swift
static private let myPrivateNumber: Int
```
- Access Control 키워드는 한 줄에 홀로 존재하면 안 되고, 설명하는 내용과 인라인으로 유지해야 합니다.

✅ Preferred
``` swift
open class Pirate {
    /* ... */
}
```
⛔ Not Preferred
``` swift
open
class Pirate {
    /* ... */
}
```
- 일반적으로 `internal` Access Control 키워드는 기본값이므로 작성하지 마세요.

- 단위 테스트에서 프로퍼티에 액세스해야 하는 경우 `@testable import ModuleName`을 사용하여 프로퍼티를 `internal`로 만들어야 합니다. 프로퍼티가 `private`로 설정되어야 하지만 단위 테스트 목적으로 `internal`로 선언하는 경우 이를 설명하는 적절한 주석을 추가해야 합니다.  아래와 같이 명확하게 표시하기 위해 `- warning:` 마크업 구문을 사용할 수 있습니다.
``` swift
/**
 This property defines the pirate's name.
 - warning: Not `private` for `@testable`.
 */
let pirateName = "LeChuck"
```

- 가능하면 `fileprivate`보다 `private`로 설정하는 것이 좋습니다.

- `public`과 `open` 중에서 선택할 때는 특정 모듈 외부에서 서브클래싱이 가능한 것을 만들려는 경우 `open`을, 그렇지 않은 경우 `public`을 사용합니다. `internal` 이상의 모든 항목은 `@testable import`을 사용하여 테스트에서 서브클래싱할 수 있으므로 이것이 `open`을 사용할 이유가 되어서는 안 된다는 점에 유의하세요. 일반적으로 라이브러리의 경우 `open`을 조금 더 자유롭게 사용하되, 여러 모듈에서 동시에 변경하기 쉬운 앱과 같은 코드베이스의 모듈에 대해서는 조금 더 보수적으로 사용하는 것이 좋습니다.

### 3. 사용자 지정 연산자
사용자 지정 연산자보다 named function을 만드는 것이 좋습니다.

사용자 정의 연산자를 도입하려는 경우 다른 구문을 사용하는 대신 새 연산자를 전역 범위에 도입하려는 매우 타당한 이유가 있는지 확인하세요.

새로운 타입(특히 `==`)을 지원하기 위해 기존 연산자를 재정의할 수 있습니다. 하지만 새 정의는 연산자의 의미를 유지해야 합니다. 예를 들어 `==`는 항상 동일성을 테스트하고 boolean을 반환해야 합니다.

### 4. Switch 문과 Enum
- 유한한 가능성의 집합(`enum`)이 있는 switch 문을 사용할 때는 `default` case를 포함하지 마세요. 대신 사용하지 않는 case를 맨 아래에 배치하고 `break` 키워드를 사용하여 실행을 방지하세요. 새로운 `case`가 생성됐을때 인지하지 못한 상태에서 `default`로 처리되지 않고 의도적으로 처리를 지정해 주기 위함입니다.

✅ Preferred
``` swift
switch someEnum {
case someCase1:
    print("someCase1")
case someCase2, soemCase3:
    break
}
```
⛔ Not Preferred
``` swift
switch someEnum {
case someCase1:
    print("someCase1")
default:
    break
}
```

- Swift의 swtich case는 기본적으로 break되므로 필요하지 않은 경우 `break` 키워드를 포함하지 마세요.

- `case` 문은 [기본 Swift 표준에 따른 `switch` 문](https://google.github.io/swift/#switch-statements)과 일치해야 합니다.

- 연관된 값이 있는 case를 정의할 때는 단순한 타입이 아니라 적절한 레이블을 지정합니다(e.g. `case hunger(Int)` 대신에 `case hunger(hungerLevel: Int)`).
``` swift
enum Problem {
    case attitude
    case hair
    case hunger(hungerLevel: Int)
}

func handleProblem(problem: Problem) {
    switch problem {
    case .attitude:
        print("At least I don't have a hair problem.")
    case .hair:
        print("Your barber didn't know when to stop.")
    case .hunger(let hungerLevel):
        print("The hunger level is \(hungerLevel).")
    }
}
```

- 가능하면 `fallthrough` 키워드보다 가능한 리스트(e.g. `case 1, 2, 3:`)를 사용합니다.

- 도달해서는 안 되는 default case가 있는 경우에는 오류를 던지거나 assert 같은 다른 유사한 방식으로 처리하는 것이 좋습니다.
``` swift
func handleDigit(_ digit: Int) throws {
    switch digit {
    case 0, 1, 2, 3, 4, 5, 6, 7, 8, 9:
        print("Yes, \(digit) is a digit!")
    default:
        throw Error(message: "The given number was not a digit.")
    }
}
```

### 5. Optional
- 암시적으로 언래핑된 optional을 사용해야 하는 유일한 경우는 `@IBOutlet`입니다. 다른 모든 경우에는 non-optional 또는 일반 optional 프로퍼티를 사용하는 것이 좋습니다. 프로퍼티가 절대 `nil`이 되지 않는다고 '보장'할 수도 있지만, 안전하고 일관성을 유지하는 것이 좋습니다. 마찬가지로 강제 언래핑을 사용하지 마세요.

- `as!` 나 `try!`를 사용하지 마세요.

- optional에 저장된 값을 실제로 사용할 계획은 없지만 이 값이 `nil`인지 여부를 확인해야 하는 경우, `if let` 구문을 사용하는 대신 이 값을 명시적으로 `nil`과 비교하여 확인합니다.

✅ Preferred
``` swift
if someOptional != nil {
    // do something
}
```
⛔ Not Preferred
``` swift
if let _ = someOptional {
    // do something
}
```

- `unowned`를 사용하지 마세요. `unowned`는 암시적으로 언래핑되는 `weak` 프로퍼티와 비슷하다고 생각할 수 있습니다(`unowned` 프로퍼티는 참조 카운팅을 완전히 무시하기 때문에 약간의 성능 향상이 있지만). 암시적 언래핑을 원하지 않으므로 마찬가지로 `unowned` 프로퍼티도 원하지 않습니다.

✅ Preferred
``` swift
weak var parentViewController: UIViewController?
```
⛔ Not Preferred
``` swift
weak var parentViewController: UIViewController!
unowned var parentViewController: UIViewController
```

- optinal을 언래핑 할 때는 언래핑된 상수 또는 변수에 동일한 이름을 사용하세요.
``` swift
guard let myValue = myValue else {
    return
}
```

- 테스트에서 강제 언래핑 대신 `XCTUnwrap`을 사용합니다.
✅ Preferred
``` swift
func isEvenNumber(_ number: Int) -> Bool {
    return number % 2 == 0
}

func testWithXCTUnwrap() throws {
    let number: Int? = functionThatReturnsOptionalNumber()
    XCTAssertTrue(isEvenNumber(try XCTUnwrap(number)))
}
```
⛔ Not Preferred
``` swift
func isEvenNumber(_ number: Int) -> Bool {
    return number % 2 == 0
}

func testWithForcedUnwrap() {
    let number: Int? = functionThatReturnsOptionalNumber()
    XCTAssertTrue(isEvenNumber(number!)) // may crash the simulator
}
```

### 6. Protocol
프로토콜을 구현할 때, 코드를 구성하는 방법에는 두 가지가 있습니다:
1. 프로토콜 구현을 나머지 코드와 분리하기 위한 `// MARK:` 주석 사용
2. `class`/`struct` 구현 코드 외부에 있지만 동일한 소스 파일에 있는 extension 사용

그러나 extension을 사용할 때는 extension의 메서드를 서브클래스로 재정의할 수 없으므로 테스트가 어려울 수 있습니다. 이것이 일반적인 use case라면 일관성을 위해 방법 1을 사용하는 것이 좋습니다. 그렇지 않은 경우에는 방법 2를 사용하면 우려 사항을 더 깔끔하게 분리할 수 있습니다.

방법 2를 사용하는 경우에도 Xcode의 메서드/프로퍼티/클래스 등 리스트 UI에서 가독성을 높이기 위해 `// MARK:` 문을 추가하세요.

- 프로토콜을 채택할 때는 extension을 만들어서 관련된 메서드를 모아둡니다.
✅ Preferred
``` swift
final class MyViewController: UIViewController {
  // ...
}

// MARK: - UITableViewDataSource

extension MyViewController: UITableViewDataSource {
  // ...
}

// MARK: - UITableViewDelegate

extension MyViewController: UITableViewDelegate {
  // ...
}
```
⛔ Not Preferred
``` swift
final class MyViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
  // ...
}
```

### 7. Property
- 읽기 전용의 계산된 프로퍼티를 만드는 경우, 그 주위에 `get {}`를 붙이지 않고 getter를 제공합니다.
``` swift
var computedProperty: String {
    if someBool {
        return "I'm a mighty pirate!"
    }
    return "I'm selling these fine leather jackets."
}
```
- `get {}`, `set {}`, `willSet`, `didSet` 사용 시, 이 블럭을 들여쓰기 합니다.

- `willSet`/`didSet` 및 `set`의 새 값이나 이전 값에 대한 사용자 정의 이름을 생성할 수 있어도 기본적으로 제공되는 표준 `newValue`/`oldValue` 식별자를 사용합니다.
``` swift
var storedProperty: String = "I'm selling these fine leather jackets." {
    willSet {
        print("will set to \(newValue)")
    }
    didSet {
        print("did set from \(oldValue) to \(storedProperty)")
    }
}

var computedProperty: String  {
    get {
        if someBool {
            return "I'm a mighty pirate!"
        }
        return storedProperty
    }
    set {
        storedProperty = newValue
    }
}
```
- 싱글톤 프로퍼티는 다음과 같이 선언할 수 있습니다:
``` swift
class PirateManager {
    static let shared = PirateManager()

    /* ... */
}
```
### 8. Closure
매개변수의 타입이 명확하다면 타입 이름을 생략해도 괜찮지만, 명시하는 것도 괜찮습니다. 때로는 명확한 세부 사항을 추가하여 가독성을 높이고 때로는 반복되는 부분을 제거하여 가독성을 높일 수 있으므로 최선의 판단을 내리고 일관성을 유지하세요.
``` swift
// omitting the type
doSomethingWithClosure() { response in
    print(response)
}

// explicit type
doSomethingWithClosure() { response: NSURLResponse in
    print(response)
}

// using shorthand in a map statement
[1, 2, 3].flatMap { String($0) }
```
- 클로저를 타입으로 지정하는 경우, 타입이 optional이거나 클로저가 다른 클로저 안에 있는 경우와 같이 필수적인 경우가 아니라면 괄호로 묶을 필요가 없습니다. 클로저의 인수는 항상 괄호로 묶어야 합니다. 인수가 없음을 나타내려면 `()`를 사용하고, 아무것도 반환되지 않음을 나타내려면 `Void`를 사용합니다.
``` swift
let completionBlock: (Bool) -> Void = { (success) in
    print("Success? \(success)")
}

let completionBlock: () -> Void = {
    print("Completed!")
}

let completionBlock: (() -> Void)? = nil
```
- 매개변수 이름은 가능하면 여는 중괄호와 같은 줄에 유지합니다.

- 매개변수 이름 없이는 클로저의 의미가 명확하지 않은 경우(e.g. 메서드에 success 및 failure 클로저에 대한 매개변수가 있는 경우)를 제외하고는 후행 클로저 구문을 사용합니다.
``` swift
// trailing closure
doSomething(1.0) { (parameter1) in
    print("Parameter 1 is \(parameter1)")
}

// no trailing closure
doSomething(1.0, success: { (parameter1) in
    print("Success with \(parameter1)")
}, failure: { (parameter1) in
    print("Failure with \(parameter1)")
})
```  
### 9. Array
- 일반적으로 subscript를 사용하여 배열에 직접 액세스하지 마세요. 가능하면 optional이며 충돌을 일으키지 않는 `.first` 또는 `.last`와 같은 접근자를 사용하세요. 가능하면 `for i in 0 ..< items.count`와 같은 구문보다는 `for item in items`와 같은 구문을 사용합니다. 배열 subscript로 직접 액세스해야 하는 경우 적절한 바운드 검사를 수행해야 합니다. `for (index, value) in items.enumerated()`를 사용하여 인덱스와 값을 모두 가져올 수 있습니다.

- 배열을 추가/연결할 때, `+=` 또는 `+` 연산자를 절대 사용하지 마세요. 대신 `.append()` 또는 `.append(contentsOf:)`를 사용하는 것이 Swift의 현재 상태에서는 (적어도 컴파일과 관련해서는) 훨씬 더 성능이 좋습니다. 다른 배열을 기반으로 하는 배열을 선언하고 이를 immutable로 유지하려는 경우, `let myNewArray = arr1 + arr2` 대신` let myNewArray = [arr1, arr2].joined()`를 사용하세요.

### 10. Error Handling
`myFunction` 함수가 `String`을 반환해야 하지만 어느 시점에서 오류가 발생할 수 있다고 가정해 보겠습니다. 일반적인 접근 방식은 이 함수가 optional `String?`을 반환하도록 하는 것입니다. 여기서 문제가 발생하면 `nil`을 반환합니다.
``` swift
func readFile(named filename: String) -> String? {
    guard let file = openFile(named: filename) else {
        return nil
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    let filename = "somefile.txt"
    guard let fileContents = readFile(named: filename) else {
        print("Unable to open file \(filename).")
        return
    }
    print(fileContents)
}
```
대신 실패의 원인을 파악해야할 때, Swift의 `try`/`catch` 동작을 사용해야 합니다.

다음과 같은 `struct`를 사용할 수 있습니다:
``` swift
struct Error: Swift.Error {
    public let file: StaticString
    public let function: StaticString
    public let line: UInt
    public let message: String

    public init(message: String, file: StaticString = #file, function: StaticString = #function, line: UInt = #line) {
        self.file = file
        self.function = function
        self.line = line
        self.message = message
    }
}
```
사용 예시:
``` swift
func readFile(named filename: String) throws -> String {
    guard let file = openFile(named: filename) else {
        throw Error(message: "Unable to open file named \(filename).")
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    do {
        let fileContents = try readFile(named: filename)
        print(fileContents)
    } catch {
        print(error)
    }
}
```
오류 처리 대신 optional을 사용하는 것이 합당한 몇 가지 예외가 있습니다. 결과를 검색하는 동안 무언가 잘못되어 결과가 <i>의미론적으로</i> `nil`이 될 가능성이 있는 경우에는 오류 처리 대신 optional을 반환하는 것이 좋습니다.

일반적으로 메서드가 '실패'할 수 있고 optional 반환 타입을 사용한다면, 실패의 이유가 즉시 명확하지 않은 경우, 메서드에서 오류를 발생시키는 것이 합리적일 수 있습니다.

### 11. `guard` 문 사용
- 일반적으로 `if` 문에 코드를 중첩하는 대신, 적용 가능한 경우 "early return" 전략을 사용하는 것을 선호합니다. 이 사용 사례에 `guard` 문을 사용하면 코드의 가독성을 향상시키는 데 도움이 되는 경우가 많습니다.

✅ Preferred
``` swift
func eatDoughnut(at index: Int) {
    guard index >= 0 && index < doughnuts.count else {
        // return early because the index is out of bounds
        return
    }

    let doughnut = doughnuts[index]
    eat(doughnut)
}
```
⛔ Not Preferred
``` swift
func eatDoughnut(at index: Int) {
    if index >= 0 && index < doughnuts.count {
        let doughnut = doughnuts[index]
        eat(doughnut)
    }
}
```
- optional을 언래핑 할 때, `if` 문 대신 `guard` 문을 사용하여 코드에서 중첩된 들여쓰기의 양을 줄입니다.

✅ Preferred
``` swift
guard let monkeyIsland = monkeyIsland else {
    return
}
bookVacation(on: monkeyIsland)
bragAboutVacation(at: monkeyIsland)

// EVEN LESS PREFERRED
if monkeyIsland == nil {
    return
}
bookVacation(on: monkeyIsland!)
bragAboutVacation(at: monkeyIsland!)
```
⛔ Not Preferred
``` swift
if let monkeyIsland = monkeyIsland {
    bookVacation(on: monkeyIsland)
    bragAboutVacation(at: monkeyIsland)
}
```

- optional 언래핑이 필요하지 않은 경우, `if` 문과 `guard` 문 중 어떤 것을 사용할지 결정할 때 가장 중요한 것은 코드의 가독성입니다. 여기에는 서로 다른 두 개의 boolean에 의존하는 경우, 여러 비교를 포함하는 복잡한 논리문 등 여러 가지 경우가 있을 수 있으므로 일반적으로 가독성과 일관성이 있는 코드를 작성하기 위해 최선의 판단을 하세요. `guard`와 `if` 중 어느 쪽이 더 가독성이 높은지 확실하지 않거나 가독성이 똑같은 것 같으면 `guard`를 사용하는 것이 좋습니다.
``` swift
// an `if` statement is readable here
if operationFailed {
    return
}

// a `guard` statement is readable here
guard isSuccessful else {
    return
}

// double negative logic like this can get hard to read - i.e. don't do this
guard !operationFailed else {
    return
}
```

- 서로 다른 두 상태 중에서 선택하는 경우, `guard` 문이 아닌 `if` 문을 사용합니다.

✅ Preferred
``` swift
if isFriendly {
    print("Hello, nice to meet you!")
} else {
    print("You have the manners of a beggar.")
}

```
⛔ Not Preferred
``` swift
guard isFriendly else {
    print("You have the manners of a beggar.")
    return
}

print("Hello, nice to meet you!")
```

- 또한, 실패로 인해 현재 컨텍스트를 종료해야 하는 경우에만 `gurad`를 사용해야 합니다. 아래는 `gurad` 두 개를 사용하는 대신 `if` 문 두 개를 사용하는 것이 더 적합한 예시입니다. 여기에는 서로 block해서는 안 되는 두 개의 관련 없는 조건이 있습니다.
``` swift
if let monkeyIsland = monkeyIsland {
    bookVacation(onIsland: monkeyIsland)
}

if let woodchuck = woodchuck, canChuckWood(woodchuck) {
    woodchuck.chuckWood()
}
``` 

- 종종 `guard` 문을 사용하여 여러 개의 optional을 언래핑해야 하는 상황에 직면할 수 있습니다. 일반적으로 각 언래핑의 실패를 처리하는 방법이 동일(e.g. `return`, `break`, `continue`, `throw` 또는 `@noescape` )하다면 언래핑을 하나의 `guard` 문으로 결합합니다.
``` swift
// combined because we just return
guard let thingOne = thingOne,
    let thingTwo = thingTwo,
    let thingThree = thingThree else {
    return
}

// separate statements because we handle a specific error in each case
guard let thingOne = thingOne else {
    throw Error(message: "Unwrapping thingOne failed.")
}

guard let thingTwo = thingTwo else {
    throw Error(message: "Unwrapping thingTwo failed.")
}

guard let thingThree = thingThree else {
    throw Error(message: "Unwrapping thingThree failed.")
}
```
## 주석
- 항상 `//` 뒤에 공백을 둡니다.

- `// MARK: -` 주석은 위로 2개, 아래로 1개의 빈 줄을 둡니다.
``` swift
class Pirate {


    // MARK: - instance properties

    private let pirateName: String


    // MARK: - initialization

    init() {
        /* ... */
    }

}
```
## 프로그래밍 권장사항
- 가능하다면 변수를 정의할 때 함께 초기화하도록 합니다. [Then](https://github.com/devxoul/Then)을 사용하면 초기화와 함께 속성을 지정할 수 있습니다.
``` swift
let label = UILabel().then {
  $0.textAlignment = .center
  $0.textColor = .black
  $0.text = "Hello, World!"
}
```
- 상수를 정의할 때에는 enum를 만들어 비슷한 상수끼리 모아둡니다. 재사용성과 유지보수 측면에서 큰 향상을 가져옵니다. struct 대신 enum을 사용하는 이유는, 생성자가 제공되지 않는 자료형을 사용하기 위해서입니다. [CGFloatLiteral](https://github.com/devxoul/CGFloatLiteral)과 [SwiftyColor](https://github.com/devxoul/SwiftyColor)를 사용해서 코드를 단순화시킵니다.
``` swift
final class ProfileViewController: UIViewController {

  private enum Metric {
    static let profileImageViewLeft = 10.f
    static let profileImageViewRight = 10.f
    static let nameLabelTopBottom = 8.f
    static let bioLabelTop = 6.f
  }

  private enum Font {
    static let nameLabel = UIFont.boldSystemFont(ofSize: 14)
    static let bioLabel = UIFont.boldSystemFont(ofSize: 12)
  }

  private enum Color {
    static let nameLabelText = 0x000000.color
    static let bioLabelText = 0x333333.color ~ 70%
  }

}
```
이렇게 선언된 상수들은 다음과 같이 사용될 수 있습니다.
``` swift
self.profileImageView.frame.origin.x = Metric.profileImageViewLeft
self.nameLabel.font = Font.nameLabel
self.nameLabel.textColor = Color.nameLabelText
```
- `Array<T>`와, `Dictionary<T: U>` 보다는 `[T], [T: U]`를 사용합니다.

✅ Preferred
``` swift
var messages: [String]?
var names: [Int: String]?
```
⛔ Not Preferred
``` swift
var messages: Array<String>?
var names: Dictionary<Int, String>?
```
- 컴파일러가 문맥 속에서 타입을 추론할 수 있으면, 더 간결한 코드를 위해 타입을 생략합니다.

✅ Preferred
``` swift
let selector = #selector(viewDidLoad)
view.backgroundColor = .red
let toView = context.view(forKey: .to)
let view = UIView(frame: .zero)
```
⛔ Not Preferred
``` swift
let selector = #selector(ViewController.viewDidLoad)
view.backgroundColor = UIColor.red
let toView = context.view(forKey: UITransitionContextViewKey.to)
let view = UIView(frame: CGRect.zero)
```

- 문법의 모호함을 제거하기 위해 언어에서 필수로 요구하지 않는 이상 `self`는 사용하지 않습니다.

✅ Preferred
``` swift
final class Listing {
  private let isFamilyFriendly: Bool
  private var capacity: Int
  
  init(capacity: Int, allowsPets: Bool) {
    self.capacity = capacity
    isFamilyFriendly = !allowsPets
  }

  private func increaseCapacity(by amount: Int) {
    capacity += amount
    save()
  }
}
```
⛔ Not Preferred
``` swift
final class Listing {
  private let isFamilyFriendly: Bool
  private var capacity: Int
  
  init(capacity: Int, allowsPets: Bool) {
    self.capacity = capacity
    self.isFamilyFriendly = !allowsPets // `self.` not required here
  }

  private func increaseCapacity(by amount: Int) {
    self.capacity += amount
    self.save()
  }
}
```
✅ Preferred
``` swift
TaxiPush.progressing.asPushActionObservable(callInfo.value.call.id)
            .map { $0.progressing }.unwrap()
            .map { $0/60 }
            .bind(to: timeRadius)
            .disposed(by: disposeBag)
```
⛔ Not Preferred
``` swift
TaxiPush.progressing.asPushActionObservable(callInfo.value.call.id)
            .map { $0.progressing }.unwrap()
            .map { $0/60 }
            .bind(to: self.timeRadius)
            .disposed(by: self.disposeBag)
```
- 프로퍼티의 초기화는 가능하면 init에서하고 가능하면 unwrapped Optionl의 사용을 지양합니다.

✅ Preferred
``` swift
class MyClass: NSObject {

  init() {
    someValue = 0
    super.init()
  }

  var someValue: Int
}
```
⛔ Not Preferred
``` swift
class MyClass: NSObject {

  init() {
    super.init()
  }

  var someValue: Int?
}
```
- 제네릭 타입 파라미터는 대문자를 사용하고 묘사적이어야 합니다. 타입 이름이 의미있는 관계나 역할을 갖지 않는 경우에만 T, U 혹은 V 같은 전형적인 단일 대문자를 사용하고 그 외에는 의미있는 이름을 사용합니다.

✅ Preferred
``` swift
struct Stack<Element> { ... }
func write<Target: OutputStream>(to target: inout Target)
func swap<T>(_ a: inout T, _ b: inout T)
```
⛔ Not Preferred
``` swift
struct Stack<T> { ... }
func write<target: OutputStream>(to target: inout target)
func swap<Thing>(_ a: inout Thing, _ b: inout Thing)
```
- 디폴트 타입 메서드는 `static`을 사용합니다.

✅ Preferred
``` swift
class Fruit {
  static func eatFruits(_ fruits: [Fruit]) { ... }
}
```
⛔ Not Preferred
``` swift
class Fruit {
  func eatFruits(_ fruits: [Fruit]) { ... }
}
```
- 더 이상 상속이 발생하지 않는 클래스는 항상 final 키워드로 선언합니다.

✅ Preferred
``` swift
final class SettingsRepository {
  // ...
}
```
⛔ Not Preferred
``` swift
class SettingsRepository {
  // ...
}
```
- `return`은 생략하지 않습니다.

✅ Preferred
``` swift
["1", "2", "3"].compactMap { return Int($0) }

var size: CGSize {
  return CGSize(
    width: 100.0,
    height: 100.0)
}

func makeInfoAlert(message: String) -> UIAlertController {
  return UIAlertController(
    title: "Info",
    message: message,
    preferredStyle: .alert)
}
```
⛔ Not Preferred
``` swift
["1", "2", "3"].compactMap { Int($0) }

var size: CGSize {
  CGSize(
    width: 100.0,
    height: 100.0)
}

func makeInfoAlert(message: String) -> UIAlertController {
  UIAlertController(
    title: "Info",
    message: message,
    preferredStyle: .alert)
}
```
- Xcode가 자동으로 생성한 템플릿을 포함한 사용하지 않는 코드는 placeholder 코멘트를 포함해 모두 제거합니다.

✅ Preferred
``` swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  return Database.contacts.count
}
```
⛔ Not Preferred
``` swift
override func didReceiveMemoryWarning() {
  super.didReceiveMemoryWarning()
  // Dispose of any resources that can be recreated.
}

override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  // #warning Incomplete implementation, return the number of rows
  return Database.contacts.count
}
```

## 참고 링크

https://github.com/StyleShare/swift-style-guide

https://jusung.github.io/Swift-Code-Convention

https://github.com/linkedin/swift-style-guide

https://google.github.io/swift

https://soojin.ro/blog/english-for-developers-swift
