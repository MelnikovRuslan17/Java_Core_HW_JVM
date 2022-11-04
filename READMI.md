# Разбор работы JVM 
## Исходный код 

    public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      
        Object o = new Object();        
        Integer ii = 2;                 
        printAll(o, i, ii);             
        System.out.println("finished"); 
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   
        System.out.println(o.toString() + i + ii);  
    }
}

## Анализ кода 
### 1. public class JvmComprehension {
    
    Загружается класс, в метаспейсе будет храниться информация о загруженном классе JvmComprehension и других системных загруженных классах.

### 2 public static void main(String[] args) 

    В стек попадает метод main открывается его frame.

### 3 int i = 1

    В frame попадает примитив int со значением 1.

### 4 Object o = new Object()

    Создается новый объект Object в куче(heap) затем создается переменная "o" в frame main, которая ссылается на Object.

### 5 Integer ii = 2

    Создается новый объект Integer в куче(heap) затем создается переменная "ii" в frame main которая ссылается на Integer со значением 2.

### 6 printAll(o, i, ii)

    Метод printAll попадает с стек открывается его frame, вызывается метод параметрами "o,i,ii". Два параметра "o,ii" берет и кучи см. п. 4.5, один параметр из frame main "i"

### 7  private static void printAll(Object o, int i, Integer ii) {    
###    Integer uselessVar = 700;                                

    В куче создается новый объект Integer, создается переменная "uselessVar" в frame printAll которая ссылается на Integer со значением 700.

### 8 private static void printAll(Object o, int i, Integer ii) {
### Integer uselessVar = 700;                   
###       System.out.println(o.toString() + i + ii);  

    Выполнается печать данных в консоль, после этого frame printAll будет закрыт, сборщик мусора может убрать Integer 700 из кучи так как ссылок на него больше нет.

### 9 System.out.println("finished")

    Выполняется вывод в консоль "finished" frame main заканчивается работу и будет закрыт, после этого сборщик мусора может собрать Integer со значением "2" и Object.

