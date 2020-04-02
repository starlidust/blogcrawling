# 네이버 블로그 크롤링

네이버 블로그검색 크롤링을 통해 "검색어"가 등장한 블로그를 크롤링

# 주 사용합수 naver_blog_crawling
naver_blog_crawling(keyword, start_num=1, end_num=101,date_option=0,date_from='',date_to='',save = True)

    네이버 블로그 크롤링 함수
    네이버 블로그 검색결과를 크롤링하며, 1페이지당 10개씩을 검색한다
    
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

# 참고
[네이버블로그크롤러](https://github.com/xotrs/naver-blog-crawler)
