# 네이버 블로그 크롤링

네이버 블로그검색 크롤링을 통해 "검색어"가 등장한 블로그를 크롤링

# Update
 * 20-04-02 v1.0.1
    저장파일에 날짜추가  
    del_outword에 제외문자반복변경 추가 :[^-]  
    time_change에 일자 처음 월로 통일  ex) 2017-01-01
    mecab(은전한닢) test 
* 20-04-03 v1.0.1
    1차 통합본제작(2개 함수로 통일 크롤링/아웃풋)
    워드클라우드 추가
    --확인사항--
    모든 마을 13개에서 약 600번대 이후 중복에러 발생 -> drop_duplicate 필수 (원인파악필요)
    del_outword에 \로 시작되는 예외값 계속발생 -> 정규표현식으로 제거 필요 
* 20-04-06 v1.0.2
    크롤링결과 중복값제거 (drop_duplicates)
    결과저장 모두 utf-8
    --확인사항--
    komoran 사용할때 가끔씩 java.lang.NullPointerException: java.lang.NullPointerException 에러발생 회피방법 알아볼것 
* 20-04-07 v1.0.3
    komoran에러 해결 -> 공백으로 있는 문자열 처리
    Okt로 명사+형용사코드 생성

    

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

