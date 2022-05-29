Comparator 와 Comparable에 대해 알아보자

## 공통점과 다른점
 
### 둘다 모두 객체를 비교할때 사용되는 Interface 이고 사용하자면 내부 선언 메소드를 구현해야된다.

>
> Comparable => compareTo(T o)     
> Comparator => compare(T o1, T o2)


#### 엥 ? 그러면 두개 뭔차이에요?? 그저 매개변수차이인가요?

> #### 자기자신과 객체비교 // 두 매개변수 객체를 비교하는 차이입니다.
> 하지만 본질적으로 비교한다는 것은 같지만 비교 대상이 다르다고 보면됩니다. 


## 구현과정

### 1. Comparable
```
class MyComparable implements Comparable<MyComparable> {
	int value;
	
	@Override
	public int compareTo(MyComparable o) {
		return this.value - o.value;
	}
}
```

### 2. Comparator
```
class MyComparator implements Comparator<MyComparator> {
	int value;
	
	@Override
	public int compare(MyComparator o1, MyComparator o2) {
		if(o1.value > o2.value) {
			return 1;
		}
		else if(o1.value == o2.value) {
		return 0;
		}
		else {
			return -1;
		}
	}
}
```
#### 익명 객체를 이용해서 구현해보기

```
Comparator<Student> comp1 = new Comparator<Student>() {
			@Override
			public int compare(Student o1, Student o2) {
				return o1.classNumber - o2.classNumber;
			}
		};
```

## 주의할점 !! (이거때문에 글작성한거라고 보면됨)

### 비교할때 Underflow의 경우를 조심하자..
> 비교할 return 구현을 o.value - this.value 이런식으로 구현을 하였다면   
> 비교할 객체가 -2,147,483,648 와 -2 를 비교하면 -2,147,483,650 이 return 된다. 하지만 Underflow로 인해 +2,147,483,646 이된다. 

### 엥 그러면 비교로 구현해볼까요 ?
> 비교할 return 구현을 if(this.value> o.value) return 1 

#### 그러나 IllegalException의 위험이 있다.

> 바로 모든 상황에 대한 return값을 하지 않는 경우이다.
> 
> IllegalArgumentException - (optional) if the comparator is found to violate the Comparator contract
> 
> compare() 메서드는  두 값 중 앞의 것이 크면  음수, 같으면 0, 뒤의 것이 크면 양수를 리턴하는 함수입니다.  
> 이를 오버라이드 하여 구현하였을때 같은 값이 계속 리턴되면 두 수를 비교할 방법이 없다고 여겨집니다. 

```
class rooms implements Comparable<rooms>{
  long s;
	long e;
	
	public int compareTo(rooms o){
		if(o.s<s) return 1;
		if(o.s==s) {
			if(o.e<e) return 1;
			
		}
		return (int) (this.s-o.s);
	}
}
```

해당 코드를 보면 o.s와 s 가같으면서 o.e 와 e가같을때나 나머지에 대한 예외처리를 안해줫다. 그러면 return이 제대로 되지않아 illegalException이 된다.

#### 엥? 어차피 o.s==s 로 가고 return 이안되면 밑에 return (int) (this.s-o.s); 여기서 return 되는게아닌가요??

> 아니라고한다.. 이문제잡느라..1시간..ㅠㅠ.. 잘알아보고 사용하도록 하자..




