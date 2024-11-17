# TeamProject

이준현 [김남규, 배창민, 최성현, 장진천] 조 백엔드 파트 깃허브입니다.

백엔드 파트: 최성현, 배창민

* 최근 데이터베이스에 보안문제로 데이터가 모두 날아가 데이터 수가 적습니다...
* application-aws.properties 파일에 민감한 정보가 포함되어 깃허브엔 포함되지 않았습니다.
* Redis가 설치된 환경에서 사용 가능합니다.
* 페이지 관련 기능은 기능동작 테스트용입니다. 현재 사용가능하지 않습니다.
* 배포는 AWS에서 진행
  
<검수 이후 추가된 기능입니다.>

1. 혐오표현 감지
 - PyTorch를 통해 Deep-Learning 모델을 만들어 혐오표현을 감지해 리뷰 생성에 제한을 둠
 - beomi/KcELECTRA-base-v2022 모델을 이용해 학습함
 - 관련 파일은 https://github.com/ChoiSHy/HaterSeeker 에서 확인할 수 있습니다.
 - 과정
   Client(Review 저장 요청)
       -->
         Spring api server(AWS EC2)
             -->
               Fast api server (Local, 리뷰 혐오표현 판단)
             -->
         Spring api server(AWS EC2, 데이터 저장)
       -->
   Client(결과 전달)


2. 포인트 제도
 - 리뷰 작성시 5포인트씩 적립
 - 자신의 리뷰에 좋아요 추가시, 1포인트 적립
 - 자신의 리뷰에 싫어요 추가시, 1포인트 감소

3. 리뷰 테러 방지
 - 리뷰 작성시, 해당 메뉴 리뷰 작성 후 24시간 지나야 작성 가능

4. 추천 시스템
 - 사용자의 리뷰 기록에 따른 추천 메뉴 선별
 - Jaccard 유사도를 통해, 기록이 비슷한 다른 사용자들의 리뷰 남긴 메뉴들을 추천
 - Jaccard 유사도 : |A ∩ B| / |A ∪ B|
   ex)
      • 사용자 의 구매 항목 집합 A = {1 2 3 4 5}
      • 사용자 의 구매 항목 집합 B = {1 2 3 6 7 9}
      • A B = 3 / 8 와 의 유사도
      • A = 6, 7, 9

5. 사용자가 자주 찾는 카테고리 선별
 - 사용자가 남긴 리뷰 숫자 외에도, 높은 점수를 남긴 카테고리들을 보여줌
