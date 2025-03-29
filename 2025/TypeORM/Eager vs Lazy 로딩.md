# Eager vs Lazy 로딩
테이블 관계 데이터를 가져오는 방식에는 두 가지가 있다

|로딩 방식|설명|장점|단점|
|:------:|:-------:|:--------:|:----:|
Eager (즉시 로딩)|연관된 데이터를 자동으로 불러옴 (eager: true)|한 번의 쿼리로 모든 데이터를 가져올 수 있음|항상 데이터를 불러와서 성능이 저하될 수 있음
Lazy (지연 로딩)|데이터를 필요할 때만 불러옴 (lazy: true)|필요할 때만 데이터베이스에서 가져와서 최적화 가능|추가적인 쿼리가 발생할 수 있음

### Eager (즉시 로딩)
eager: true를 설정하면 자동으로 데이터를 가져옴

```TypeScript
@OneToOne(() => Profile, (profile) => profile.user, { eager: true })
profile: Profile;
```
<br>

사용할 때:
```TypeScript
const user = await userRepository.findOne({ where: { id: 1 } });
console.log(user.profile); // 자동으로 profile이 로드됨
```
장점: 한 번의 쿼리로 모든 데이터를 가져올 수 있어서 편리함.

단점: 항상 데이터를 불러와서 불필요한 성능 저하가 발생할 수 있음.


<br>
<br>

### Lazy (지연 로딩)
lazy: true를 설정하면 필요할 때 데이터를 가져옴.
```TypeScript
@OneToOne(() => Profile, (profile) => profile.user, { lazy: true })
profile: Promise<Profile>;
```
<br>

사용할 때:
```TypeScript
const user = await userRepository.findOne({ where: { id: 1 } });
const profile = await user.profile; // profile이 필요할 때 로드됨
```
장점: 필요할 때만 데이터를 가져와서 성능 최적화 가능.

단점: 추가적인 쿼리가 실행되어 성능이 저하될 수도 있음.