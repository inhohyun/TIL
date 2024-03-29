# Comparator와 Comparable
- 객체 정렬에 필요한 메서드(정렬 기준 제공)를 정의한 인터페이스 

    Comparable : 기본 정렬기준을 구현하는데 사용
    
    Comparator : 기본 정렬기준 외에 **다른 기준**으로 정렬하고자할 때 사용

    ```
    public interface Comparator{
        int compare(Object o1, Object o2); // o1, o2 두 객체를 비교
        boolean equals(Object obj); // equals를 오버라이딩
    }

    public interface Comparable{
        int compareTo(Object o); // 주어진 객체(o)를 자신과 비교

    }

    ```
    위의 코드처럼 Comparator는 o1, o2라는 객체를 비교해서 어느쪽이 큰지를 정수값으로 반환함
    - 0이면 같음
    - 양수면 왼쪽이 큼
    - 음수면 오른쪽이 큼

    CompareTo를 보면 비교 값이 o 1개임 -> 자기 자신과 비교

## 정렬이란?
- 두 대상을 비교해서 자리 바꿈을 하는 것(이를 반복함)
- Comparator와 Comparable을 사용해서 정렬 기준을 정의함(오름차순, 내림차순 등)
- 흔히 알고있는 선택 정렬, 버블 정렬 등도 두 대상을 선택하는 전략이 다를 뿐 근본은 같음


## Comparator와  Comparable은 어떻게 구현되나?
- compare()와 compareTo()를 두 객체의 비교 결과를 반환하도록 작성

```
    public final class Integer extends Number implements Comparable{
        public int compareTo(Integer anotherInteger){
            int v1 = this.value;
            int v2 = anotherInteger.value;

            //같으면 0, 오른쪽 값이 크면 -1, 작으면 1을 반환
            return (v1 < v2 ? -1 : (b1 == v2 ? 0 : 1));
        }
    }
```
상황에 맞춰서 자리를 바꾸는 기준을 설정하면 됨

오름차순 : 왼쪽이 더 크면 자리바꿈(e.g : 7 > 5 -> 바꿈)

내림차순 : 왼쪽이 더 크면 자리바꿈(e.g : 5 < 7 -> 바꿈)


## 정렬 사용법

```
static void sort(Object[] a); 
// 객체 배열에 저장된 객체가 구현한 Comparable에 의한 정렬

static void(Object[] a, Comparator c);
//지정한  Comparator에 의한 정렬




//e.g
Arrays.sort(strArr, new Descending());

class Descending inplements Comparator{
    public int compare(Object o1, Object o2){
        if(o1 instanceof Comparable && o2 instanceof Comparable){
            Comparable c1 = (Comparable) o1;
            Comparable c2 = ((Comparable) o2);
            return c1.compareTo(c2) * -1; 
            // -1을 곱해서 기본 정렬방식의 역으로 변경한다.
            //도는 c2.compareTo(c1)과 같이 순서를 바꿔도 된다.
        }
        return -1;
    }

}


