- **SW 테스팅이란**
	- Software의 **오류를 확인**하는 두 가지 방법 : 1.Inspection 2.Testing 
		-Inspection은 static analysis. code를 분석함(개발 과정 내내 가능함, DB, model, requirements에도 적용 가능)
		-Testing은 dynamic analysis. 실제 프로그램을 돌리며, 버그를 확인(실행버전 있어야 함, 프로그램에만 적용가능)
	- **필요성** : SW가 실생활에 밀접하게 연결되면서, SW 오류 발생시 막대한 피해 발생
		- ex)therac-25 , Nationcal Cancer Institute 방사능 피폭 사고 등
	- Testing은 크게 BlackBox/WhiteBox . Verification/Validation(V&V)로 나눌 수 있음
	- **SW 테스팅 절차**
		- TestCase를 만듦(Test 비용의 80%)->execution by tool ->Comparison,Analysis
	- **진행 과정**
		- Unit Testing - Integration Testing - System Testing - Release Testing - Acceptance Testing
		- 이 중 Unit~System은 Verification, Release~Acceptance는 Validation이라 볼 수 있음
		- Verificaion은 주로 개발팀 내부에서 defect testing 용도로. Validation은 CS팀, 유저 등 개발팀 외부에서 requirements나 needs 충족 여부를 검사함
