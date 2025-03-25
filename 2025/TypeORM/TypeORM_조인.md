### TypeORM에서 조인을 하는 방법에는 크게 Relations(관계 설정)과 QueryBuilder(쿼리 빌더) 두 가지가 있다.
엔티티 관계(Relations) 사용 → TypeORM이 자동으로 조인해줌
<br>
QueryBuilder 사용 → 직접 쿼리를 작성해서 조인하는 방법

<br>


## Relations (관계 설정)
TypeORM에서는 @OneToOne, @ManyToOne, @OneToMany, @ManyToMany 등의 데코레이터를 사용하여 엔티티 간의 관계를 설정할 수 있고 <br>

엔티티(테이블)끼리 관계를 설정하면 TypeORM이 자동으로 필요한 데이터를 가져온다

예를 들어, **사용자(User)**와 **프로필(Profile)**이 **1:1 관계(One-to-One)**라고 가정하면 다음과 같이 설정할 수 있다.
``` TypeScript
예제:
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @OneToOne(() => Profile, (profile) => profile.user, { eager: true }) 
  @JoinColumn()
  profile: Profile;
}

@Entity()
export class Profile {
  @PrimaryGeneratedColumn()
  id: number;

  @OneToOne(() => User, (user) => user.profile)
  user: User;

  @Column()
  bio: string;
}

```
User 엔티티가 Profile을 1:1로 가지고 있음.

eager: true 덕분에 User 데이터를 가져오면 profile도 자동으로 따라옴.

<br>

## QueryBuilder 사용하여 조인하기
위 방식 대신, 직접 SQL처럼 쿼리를 작성해서 조인할 수도 있다, <br>
QueryBuilder를 사용하면 보다 유연하게 조인을 할 수 있다.
``` TypeScript
const users = await dataSource
  .getRepository(User)
  .createQueryBuilder("user")
  .leftJoinAndSelect("user.profile", "profile")
  .getMany();
```
leftJoinAndSelect("user.profile", "profile")
→ user 테이블과 profile을 조인하여 한 번에 가져옴.

위 코드에서 leftJoinAndSelect( )를 사용하여 user.profile을 함께 가져온다.


<br>


## One-to-One, Many-to-One, Many-to-Many 관계
데이터베이스에서 테이블끼리 관계를 맺는 방식은 크게 세 가지이다

|관계 유형|설명|유형|
|:------:|:----:|:----:|
One-to-One (1:1)|하나의 데이터가 다른 하나의 데이터와 연결됨|``` User ↔ Profile ```(사용자 ↔ 프로필)
Many-to-One (N:1)|여러 개의 데이터가 하나의 데이터와 연결됨|``` Post ↔ User ```(게시글 ↔ 작성자)
Many-to-Many (N:N)|여러 개의 데이터가 여러 개의 데이터와 연결됨|``` Student ↔ Class ```(학생 ↔ 수업)

<br>
<br>

### One-to-One (1:1 관계)

한 명의 유저는 하나의 프로필을 가짐.

@OneToOne()을 사용.

``` TypeScript
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @OneToOne(() => Profile, (profile) => profile.user)
  @JoinColumn() 
  profile: Profile;
}

@Entity()
export class Profile {
  @PrimaryGeneratedColumn()
  id: number;

  @OneToOne(() => User, (user) => user.profile)
  user: User;
}
```

<br>

### Many-to-One (N:1 관계)
여러 개의 게시글(Post)이 한 명의 사용자(User)에게 속함.

@ManyToOne()을 사용.
``` TypeScript
@Entity()
export class Post {
  @PrimaryGeneratedColumn()
  id: number;

  @ManyToOne(() => User, (user) => user.posts)
  user: User;
}
```

<br>

### Many-to-Many (N:N 관계)
한 명의 학생(Student)은 여러 개의 수업(Class)에 등록할 수 있고,
한 개의 수업(Class)도 여러 명의 학생을 가질 수 있음.

@ManyToMany()을 사용.
``` TypeScript
@Entity()
export class Student {
  @PrimaryGeneratedColumn()
  id: number;

  @ManyToMany(() => Class, (classItem) => classItem.students)
  @JoinTable() // 중간 테이블 자동 생성
  classes: Class[];
}

@Entity()
export class Class {
  @PrimaryGeneratedColumn()
  id: number;

  @ManyToMany(() => Student, (student) => student.classes)
  students: Student[];
}
```