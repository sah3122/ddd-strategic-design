# 키친포스

## 요구 사항

### 상품

* 상품을 등록할 수 있다.
* 상품의 가격이 올바르지 않으면 등록할 수 없다.
    * 상품의 가격은 0 원 이상이어야 한다.
* 상품의 목록을 조회할 수 있다.

### 메뉴 그룹

* 메뉴 그룹을 등록할 수 있다.
* 메뉴 그룹의 목록을 조회할 수 있다.

### 메뉴

* 1 개 이상의 등록된 상품으로 메뉴를 등록할 수 있다.
* 메뉴의 가격이 올바르지 않으면 등록할 수 없다.
    * 메뉴의 가격은 0 원 이상이어야 한다.
    * 메뉴에 속한 상품 금액의 합은 메뉴의 가격보다 크거나 같아야 한다.
* 메뉴는 특정 메뉴 그룹에 속해야 한다.
* 메뉴의 목록을 조회할 수 있다.

### 테이블

* 테이블을 등록할 수 있다.
* 테이블의 목록을 조회할 수 있다.
* 빈 테이블 설정 또는 해지할 수 있다.
* 단체 지정된 테이블은 빈 테이블 설정 또는 해지할 수 없다.
* 주문 상태가 조리 또는 식사인 테이블은 빈 테이블 설정 또는 해지할 수 없다.
* 방문한 손님 수를 입력할 수 있다.
* 방문한 손님 수가 올바르지 않으면 입력할 수 없다.
    * 방문한 손님 수는 0 명 이상이어야 한다.
* 빈 테이블은 방문한 손님 수를 입력할 수 없다.

### 단체 지정

* 2 개 이상의 빈 테이블을 단체로 지정할 수 있다.
* 단체 지정은 중복될 수 없다.
* 단체 지정을 해지할 수 있다.
* 단체 지정된 테이블의 주문 상태가 조리 또는 식사인 경우 단체 지정을 해지할 수 없다.

### 주문

* 1 개 이상의 등록된 메뉴로 주문을 등록할 수 있다.
* 빈 테이블에는 주문을 등록할 수 없다.
* 주문의 목록을 조회할 수 있다.
* 주문 상태를 변경할 수 있다.
* 주문 상태가 계산 완료인 경우 변경할 수 없다.

## 용어 사전

| 한글명 | 영문명 | 설명 |
| --- | --- | --- |
| 메뉴 그룹 | Menu Group  | 추천 메뉴, 한 마리 메뉴 등 메뉴를 그룹화 할 수 있다. |
| 메뉴 | Menu | 후라이드 치킨, 양념 치킨 세트 등 판매 가능한 메뉴이다. (이름, 가격, 메뉴 그룹 정보, 포함 상품 정보) |
| 포함 상품 | Menu Product | 메뉴에 포함되어 있는 상품 정보. |
| 상품 | Product | 판매 가능한 상품 정보(이름, 가격) |
| 테이블 | Order Table | 매장 내부에 배치 되어 있는 좌석. |
| 단체 지정 | Table Group | 단체 손님들을 하나의 테이블로 묶어 주문을 받을수 있도록 한다. |
| 주문 | Order | 손님이 선택한 메뉴, 테이블 정보를 포함 하고 있다. <br> 주문은 주문 상태를 가지며 주문의 초기 상태는 요리중 상태이다. |
| 상세 주문 내역 | Order Line Item | 주문에 포함되어 있는 메뉴, 수량을 나타낸다. |
| 주문 상태 | Order Status | 주문 된 메뉴의 상태. 요리중, 식사중, 식사 완료 상태로 구분 가능하다. |
| 요리중 | COOKING | 주문이 처음 들어왔을때 요리를 시작하는 상태. |
| 식사중 | MEAL | 손님들이 식사를 하는 상태. |
| 식사 완료 | COMPLETION | 손님들이 식사를 끝낸 상태. |


## 모델링

* 상품(Product)
    * 상품번호, 이름, 금액으로 구성된다.
    * 상품을 등록 한다.
        * 상품의 가격은 0 원 이상이어야 한다.
    * 상품 목록을 조회 한다.
    
* 포함 상품(Menu Product)
    * 포함 상품(Menu Product)은 포함 상품 번호, 메뉴번호, 상품번호, 수량으로 구성된다.
    
* 메뉴(Menu)
    * 메뉴번호, 이름, 금액, 메뉴 그룹 번호, 포함 상품(Menu Product)들로 구성된다.
    * 메뉴를 등록 한다.
        * 적어도 1개 이상의 상품으로 구성되어야 한다.
        * 메뉴의 가격은 0원 이상이어야 하고 포함 상품들의 가격의 합보다 적거나 같아야 한다.
        * 등록된 메뉴 그룹에 포함되어야 한다.
    * 메뉴 목록을 조회 한다.
    
* 메뉴 그룹(Menu Group)
    * 메뉴 그룹 번호, 메뉴 그룹 이름으로 구성 된다.
    * 메뉴 그룹을 등록한다.  
    * 메뉴 그룹 목록을 조회 한다.
    
* 테이블(Table)
    * 테이블 번호, 단체 지정 번호, 손님 수, 빈 테이블 여부로 구성된다.
    * 테이블을 등록 한다.
        * 초기 상태는 빈 테이블 및 단체 지정되지않은 상태이다.
    * 테이블의 상태를 변경 한다.
        * 빈 테이블 설정 / 해지 할 수 있다.
        * 주문상태가 계산 완료(COMPLETION) 상태이어야 한다.
        * 단체 지정 테이블은 상태를 변경할 수 없다.
    * 테이블의 손님 인원수를 변경한다.
        * 0명 이상의 인원수만 변경 가능하다.
        * 빈 테이블은 변경 할 수 없다.
    * 테이블 목록을 조회 한다.
    
* 단체 지정(Table Group)
    * 단체 지정 번호, 생성 시간, 테이블(OrderTable)들로 구성된다.    
    * 여러 테이블을 하나의 테이블로 단체 지정 한다.
        * 2개 이상의 테이블을 단체 지정할수 있다.
        * 등록된 테이블만 가능하다.
        * 이미 단체 지정이 되었거나 빈 테이블이 아니면 단체 지정 할 수 없다. 
    * 단체 지정을 해제 한다.
        * 단체 지정을 해제하는 경우 데이블의 단체 지정 번호를 삭제한다.
        * 주문 상태(Order Status)가 계산 완료(COMPLETION) 상태이어야 한다.
        
* 주문(Order)
    * 주문번호, 주문 테이블 번호, 주문 상태(Order Status), 주문 시간. 상세 주문 내역(Order Line Item)들로 구성된다.
    * 주문을 등록 한다.
        * 1개 이상의 등록된 메뉴가 포함되어야 한다.
        * 빈 테이블은 주문 할 수 없다.
        * 주문의 초기 상태는 요리 중(COOKING) 상태이다.
    * 주문 상태(Order Status)를 변경 한다.
        * 주문 상태가 계산 완료(COMPLETION) 인 경우 변경 할 수 없다.
    * 주문 목록을 조회 한다.

* 주문 상태(Order Status)
    * 주문상태는 요리중(COOKING), 식사중(MEAL), 계산완료(COMPLETION) 상태를 나타낼수 있다.
    
* 상세 주문 내역(Order Line Item)
    * 상세 주문 내역은 상세 주문 내역 번호, 주문 번호, 메뉴 번호, 주문 수량으로 구성된다.
