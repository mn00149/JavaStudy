# 정적 멤버와 static

- 정적 멤버란 클래스의 고정된 멤버로써 **객체를 생성하지 않고**사용 할 수 있는 필드와 메서드(클래스 멤버라고도 한다)

## static 멤버 선언

- static 키워드를 붙여 줌으로써 정적 멤버를 선언

```
    public class StaticTest{
         // 최초 1회만 메모리 할당을 받고 모든 객체들이 공유함
         public static int b = 0;
        // 정적 메서드 선언
        static int pius(int x, int y) {
            return x+y;
        }
         //인스턴스 변수
         private int a = 0;
     }
```

- 정적 필드와 메서드는 클래스에 고정된 멤버이므로 클래스 로딩이 끝나면 바로 사용이 가능
- 인스턴스로 필드로 선언 할 지 static 필드로 선언 할 지의 판단 기준

  - 객체마다 각각 가져야 하는 데이터 => 인스턴스 필드로 선언
  - 공용적인 데이터 => static 으로 선언

- 인스턴스로 메서드로 선언 할 지 static 메서드로 선언 할 지의 판단 기준
  - 인스턴스 필드를 사용하는 경우 => 인스턴스 메서드로 사용
  - 인스턴스 필드를 사용하지 않는 경우 => static 메서드로 사용

```
    public class Calculator {
        String color;
        void setColor(String color) { this.color = color }// 인스턴스 필드 사용, 인스턴스 메서드
        // 정적 메서드
        static int pius(int x, int y) {
            return x+y;
        }
    }
```

- 정적요소의 접근은 클래스로 하는것을 권장 한다

```
    class ScjpPass{
    //멤버 변수, Heap
    int t1=0;
    int t2=0;
    int t3=0;
    int t4=0;

    //클래스 변수, Data area
    static int BONUS=100;

    //생성자, Source area
    public ScjpPass(){
    }

    //생성자, this = sp객체가 가지고 있는 hash code
    //sp객체의 heap메모리를 공유하게됩니다.
    //int t1, int t2, int t3, int t4: Stack
    public ScjpPass(int t1, int t2, int t3, int t4){
        //Heap = Stack
        //전역 변수 = 지역 변수
        //멤버 변수 = 지역 변수
        this.t1 = t1;
        this.t2 = t2;
        this.t3 = t3;
        this.t4 = t4;
    }

}


public class Scjp {
    public static void main(String[] args) {
        System.out.println("ScjpPass.BONUS: " + ScjpPass.BONUS);

        //t1은 static이 아님으로 클래스명으로 접근 할 수 없습니다.
        //System.out.println(ScjpPass.t1);
        //heap memory 할당
        ScjpPass sp = new ScjpPass(85, 90, 80, 70);
        System.out.println("sp.t1: " + sp.t1);
        //static변수는 클래스명으로 접근을 권장합니다.
        //System.out.println("sp.BONUS: " + sp.BONUS);
    }
}

```

## 정적 초기화 블록

- 계산이 필요한 복잡한 정적필드의 초기화시 static block 을 통해 초기화 한다
- static block은 클래스 로딩시 자동 실행되고 클래스 내에 여러개가 선언 가능

```
public class StaticBlock {
    static String company = "Samsung";
    static String model = "LEDTV";
    static String TV;
    static {
        TV = company + model;
    }

}
```

## 정적 메서드와 블록선언 시 주의점

- static 메서드나 블록은 객체가 없이도 실행 가능 => 인스턴스 필드나 메서드, this 키워드 사용X
- static block에서 인스턴스 멤버를 쓰고 싶을 땐 객체를 먼저 생성 후 참조 변수로 접근해야한다
- main() 메서드 또한 static이므로 인스턴스 메서드를 바로 사용 할 수 없다

```
public class Car {
    int speed;

    void run(){
        System.out.println("지금 차량의 속도:"+speed);
    }
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.speed = 60;
        myCar.run();
    }
}

```

## 싱글톤(Singleton)

- 전채 프로그램중 **단 하나만** 만들수 있도록 보장된 객체
- 만드는 법
  1. 생성자를 외부에서 호출 할 수 없도록 private 접근 제한자를 붙여준다
  2. 자신의 타입인 정적 필드를 선언하고 자신의 객체를 생성하여 초기화
  3. 정적 메서드인 getInstance()를 선언하여 정적 필드에서 참고하고 있는 자신의 객체를 리턴

```public class Singleton {
    //자신의 타입인 정적 필드를 선언하고 자신의 객체를 생성하여 초기화
    private static Singleton instance = new Singleton();

    private Singleton() {
        // 생성자는 외부에서 호출못하게 private 으로 지정해야 한다.
    }

    //정적 메서드인 getInstance()를 선언하여 정적 필드에서 참고하고 있는 자신의 객체를 리턴
    public static Singleton getInstance() {
        return instance;
    }

}
```

## 싱글톤 패턴의 사용하는 이유

- 최초 한번의 new 연산자를 통해서 고정된 메모리 영역을 사용하기 때문에 추후 해당 객체에 접근할 때 메모리 낭비를 방지할 수 있다.
- 다른 클래스 간에 데이터 공유가 쉽다.
- 싱글톤 인스턴스가 전역으로 사용되는 인스턴스이기 때문에 다른 클래스의 인스턴스들이 접근하여 사용할 수 있다.
- 도메인 관점에서 인스턴스가 한 개만 존재하는 것을 보증하고 싶은 경우 싱글톤 패턴을 사용하기도 한다.

- 위의 코드는 멀티 스레드 환경에서 Thread-Safe 를 보장해주지 않는다.
- 두 개의 스레드에서 동시에 getInstance() 를 호출 한경우 에 if (instance == null) 조건문에 동시에 도달하게 되어 instance 를 두번 생성할 수 도 있기 떄문!
- 이를 해결하기 위해, Java 에서 스레드 동기화를 지원하는 Synchronzied 를 사용할 수 있다.

```
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    // synchronzied 스레드 동기화를 사용하며 멀티 스레드 환경에서의 동시성 문제 해결
    public static synchronzied Singleton getInstance() {
      if(instance  == null) {
         instance  = new Singleton();
      }
      return instance;
    }
}
```

## final

값을 변경할 수 없는 final 변수(상수 선언)

- 값을 변경할 수가 없습니다.

- 값을 고정할 필요가 있는 코드와 같은 형태의 데이터에 사용합니다.

```
값을 변경할 수 없는 final 변수(상수 선언)
   - 값을 변경할 수가 없습니다.

   - 값을 고정할 필요가 있는 코드와 같은 형태의 데이터에 사용합니다.
     예)1년 12달, 요일, 주7일


>>>>> Finalmain.java

class Final{
    int money = 10000;  //인스턴스 변수

    //값을 변경 할 수 없습니다.
    final int day = 7;  //1주, final 인스턴스 변수
    final int week = 4; //한달, final 인스턴스 변수

    //객체를 만들지 않아도 사용할 수 있습니다.
    //final static 변수
    final static int month = 12; //1년

    //생성자가 존재 하지만 아무런 처리를 하지 않습니다.
    public Final(){}
}

public class Finalmain {

    public static void main(String[] args) {
        Final fi = new Final();
        fi.money = 15000;
        //final변수는 값을 변경(대입)할 수 없습니다.
        //fi.day = 10;
        System.out.println("1주일 용돈:" + fi.money * fi.day);
        System.out.println("1년" + Final.month + "달");
        //Final.month = 20000;
    }
}

```
