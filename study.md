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