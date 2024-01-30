# Java gyakorlatok - Fájlkezelés

## Fájl beolvasása

### A fájl

```txt
Id:Name:City:Salary:Birth
1:János:Szolnok:392:1993-04-12
2:Béla:Szeged:397:1998-07-21
```

### Modell

Emplyoee.java

```java
class Employee {
    Integer id;
    String name;
    String city;
    Double salary;
    LocalDate birth;
}
```

### A beolvasás

```java
import java.io.File;
import java.io.FileNotFoundExcepiton;
import java.time.LocalDate;

class Fajlkezelo {
    public void readfile() {
        try {
            tryReadfile();
        }catch(FileNotFoundException e)
    }
    public void tryReadfile() throws FileNotFoundException {
        File file = new File("adat.txt");
        Scanner sc = new Scanner(file);

        while(sc.hasNext()) {
            String line = sc.nextLine();
            String[] lineArray = line.split(":");
            Employee emp = new Employee();
            emp.id = Integer.parseInt(lineArray[0]);
            emp.name = lineArray[1];
            emp.city = lineArray[2];
            emp.salary = Double.parseDouble(lineArray[3]);
            emp.birth = LocalDate.parse(lineArray[4]);
        }
    }
}
```
