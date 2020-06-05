# 네이버 블로그 크롤링

네이버 블로그검색 크롤링을 통해 "검색어"가 등장한 블로그를 크롤링

# Update
 * 20-04-02 
    저장파일에 날짜추가  
    del_outword에 제외문자반복변경 추가 :[^-]  
    time_change에 일자 처음 월로 통일  ex) 2017-01-01
    mecab(은전한닢) test 
* 20-04-03 
    1차 통합본제작(2개 함수로 통일 크롤링/아웃풋)
    워드클라우드 추가
    --확인사항--
    모든 마을 13개에서 약 600번대 이후 중복에러 발생 -> drop_duplicate 필수 (원인파악필요)
    del_outword에 \로 시작되는 예외값 계속발생 -> 정규표현식으로 제거 필요 
* 20-04-06 
    크롤링결과 중복값제거 (drop_duplicates)
    결과저장 모두 utf-8
    --확인사항--
    komoran 사용할때 가끔씩 java.lang.NullPointerException: java.lang.NullPointerException 에러발생 회피방법 알아볼것 
* 20-04-07 
    komoran에러 해결 -> 공백으로 있는 문자열 처리
    Okt로 명사+형용사코드 생성

* 20-04-20 2차배포본
    형용사추가, 불용어(stopword) 밖으로 꺼냄, 다수의 날짜로 크롤링가능
    네트워크분석 시도(아직고민중)
* 20-04-21 2차배포본, 네트워크분석 함수화
    네트워크분석 이해 완료, 2차배포본에서 월간단위로 검색가능하게 함수추가
    시각화를 위한 방안모색중 1안 시도 
* 20-04-22 카테고리화,분할화
    상위 30개 단어를 카테고리화하고 비중계산
    crawling, (merging),tokenize, visualization, 분할
* 20-05-08 저장방식변경  
    기존 "날짜_키워드_길이_기간" 
    ex) 2020-05-07_물치리 +강원도_9_20160501 ~ 20160531 -> 변경 "기간_키워드_길이_날짜" ex) 20160501 ~ 20160531_물치리 +강원도_9_2020-05-07
* 20-06-05 각 진행과정 분할 등  
    workflow에 있는 내용으로 분할작업진행   
    크롤링/크롤링종합/토큰화/토큰화종합/활용 5단계로 분류됨  
    git에 올라온 파일 정리 
    간 단계별 저장위치, 저장방식 f-sting으로 변경 (기존: .format)


    

# 주 사용함수 naver_blog_crawling
naver_blog_crawling(keyword, start_num=1, end_num=101,date_option=0,date_from='',date_to='',save = True)

    네이버 블로그 크롤링 함수
    네이버 블로그 검색결과를 크롤링하며, 1페이지당 10개씩을 검색한다
```    
    keyword : string
     검색하고 싶은 키워드를 넣는다 
     "keyword +필수어" 형태로 필수단어 추가 가능
    start_num : int (default = 1) 
     시작할 위치 1로 끝나는 단위 추천
    end_num : int (default = 101)
     끝나는 위치 1로 끝나는 단위 추천
    date_option : int (default = 0)
     주어지는 숫자에 의해 검색방법이 변경됨
     0 : 전체, 2 : 1일, 3 : 1주, 4 : 1개월, 6 : 6개월, 7 : 1년, 8 : 기간지정
    date_from : YYYYMMDD (default = "")
     date_option이 8일때 사용 검색 시작일자를 지정
    date_to : YYYMMDD (default = "")
     date_option이 8일때 사용 검색 마지막일자를 지정
    save : bool (default = True)
     csv로 저장 여부 결정
```
# 참고
[네이버블로그크롤러](https://github.com/xotrs/naver-blog-crawler)

