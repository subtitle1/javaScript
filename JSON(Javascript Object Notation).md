# JSON
- 동종 혹은 이종 시스템 간의 데이터 교환을 위한 경량의 데이터교환용 표기법이다.
- 사람이 읽고 쓰기 쉽다.
- 기계 혹은 소프트웨어가 분석하거나 생성하기 쉽다.
  + 분석: json 형식의 텍스트를 객체로 쉽게 변환할 수 있다.
  + 생성: 다른 시스템으로 데이터를 전송하기 위해서 객체를 json 형식의 텍스트로 쉽게 변환할 수 있다.

## JSON의 데이터 구조
- object 표기법
  + 값들의의 `비순서화된 집합`
  + {name:value, name:value}와 같은 형식으로 정의된다
  + name은 String 타입만 가능하다
  + value는 true/false, null, string, number, object, array가 가능하다.
  + 작성예: (이미지는 예전에 자주 하던 게임인 stardewValley의 파일 안에 json 파일이 있어서 일부 캡쳐했다.)
    + {"name":"홍길동", "deptNo":100, "salary":3000000, "married":false}
  + ![image](https://user-images.githubusercontent.com/87356533/146667154-2d5a3c79-c3af-4380-94e0-547361a6812c.png)


- array 표기법
  + 값들의 `순서화된 리스트`
  + [value, value, value]와 같은 형식으로 정의된다
  + name은 String 타입만 가능하다
  + value는 true/false, null, string, number, object, array가 가능하다.
  + 작성예: (이미지는 예전에 자주 하던 게임인 stardewValley의 파일 안에 json 파일이 있어서 일부 캡쳐했다.)
    + [{"no":100, "title":"자바의 정석", "price":35000}, {"no":200, "title":"이것이 자바다", "price":35000}]
  + ![image](https://user-images.githubusercontent.com/87356533/146667092-1971d43e-32c7-4b42-a6b9-6a65818c0f90.png)
