# SQL 인젝션이란?

2025.02.24

**웹 애플리케이션의 SQL 쿼리를 조작하여 데이터베이스(DB)에서 비정상적인 동작을 유도하는 해킹 기법**

아래처럼 PHP 코드가 있으면 SQL 인젝션 공격이 가능함

```php
$username = $_POST['username'];
$password = $_POST['password'];

$query = "SELECT * FROM users WHERE username = '$username' AND password = '$password'";
$result = mysqli_query($conn, $query);
```
사용자가 입력한 값을 그대로 SQL 문에 넣기 때문에 위험
<br>

SQL 인젝션 공격 예제
<br>
공격자가 아래처럼 입력하면?
```
아이디: admin  
비밀번호: ' OR '1'='1 
```
<br>

실제 실행되는 SQL 쿼리:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = '' OR '1'='1';
```
'1'='1' → 항상 참(True)이므로 비밀번호 없이 로그인 성공<br>

결과:<br>
비밀번호를 몰라도 로그인됨 (관리자 계정 해킹 가능)<br>
SQL 문을 조작해서 원하는 데이터를 빼올 수도 있음



## SQL 인젝션 방지

SQL 인젝션을 막으려면 Prepared Statement를 사용해야함
 ```
 $stmt = $conn->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->bind_param("ss", $username, $password);
$stmt->execute();
$result = $stmt->get_result();
 ```

  ? 를 사용하면 사용자의 입력이 SQL 문과 분리되어 조작할 수 없음<br>
  즉, ' OR '1'='1 같은 공격이 먹히지 않음