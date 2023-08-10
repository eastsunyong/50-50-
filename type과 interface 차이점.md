## type 선언

```
type NameType={
	firstName:string;
  lastName:string;
}

const person1:NameType={
	firstName:'Tom';
  lastName:'Cruise;
}
```

## interface 선언

```
interface NameType{
	firstName:string;
  lastName:string;
}

const person1:NameType={
	firstName:'Tom';
  lastName:'Cruise;
}
```

## type 과 interface의 차이

### 확장하는 방법

type같은 경우 확장할 때 '&'기호를 사용하여 타입확장을 한다.

```
type PersonType={
	name:string;
  age:string;
}

type StudentType=PersonType & {
	school:string
}
```

interface같은 경우 extends키워드를 사용하여 타입확장을 한다.

```
interface PersonType{
	name:string;
  age:string;
}

interface StudentType extends PersonType{
	school:string
}

```

### computed property에서의 사용

> computed property란 표현식을 이용해 객체의 키 값을 정의하는 문법이다.
> 

```
type name = 'firstName'|'lastName';

type Nametype={
	[key in name]:string; // 가능
}

interface NameType={
	[key in name]:string; // 불가능
}

```

### 선언가능한 타입

type같은 경우 primitive, union, tuple, object타입 모두 선언이 가능하지만 interface같은 경우 object타입만 선언이 가능하다.

```
type NameType='firstName'|'lastName';

type Nametype= FirstNameType | LastNameType;

type NameType=[string, number];

```

### 함수 선언 방법

```
type getList=(id: number) => void;

interface getList{
	(id:number): void;
}
```

### interface에서만 가능한 것

> 선언적 확장 : 같은 이름으로 선언하여 새로운 속성을 추가하는 것
> 

```
type NameType={
	firstName:string;
}

type NameType={
	lastName:string; // 불가능
}

interface NameType{
	firstName:string;
}

interface NameType{
	lastName:string; // 가능

}
```

- **type과 interface 차이점**
    
    **확장**을 하는 방법은 다를지언정 type과 interface 둘 다 확장이 **가능한 것**을 볼 수 있다.
    여기서 **차이점**이 발생하는데, 인터페이스의 경우에는 **선언적 확장**이 가능하다는 점이다.
    **선언적 확장은 동일한 이름으로 interface를 선언해줬을 경우 자동적으로 하나로 합쳐진다.**
    이는 **type에서는 불가능**한 기능이므로 interface만 가능하다.
    그리고 확장 기능에 있어서 **성능**적으로 interface 좀 더 준수한 성능을 가지고 있다고 한다.
    
- **그래서 무엇이 더 좋은가 ?**
    - 팀 내 공통적으로 정해서 사용하는 게 가장 베스트이며, type과 interface의 쓰임새를 생각하고 각각에 맞게 사용해주는 게 좋다고 생각된다.
    - 사실 객체지향적 언어에서 많이 사용되는 interface의 경우 type처럼 사용하는 경우는 없고 하나의 규격으로 클래스에 구현하는 방식으로 많이 사용되기 때문에 **type은 경우 그저 interface처럼 구현을 한다기보다는 값을 담아두기 위해 사용**하고, **interface는 하나의 규격이기 때문에 그것을 이용해 구현하고자 할 때 사용하면 될 거라 생각**한다.
