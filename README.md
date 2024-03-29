# 축구선수 정보를 보여주고, 더해서 이들의 스텟을 분석할 수 있는 페이지

## 프로젝트의 목적
* 스텟 분석을 통하여 선수의 몸 값을 예상하고, 이에 대한 소통의 장구를 열어주고 싶었다. 일반인도 구단의 에이전트의 입장에서 이러한 경험해볼 수 있다는 것은 매우 흥미롭다고 생각한다. 또한, 당연스럽게 스포츠에 관심이 많은 사람들일테니 스포츠 용품에 관한 광고도 잘 받아낼 수 있을 것으로 예상된다. 더해서 예측을 잘하는 일반인을 상대로 포인트를 부여하고 이를 사용할 수 있도록하는 페이지를 구현해보고 싶다.

### 사용 기술
* backend - FastAPI
* db - postgreSQL, Redis
* frontend - React

DB의 경우, 사용자의 경험을 향상시킬 수 있도록 상황에 맞춰서 아키텍처를 구현.

# 로컬 환경 세팅

"먼저 backend 디렉토리 안의 dockerfile 실행하여 backend 이미지 생성"

1. 도커 컴포즈 파일 database 부분 환경 변수 설정 후, docker-compose up -d --build 를 활용하여 프로젝트 컨테이너 생성

2. DB 컨테이너만 실행

3. alembic 을 활용하여 모든 테이블 자동 생성
   -> alembic.ini과 .env 안의 url 사용자 설정 후 (localhost)

        alembic revision --autogenerate -m "create all table"
   
        alembic upgrade head 

#크롤링 전에 models.py 의 3번 줄 수정
from database.DBConn import Base -> from DBConn import Base

4. playerDataSet.py 실행 - 크롤링하여 가져온 선수 데이터를 테이블에 넣는 작업

5. playerImage.py 실행 - 선수의 이미지를 크롤링하여 이미지를 저장하는 폴더를 구성하는 작업 (셀레니움 활용)

#로컬 서버 시작 전 models.py 의 3번 줄 재수정
from DBConn import Base -> from database.DBConn import Base

6. DB, Backend 컨테이너 동시 실행 후, http://localhost:8000/docs 를 통하여 스웨거 확인