- **Program Testing**
1. **Unit Testing**
	1. 개요 : 프로그램의 기본이 되는 단위(class, module, function 단위의 테스트를 말함)
	2. 목적 : 각 요소의 완성도가 주된 평가 대상. defect find
	3. 전략 : Brricade module, clean Area 구분
	4. Test Case 생성 전략 : Code based(Structural,White Box) / Spec Base(Black box, functional)
	5. **Spec Based Testing**
		1. 특징 : black box testing.
		2. 장점 : 
			1. 코드 생성 이전에도 TestCase를 만들 수 있음 ->TDD와 찰떡궁합
			2. 코드가 수정되더라도 TestCase를 수정할 필요가 없음
		3. 종류 : Boundary Value Testing / Equivalence Testing / Decision Table Testing
			1. **Boundary Value Testing** : Input Domain의 변수 영역을 활용함
				1. Normal Boundary Value
					- 가장 일반적인 Boundary Value Testing의 형태.
					- 변수 간 관계가 독립적이라 가정하며, 경계값과 그 근처 값을 주로 Test Input으로 삼음
				2. Robust Boundary Value
					- 비정상적 값 역시 Test input으로 삼음.
					- 변수간 관계는 normal boundary처럼 독립적
				3. Worst-Case Boundary Value
					- 변수 간 관계에 의존성을 고려.
					- 정상적 Input 범위 내에서 Boundary 값, 근처 값, 정상값 짝맟춰
				4. Robust Worst-case Boundary Value
					- 변수간 관계 의존성 O / 비정상적 Input 포함 O
					- 비정상, 정상, 경계값, 경계근처 4가지 경우의 수를 조합하여 설정(4*4)
			2. **Equivalance Testing** : 비슷한 결과를 가져오는 input들을 묶어서 class 단위로 하나만. why? 중복을 피하기 위하여(eg. 모듈러 연산 if %5의 경우 5가지 class)
				1. Traditional Equivalance Testing
					- valid, invalid 등 모든 범주에서 class 당 하나씩만 뽑아서 testing
				2. Strong/Weak Equivalance Testing
					- 의존성 개념 추가. Strong이면 의존성 有, weak면 의존성 無
					- Boundary Value의 Worst Case와 비슷한 개념
					- 모두 정상범주 값만 사용
				3. Strong/Weak Robust Equivalance
					- 비정상 범위 역시 Input의 범주.
					- Strong이면 의존성 있고, Weak면 의존성 없는 경우
			3. **Decision Table Based Testing**
				1. 행위의 수행 조건에 따라 적은 decision table을 활용, Test Case를 추출하는 전략, 복잡한 논리구조 파악
				2. 품이 많이 들지만, 결과물의 품질은 아주 훌륭함
				3. Impossible case는 테스트 불필요
		4. testing effort
			1. ![[Pasted image 20240615224731.png]]
		2. .
	6. **Code Based Testing**
		1. 특징 : White Box Testing, Structural Testing이라고도 함
		2. 장점 : 
			1. 코드 생성 이전에도 TestCase를 만들 수 있음 ->TDD와 찰떡궁합
			2. 코드가 수정되더라도 TestCase를 수정할 필요가 없음
		3. 종류 : PathBasedTesting / Data flow testing / slicing
			1. **Control Flow Graph** : path Based Testng의 기본이 되는 그래프. Node(basic Block), Edge로 구성되어 있으며 DU, branch등에 대한 설명이 추가되기도 함. CFG를 기반으로 Coverage를 정하는 게 code based Generating의 특징임. 다만, condition이 하나씩만 쓰인 조건문은 모든 커버리지가 일치함
				1. Statement Coverage
					- 모든 문장을 적어도 한 번 체크하는 커버리지.
					- TDD 구성시 쉽게 충족 가능
					- 하지만, 실제로는 infeasible path로 인해 달성 불가능
					- 가장 널널한 조건
				2. Decision(Branch) Coverage
					- CFG의 모든 브랜치를 적어도 한 번 방문하도록 path 설정해야 함.
					- 현업에서는 75% 이상의 브랜치 커버리지를 만족하라는 게 일반적
					- condition coverage와의 우열 관계는 말할 수 없음
					- eg. 최소로 구성할 경우 or문의 경우(TT,FF), (TF,FF),(FT,FF)가 가능/ and문의 경우(TT,FT),(TT,TF),(TT,FF)
				3. Condition/Decision Coverage
					- 조건문 내부에 모든 컨디션과 모든 브랜치를 만족해야 하는 커버리지.
					- eg. or문 and문 모두 최소로 구성할 땐 (TT,FF)만 가능
				4. MC/DC(Modified Condition/Decision Coverage)
					- 다른 조건식과 독립적 개별 조건식이 전체에 영향을 주는 경우를 골라내는 기법.
					- 안전이 중요한 방산, 자동차, 의 업계에서 주로 사
					- eg)or의 경우 유니크 path인 FF에서 하나씩 바꿨을 때 결과인 TF,FT를 모두 추가 / and의 경우 유니크 path인 TT에서 컨디션을 바꿨을 때 결과가 바뀌는 FT, TF를 추가.
			2. **data-flow testing** : Def - Use간의 관계를 통해 Data Flow를 테스트하는 방식. Data flow 관점에서 꼭 체크해야 하는 부분을 나타냄. 일반적으로 CFG보다 많은 비용이 들어감
				1. Def : 변수에 새로 값이 할당되거나 formal parameter로 사용될 때. Use : 변수가 실인자, 피연산자로 사용될 때
				2. 조건 :
					1. 한 Statement에서 Def-Use가 일어날 경우. 그건 다른 곳에 영향이 없기에 DU pair가 아님.
					2. 루프에서 use 이후 def가 올 경우 DU-pair임. 검사 必
					3. Def와 Use 사이 새로운 Def가 있을 경우는 제
				3. 계층
					1. ![[Pasted image 20240615223628.png]]
			3. **Slice based testing**
				1. 기능의 실행 시 꼭 필요한 파트들만 나누어 확인하는 전략.
		4. numbers of test case
	7. **SW testing Technique**
		1. Regression Testing : change 발생시 영향을 체크하는 테스트
		2. Conformance Testing : requirements나 constrain등 충족 여부 테스트
		3. Random Testing : T.C를 만들지 않고, Input을 랜덤으로. 시스템의 critical point 확인이 목적
		4. concolic testing : 좀 더 세련된 Critical Point 확인 방식. 각 path 별로 필요한 input의 범주를 규정한 뒤 테스트를 진행함.
		5. Mutation Testing : Test Case의 평가를 위한 테스팅. 고의적으로 에러(문장 삭제, 복사, 삽입 / 불리언 반대로 등)를 넣은 뒤, 해당 에러를 얼마나 잡아내는지로 Test Case의 점수를 매김.
	8. Unit Testing 비용 분석
		1. ![[Pasted image 20240615225435.png]]
		2. ![[Pasted image 20240615225450.png]]
	9. TDD
		1. Test Driven Development의 약자
		2. 필요성 : 프로그래머들은 테스트를 지루한, 남들의 일로 생각함. TDD는 그러한 사고방식을 전환할 수 있는 기회
		3. Test Case 추출 -> Test Case 기반 Test 환경 구축 -> 빈 코드로 테스트(all fail시 성공) -> 리얼 코드 작성 -> 올 테스트 -> 코드 클린업
		4. 장점 
			1. regression testing 쉬워짐
			2. 모든 코드가 적어도 한 번씩은 테스팅됨
			3. incremental 개발과 합쳐질 시, 디버깅이 쉬워짐(error원인이 뚜렷함)
			4. TDD 검사 결과를 그대로 문서로 사용 가능
		5. Junit
			1. Beck and Gamma 개발
			2. Unit Test 자동화 툴
			3. 장점
				1. main 함수 건드리지 않고 test 가능
				2. import, test class 선언 필수적
				3. 문법
					1. ![[Pasted image 20240615225938.png]]
					2. ![[Pasted image 20240615230001.png]]
2. Integration Testing
	1. 
3. System Testing
4. Embedded Testing

