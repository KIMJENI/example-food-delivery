![image](https://user-images.githubusercontent.com/487999/79708354-29074a80-82fa-11ea-80df-0db3962fb453.png)

# 예제 - 음식배달



# 서비스 시나리오

![image](https://user-images.githubusercontent.com/55964235/206555962-b2eeb004-1e94-47dc-8aec-2c6509b5333f.png)


기능적 요구사항
1. 고객이 메뉴를 선택하여 주문한다.(ok)
1. 고객이 선택한 메뉴에 대해 결제한다.(ok)
1. 주문이 되면 주문 내역이 입점상점주인에게 주문정보가 전달된다.(ok)
1. 상점주는 주문을 수락하거나 거절할 수 있다.(ok)
1. 상점주는 요리시작때와 완료 시점에 시스템에 상태를 입력한다.(ok)
1. 고객은 아직 요리가 시작되지 않은 주문은 취소할 수 있다.(ok)
1. 요리가 완료되면 고객의 지역 인근의 라이더들에 의해 배송건 조회가 가능하다.(ok)
1. 라이더가 해당 요리를 pick 한후, pick했다고 앱을 통해 통보한다.(ok)
1. 고객이 주문상태를 중간중간 조회한다.(ok)
1. 주문상태가 바뀔 때 마다 카톡으로 알림을 보낸다.(ok)
1. 고객이 요리를 배달 받으면 배송확인 버튼을 탭하여, 모든 거래가 완료된다.(ok)
1. (추가) 고객이 주문 후기를 등록한다.(ok)
1. (추가) 점주는 고객 후기를 확인하다.(ok)




# 체크포인트

## 1. Saga (Pub/Sub)
1. 주문이 들어오면 OrderList에 Sync해준다.

![image](https://user-images.githubusercontent.com/55964235/206559699-6136c674-2d42-4712-8a7d-4221ae31da89.png)


![image](https://user-images.githubusercontent.com/55964235/206559272-a0378462-922c-40a8-a22e-6e7ea9f5acc2.png)


![image](https://user-images.githubusercontent.com/55964235/206559070-1e2f9400-6689-4c9d-828d-28cd93973736.png)


2. OrderList에 주문이 들어오면 자동으로 결제된다.

![image](https://user-images.githubusercontent.com/55964235/206559909-1caac369-96c0-4e08-9642-8afb3e2125f1.png)

![image](https://user-images.githubusercontent.com/55964235/206560072-82841759-9db6-4da9-a3f1-828ec151fcf4.png)

![image](https://user-images.githubusercontent.com/55964235/206560215-260bfc16-967d-4c97-b425-b7d603a7ddc7.png)

## 2. CQRS
주문상태가 변하는 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/55964235/206560603-9c93dad4-6b0d-475e-bd70-da63302fa4a8.png)


![image](https://user-images.githubusercontent.com/55964235/206560472-886b9616-32b0-4257-832e-665f2846ff25.png)

![image](https://user-images.githubusercontent.com/55964235/206560520-ee03cd29-ac1d-48c5-88a3-0bf47631735f.png)


![image](https://user-images.githubusercontent.com/55964235/206561152-8f6b9d38-574d-4f77-9014-ad8394ad65bd.png)


![image](https://user-images.githubusercontent.com/55964235/206561221-a5173d54-76ae-4339-84db-4daa0bc54438.png)


## 3. Compensation/Correlation

![image](https://user-images.githubusercontent.com/55964235/206562384-a267430b-58c3-48b4-869c-f9dcfd56cb6e.png)

## 4. Request/Response
결제가 되어 있고 아직 요리를 시작하지 않았으면 결제 취소를 요청한다.
![image](https://user-images.githubusercontent.com/55964235/206562742-c58fd841-dd43-412b-bdbc-29e7827f022e.png)

![image](https://user-images.githubusercontent.com/55964235/206563571-de812c9f-04d0-4242-93fc-e327e084dbac.png)

## 5. Circuit Breaker

![image](https://user-images.githubusercontent.com/55964235/206564553-5b3d864b-78b1-4dce-81eb-ebccfe98e35c.png)

![image](https://user-images.githubusercontent.com/55964235/206564891-cf606813-64f4-4941-bf94-5b2a0f51a0e2.png)

## 6. Gateway/Ingress

![image](https://user-images.githubusercontent.com/55964235/206565401-8314344f-c1e3-4a25-a738-5d0dff7c5877.png)
![image](https://user-images.githubusercontent.com/55964235/206565441-1477e127-dd42-4274-8c02-3f9e2f0f65d6.png)
