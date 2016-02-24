# 콩랭 (KongLang)

콩랭은 하단의 규칙을 따르는 고수준의 난해한 프로그래밍 언어입니다.  
이 언어는 (느슨하게) 튜링 완전한 언어입니다.

## 숫자 리터럴 표기에 관한 규칙

  1. 모든 숫자 리터럴은 2의 사칙연산을 통해 표기해야 합니다.  
    - 0: 2 - 2  
    - 1: 2 / 2  
    - 3: 2 + 2 / 2  
    - 7: 2 * 2 * 2 - 2 / 2  
  2. 사칙연산의 우선순위는 수학에서의 순서와 같습니다.
  
## 메모리에 관한 규칙

  1. `#`은 표준 입/출력을 뜻하는 가상의 메모리 주소입니다.
	
	예제: 0번 메모리의 값을 출력하기
	`<2 - 2> } (#)`
	
	예제: 0번 메모리에 사용자가 입력한 문자의 유니코드 값 넣기
	`(2 - 2) { <#>`

  2. 메모리 주소는 `#`, 0 혹은 임의의 자연수여야 합니다.  

## 오류에 관한 규칙

  1. 숫자 리터럴 표기에 2와 사칙연산 기호 외에 다른 문자, 기호, 숫자가 들어갔을 경우 컴파일 오류와 함께 코드의 실행이 중지됩니다.  
  2. 메모리 주소가 `#`, 0 또는 자연수가 아닐 경우, 컴파일 오류와 함께 코드의 실행이 중지됩니다.  
  3. 각 명령어가 줄바꿈 문자(LF)로 구분되어 있지 않을 경우, 컴파일 오류와 함께 코드의 실행이 중지됩니다.  
  4. 잘못된 구문의 명령 줄의 경우, 컴파일 오류와 함께 코드의 실행이 중지됩니다.  
  
    예제:
      - `(메모리 주소) [`와 `]`의 짝이 맞지 않는 경우  
      - `(메모리 주소) {` 뒤에 `숫자`가 누락된 경우  
      - 그 외에 각 명령어가 제시하는 조건을 충족하지 못하는 경우  


## 값을 대입하는 명령어

  1. `(메모리 주소) { 숫자` 혹은 `숫자 } (메모리 주소)`를 이용하여 해당하는 메모리에 숫자를 대입할 수 있습니다.  

      예제: 0번 메모리에 숫자 1 넣기  
		  `(2 - 2) { 2 / 2`  
		
## 숫자를 반환하는 명령어

  1. `<메모리 주소>`는 해당 메모리 주소의 값을 반환하며, 이는 숫자로 취급합니다.  
  
    예제: 0번 메모리에 숫자 3을 더하기  
		`(2 - 2) { <2 - 2> + 2 + 2 / 2`  
		
## 흐름을 제어하는 명령어
  1. `<메모리 주소> [`는 해당 메모리 주소의 값이 0인 경우 짝이 되는 `]`까지의 내용을 실행합니다.  
  2. `]`는 짝이 되는 `<메모리 주소> [`으로 되돌아갑니다.  
  
    예제: 0번 메모리가 0일 때 계속 반복하기
    
```
  <2 - 2> [  
	  코드  
  ]  
```

## FAQ
### `<>`와 `()`가 헷갈려요!

  1. 송신자 - `<메모리 주소>`: 값을 내보냅니다. 메모리의 값을 내보내려면 `<메모리 주소>`, 콘솔 입력 값을 내보내려면 가상의 메모리 주소를 이용한 `<#>`을 사용합니다.
  
  2. 수신자 - `(메모리 주소)`: 값을 받습니다. 메모리에 값을 받으려면 `(메모리 주소)`, 콘솔의 값을 받으려면 가상의 메모리 주소를 이용한 `(#)`을 사용합니다.
  
  3. 표준 입출력에 대한 정리:  
    수신자 = 값을 받는다. = 저장한다. -> 콘솔에 값을 내보낸다.  
    송신자 = 값을 내보낸다. = 꺼내온다. -> 콘솔입력을 받는다.  

### 가상의 메모리 주소라는 개념이 이해가 안가는데요?

가상의 메모리라는 것은 입/출력이 가능하며, 실제로는 메모리가 아닌 무언가를 메모리의 형태만 따와서 쓰이는 것이며, 가상의 메모리 주소는 여기에 부여된 주소입니다.
