
### join에 대해 알아보자

#### 정의:
관계성이 있는테이블 복수의 테이블 결합 하나의 테이블인것처럼 출력

#### 쓰는이유:
복잡한 이슈,데이터 여러개 분할,조인을 통해 데이터결합 더 빠르게 효과적으로 가져오기

### outer join 
매칭되는 행이 없어도 결과를 가져오고 매칭되는 행이 없는경우  null

left join (outer join종류:가장 많이 쓰임)
left조인은 from 기준으로 왼쪽테이블에 오른쪽 내용을 넣는다
ex) select s.name,s.location_id, l.name AS address, l.distance from student AS s LEFT JOIN location AS l ON s.location_id = l.id;

### inner join
조인하는 두개의 테이블 모두에 데이터가 존재하는 행에 대해서만 결과를 가져온다

### outer와 inner 차이
outer 데이터가 없어도 결과에 null을 출력함
inner은 데이터없으면 그냥 행을 결과에서 없애버림
