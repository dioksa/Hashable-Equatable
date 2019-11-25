<strong>Hashable</strong>  - возвращает уникальный хэш для каждой сущности (if two hash values are different, then their corresponding original values must be different too)

Int, String, Double, Bool ... are hashable data types

<h3>(!)</h3> Hashable conforms to Equatable

Equatable - позволяет сравнивать одну сущность с другой

# Hashable
```
struct Person: Hashable {
    let name: String
    let age: Int
}
```

let user = Person(name: "Tina", age: 12)

let people = [user]

let user2 = Person(name: "Margo", age: 19)

var user3 = user

var setOfPeople = Set<Person>()

setOfPeople.hashValue

<h3>Important</h3> If 'Person' doesn't conform to Hashable protocol compiler will throw an error

     
<strong>Examples of errors:</strong>

* Generic struct 'Dictionary' requires that 'Person' conform to 'Hashable'

* Type 'Person' does not conform to protocol 'Hashable'

* Binary operator '==' cannot be applied to two 'Person' operands

```
struct Car: Hashable {
    let type: String
}
```

let miniCar = Car(type: "BMW")

```
struct People: Hashable {
    let car: Car
}
```

let personHasCar = People(car: miniCar)

В массивах мы непосредственно обращаемся к элементам по индексу, а вот в словарях или сэтах нам необходимо именно хеш значение элемента

A hash value, provided by a type’s hashValue property, is an integer that is the same for any two instances that compare equally. That is, for two instances a and b of the same type, if a == b then a.hashValue == b.hashValue. The reverse is not true: Two instances with equal hash values are not necessarily equal to each other.

Set cannot has duplicates, it is collection of unique elements (objects...)

To define that collection has only unique values we need to compare hash values of elements

# Equatable
The Equatable protocol is what allows two objects to be compared using ==, and it’s surprisingly easy to implement because Swift does most of the work for you by default

```
struct NewPerson: Hashable {
    let name: String
    let age: Int
    
    static func ==(lhs: NewPerson, rhs: NewPerson) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age
    }
}
```
Put 'static func' inside the NewPerson struct. 

Because that’s your own function you can make it do any comparisons you like. 

Swift’s default Equatable implementation will check all properties for equality, so if you have one property that is guaranteed to be unique adding your own Equatable implementation is a good idea.

Conditional Conformance to Equality
```
struct Shop<SomeType> {
    let name: String
    let buildingNumber: SomeType
}
```
```
extension Shop: Equatable where SomeType: Equatable {}
```

let foodShop = Shop<Int>(name: "Food", buildingNumber: 12)

let drinkShop = Shop<Int>(name: "Drink", buildingNumber: 53)

foodShop == drinkShop

Equality by Reference

```
class SomeObject: Equatable {
    static func == (lhs: SomeObject, rhs: SomeObject) -> Bool {
        lhs === rhs
    }
}
```

let firstObject = SomeObject()

let secondObject = SomeObject()

let thirdObject = firstObject

firstObject === secondObject // objects are not equal, they have different instances in Heap

firstObject === thirdObject  // objects are equal, because they point to the same instance in Heap area

