# AJAX
- 비동기식 자바스크립트 `XML(Asynchronous Javascript And XML)`의 약자이다.
- javScript를 사용한 비동기 통신, 클라이언트와 서버 간에 XML 데이터를 주고받는 기술이다.

## 동기식 통신과 비동기식 통신의 차이
- ***동기식 통신***
  + 일반적인 http 통신
  + 요청을 보내는 순간부터 응답이 올 때까지 새 요청을 보낼 수 없다
  + `화면 전체가 리로딩`된다
  + `응답이 올 때까지 대기 상태`이다
  + 요청 -> 응답 순서로만 동작한다
  + ***html이 주로 응답***으로 온다
  + 브라우저가 요청을 주고 응답을 받는 주체가 된다
  
- ***비동기식 통신***
  + html 페이지 전체가 아닌, `일부분만 갱신하기 위한 통신 방식`
  + 컨텐츠가 화면에 표시되지 않는 구간이 존재하지 않는다
  + `응답에 상관없이 언제든 새로운 요청`을 할 수 있다 (기존의 서버는 응답이 올 때까지 기다려야 했다)
  + 사용자가 동작(마우스 클릭, 이동, 값 입력 등등)하면 event가 발생한다
  + XHR(XMLHttpRequest)가 요청을 주고 응답을 받는 주체가 된다
  + xml, json, 텍스트가 주로 응답으로 온다
  + ajax는 XHR 객체를 통해 서버에 request를 한다. <br> Json이나 xml 형태로 필요한 데이터만 받아 갱신하기 때문에, 웹페이지의 속도 향상되며 자원 또한 아낄 수 있다.
 
## AJAX 예제
```java
@WebServlet("/product/list.hta")
public class ProductListController extends HttpServlet {
  @Override
  protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    List<Product> productList = List.of(new Product(100, "갤럭시", "삼성", 15000000, 1300000, true),
				new Product(200, "Iphone 13 Pro", "애플", 16000000, 1400000, true),
				new Product(300, "apple watch", "애플", 600000, 500000, false));
        
    Gson gson = new Gson();
    // 위에서 생성한 더미데이터 전달
    String jsonText = gson.toJson(productList);
    response.setContentType("application/json; charset=UTF-8");
    
    PrintWriter writer = response.getWriter():
    writer.write(jsonText);
    writer.flush();
  }
}
```
```jsp
<div class="container">    
  <div>
    <div class="row mb-3">
      <div class="col">
        <h1>상품 리스트</h1>
      </div>
    </div>
  </div>
  <div class="row mb-2">
    <div class="col text-end">
      <button class="btn btn-primary" onclick="runAjax()">조회</button>
    </div>
  </div>
  <div class="row mb-3">
    <div class="col">
      <table class="table" id="table-products">
        <thead>
          <tr>
            <th>번호</th>
            <th>상품명</th>
            <th>제조회사</th>
            <th>가격</th>
            <th>할인가격</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table>
    </div>
  </div>
</div>
<script>
  // XMLHttpRequest로 웹서버와 비동기식 통신하기
  function runAjax() {
    // 1. XMLHttpRequest 객체를 생성한다
    var xhr = new XMLHttpRequest();
    
    // 2. xhr 객체의 상태가 변할 때마다 실행할 메소드를 등록한다
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4 && xhr.state == 200) {
        // 5. XMLHttpRequest의 responseText 프로퍼티에 저장된 응답데이터 가져오기
        var jsonText = xhr.responseText;
        
        // 6. jsonText를 자바스크립트 객체/배열로 변환하기
        var products = JSON.parse(jsonText);
        
        // 7. 응답데이터로 HTML 컨텐츠 생성하기
        var htmlContent = "";
        products.forEach(item => {
          htmlContent += "<tr>";
          htmlContent += "<td>"+item.no+"</td>";
          htmlContent += "<td>"+item.name+"</td>";
          htmlContent += "<td>"+item.company+"</td>";
          htmlContent += "<td>"+item.price+"</td>";
          htmlContent += "<td>"+item.discountPrice+"</td>";
          htmlContent += "</tr>";
        });
        
        var tbody = document.querySelector("#table-products tbody");
        tbody.innerHTML = htmlContent;
      }
    };
    
    // 3. XMLHttpRequest 객체 초기화
    xhr.open("GET", "/script2/product/list.hta");
    
    // 4. 웹서버로 요청 보내기
    xhr.send();
</script>
```

## XMLHttpRequest의 readyState 프로퍼티
- readyState 프로퍼티는 HTTP 요청의 처리 상태에 따라서 0~4까지 값이 변한다.
- onreadystatechange는 readyState 프로퍼티의 값이 변할 때마다 발생하는 이벤트이다.
- xhr.onreadystatechange = function()은 이벤트가 발생할 때마다 실행될 함수를 등록한 것이다.
- readyState : 진행상태
    + 0: open() 메소드를 수행하기 전 (객체 생성)
    + 1: loading 중 (객체 초기화 완료)
    + 2: loading 완료 (서버에게 요청 보냄)
    + 3: Server 처리중 (서버에서 요청을 처리하기 시작함)
    + 4: Server 처리완료 (응답 완료)
- status
  + 200: 성공
  + 403: 접근 금지
  + 404: 없음.
  + 500: 구문 에러
- 응답코드의 구분: https://github.com/subtitle1/JSP/blob/main/2.%20HTTP.md
