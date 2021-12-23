```jsp
<div class="container">    
  <div class="row mb-3">
    <div class="col">
      <h1>장바구니</h1>
    </div>
    </div>
    <div class="row mb-3">
    <div class="col">
      <table class="table" id="table-cart-items">
        <thead>
          <tr>
            <th style="width:5%"><input type="checkbox" id="checkbox-toggle-checked" checked/></th>
            <th style="width:40%">상품명</th>
            <th style="width:15%">가격</th>
            <th style="width:15%">수량</th>
            <th style="width:15%">구매가격</th>
            <th style="width:10%"></th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><input type="checkbox" name="itemNo" value="10" checked/></td>
            <td>iphone 13 pro max</td>
            <td class="text-end"><strong id="price-10">1,500,000</strong> 원</td>
            <td><input type="number" min="1" name="amount" id="amount-10" value="1" style="width: 50px;"/> <button data-item-no="10" data-btn="update">변경</button></td>
            <td class="text-end"><strong class="text-danger" id="order-price-10" data-order-price="1500000">1,500,000</strong> 원</td>
            <td><button data-item-no="10" data-btn="delete">삭제</button></td>
          </tr>
          <tr>
            <td><input type="checkbox" name="itemNo" value="20" checked/></td>
            <td>갤럭시z 플립 3</td>
            <td class="text-end"><strong id="price-20">1,700,000</strong> 원</td>
            <td><input type="number" min="1" name="amount" id="amount-20" value="1" style="width: 50px;"/> <button data-item-no="20" data-btn="update">변경</button></td>
            <td class="text-end"><strong class="text-danger" id="order-price-20" data-order-price="1700000">1,700,000</strong> 원</td>
            <td><button data-item-no="20" data-btn="delete">삭제</button></td>
          </tr>
          <tr>
            <td><input type="checkbox" name="itemNo" value="30" checked/></td>
            <td>apple watch 7</td>
            <td class="text-end"><strong id="price-30">600,000</strong> 원</td>
            <td><input type="number" min="1" name="amount" id="amount-30" value="1" style="width: 50px;"/> <button data-item-no="30" data-btn="update">변경</button></td>
            <td class="text-end"><strong class="text-danger" id="order-price-30" data-order-price="600000">600,000</strong> 원</td>
            <td><button data-item-no="30" data-btn="delete">삭제</button></td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="5" class="text-end">총구매가격</td>
            <td class="text-end"><strong id="total-order-price"></strong> 원</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</div>
<script type="text/javascript">
// 아이디를 어떻게 잘 부여하느냐가 자바스크립트 코드의 양을 확 줄여줌
// 조회, 변경의 대상이 되는 것들은 항상 id가 붙는다고 생각하자!
// 연관이 있는 줄은 아이디에 연관된 값이 존재해야 한다 (price-10, order-price-10, amount-10)
  var totalOrderPrice = 0;
  $(':checkbox[name=itemNo]:checked').each(function() {
    var itemNo = $(this).val();
    var orderPrice = $('#order-price-'+itemNo).attr('data-order-price');
    totalOrderPrice += parseInt(orderPrice);
  });
  $('#total-order-price').text(totalOrderPrice.toLocaleString());

  $('button[data-btn="update"]').click(function() {
    // 아이템 번호 조회
    var itemNo = $(this).data('item-no');

    var price = parseInt($('#price-'+itemNo).text().replace(/,/g, ""));
    var amount = parseInt($('#amount-'+itemNo).val());
    var orderPrice = price * amount;

    $('#order-price-'+itemNo).attr('data-order-price', orderPrice).text(orderPrice.toLocaleString());
    updateTotalOrderPrice();
  })

  // 삭제버튼을 클릭하면 해당 아이템을 삭제하기 (내가 클릭한 버튼 중에서 가장 가까운 tr을 찾기)
  $('button[data-btn="delete"]').click(function(){
    $(this).closest('tr').remove();
    updateTotalOrderPrice();
  })

  // 전체 선택/해제 체크박스를 변경하면 장바구니 아이템의 체크박스가 선택/해제되게 하기
  $('#checkbox-toggle-checked').change(function() {
    // 내가 선택한 체크박스의 값을 this와 같게 만들어준다
    $(':checkbox[name=itemNo]').prop('checked', $(this).prop('checked')); // $(this).prop('checked')는 true 혹은 false로 나온다

    updateTotalOrderPrice();
  })

  $(':checkbox[name=itemNo]').change(function() {
    var totalLen = $(':checkbox[name=itemNo]').length;
    var checkedLen = $(':checkbox[name=itemNo]:checked').length;

    // 체크 상태가 같으면 true, 다르면 false 반환하는 값이기 때문에 굳이 if문 안 써도 됨!
    $('#checkbox-toggle-checked').prop('checked', totalLen == checkedLen);

  /* 	
    if (totalLen == checkedLen) {
      $('#checkbox-toggle-checked').prop('checked', true);
    } else {
      $('#checkbox-toggle-checked').prop('checked', false);
    }
  */	
    updateTotalOrderPrice();
  });

  function updateTotalOrderPrice() {
    var totalOrderPrice = 0;
    $(':checkbox[name=itemNo]:checked').each(function() {
      // this -> <input type="checkbox" name="itemNo" value="10" checked/>
      var itemNo = $(this).val();
      // $('#order-price-' +10) -> <strong id="order-price-10" data-order-price="1500000">
      var orderPrice = $('#order-price-'+itemNo).attr('data-order-price');
      totalOrderPrice += parseInt(orderPrice);
    });

    $('#total-order-price').text(totalOrderPrice.toLocaleString());
  };
</script>
```
