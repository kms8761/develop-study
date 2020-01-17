## 시퀄라이즈란
시퀄라이즈는 ORM(Object - relational - Mapping)으로 분류됩니다. ORM은 자바스크립트 객체와 데이터베이스의 릴레이션을 매핑해주는 도구입니다
## 시퀄라이즈 장점
시퀄라이즈 쓰는이유 쿼리를 직접만드는것보다  코드를 작성하거나 읽기에 편리하다


### sequelize 시작
 npm에서 sequelize 패키지를 설치해준다 
-sequelize 명령어 설치 
-config.js등 model에서 설정 
model에서는-index.js이게 중요한파일이다
db를 객체화시켜 index.js에 작성하여 테이블을 연결시켜준다.
config.json의 db내용과 index.js 파일에서 연결해준다
model파일에db 객체에 시퀄라이즈 패키지 넣어준다
모듈 exports db;
인스턴스화 설정해준다 

#### 여기서잠깐
models(=데이터 저장할공간)가 자바스크립트에서 테이블과 일대일로 대응되는 부분
sequelize에서 table =model 이다 workbench에서 안하고 sequelize 패키지를 npm에 설치하면 models가 생기는데 여기에 테이블을 정의하면된다

## sequelize mysql과 비교

#### mysql
INSERT INTO nodejs.users (name, age, married, comment) VALUES ('zero',24,0,'자기소개1');         
#### orm
const { User } = require('../models')

User.create({

  name: 'zero',
  
  age: 24,
  
  married: false,
  
  comment: '자기소개1',
  
});



# 사용예시 

module.exports = sequelize, datatypes =>
return sequelize.defie('comment')

sequelize.define comment라는 테이블이 만들어진다 

index가 가장중요한데 index.js에서 다시 comment.js를 불러준다

select*from nodejs.users 를 모두 조회 user.findall로 조회한다.

attribute 속성을 사용하여 원하는 컬럼만가능


