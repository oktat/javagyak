# Java gyakorlat - Adatbázis

## Adatbázis készítése

Adatbázis létrehozása

create.sql:

```sql
create database if not exists zoldzrt
default character set utf8
default collate utf8_hungarian_ci;

grant all privileges
on zoldzrt.*
to zoldzrt@localhost
identified by 'titok';

use zoldzrt;

create table if not exists employees(
    id int not null primary key auto_increment,
    name varchar(50),
    city varchar(50),
    salary double,
    birth date
);
```

## Kapcsolódás Java nyelven

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

class DataService {
    public void createEmplyoee(Employee emp) {
        try {
            tryCreateEmployee(emp);
        }catch(SQLException e) {
            System.err.println("Hiba! A kapcsoldóás sikertelen!)
            System.err.println(e.getMessage());
        }
    }
    public void tryCreateEmployee(Employee emp) throws SQLException{
        String user = "zoldzrt";
        String pass = "titok2;
        String url = "jdbc:mariadb://localhost:3306/zoldzrt";
        Connection conn = DriverManager.getConnection(url, user, pass);

        String sql = "insert into employees " +
        "(name, city, salary, birth) "+
        "values "+
        "(?, ?, ?, ?)";

        PreparedStatement ps = new conn.prepareStatement(sql);
        ps.setString(1, emp.name);
        ps.setString(2, emp.city);
        ps.setDouble(3, emp.salary);
        ps.setDate(4, java.sql.Data.valueOf(emp.birth));
        ps.execute();

    }
}
```
