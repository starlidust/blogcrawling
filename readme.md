# 네이버 블로그 크롤링

네이버 블로그검색 크롤링을 통해 "검색어"가 등장한 블로그를 크롤링

## 사전설치
* 크롤링(beautifiulsoup, request)  
!pip install beautifulsoup4  
!pip install requests  
* 자연어 처리(konply, ckonlpy)  
!pip install konply  
* 시각화(wordcloud, networkx)  
!pip install wordcloud  
!pip install networkx  
!pip install tqdm (작업과정 시각화)  

## 사용법
작성한 코드의 크롤링은 총 5단계로 이뤄져 있습니다.  
코드의 흐름은 workflow를 참조하면 편리합니다.  

1단계에서는 keyword별로 원하는 단어를 크롤링합니다.  
<불용어처리해야하는 부분은 stopword(cp949).xlsx 파일에 미리 작성해둡니다.>  

2단계에서는 크롤링된 파일들을 하나로 병합합니다  
<광고 또는 불필요한 결과를 배제하기 위해 filter_word를 작성합니다.>  

3단계에서는 크롤링된 결과를 토큰화 합니다.  
<업데이트되어있지 않은 신조어의 경우 단어사전에 추가해줍니다.>  
※ 사용자정의 사전 추가가 편리한 ckonlpy를 사용했으나, Okt 사용을 권장합니다. (ckonlpy는 twitter사용)  

4단계는 토큰화한 결과를 다시 병합합니다.  
<keyword가 여러개인 경우 하나의 단어로 통합해주는 과정이 들어가 있습니다.>  

5단계는 시각화/활용 단계입니다.  
워드클라우드, 네트워크분석, 검색어 변화추이 3가지로 나눠져있습니다.  
워드클라우드는 연도별로 워드클라우드를 그리고 gif형태로 합칠 수 있습니다. (각 연도별 png도 가능)  
네트워크분석은 워드클라우드와 동일하게 결과를 gif형태로 합칠 수 있습니다.  
검색어변화추이 연도별 가장 많이 등장한 단어를 상위 15개 단어를 출력하고 연도별 변화를 측정합니다.

각 단계는 1번부터 차례로 실행하되   
추가단어사전, filtering을 지속적으로 진행해야하므로   
추가단어가 발생시 3단계부터 재실행하고   
filtering을 진행시 4단계부터 진행하면 됩니다. (4단계에서도 filtering 진행)  
2단계에서 filter를 진행하게되면 3단계의 연산시간이 줄어듬으로 filter단어가 증가하게되면 2단계부터 재실행을 추천합니다.


## 예상오류
1. 검색결과와 다른 형태의 결과 출력    
    "양양군 동호"를 검색하고 싶었으나, "동호회"가 더 많이 검색되었습니다.  
    따라서 필수단어를 넣는 것이 중요하며, 결과에 대한 filtering이 중요  
2. JAVA hip Memory error
    3단계 진행중에 자바메모리 에러가 발생할 수 있습니다.  
    현재 (max_heap_size=5120)로 hip_size를 5기가로 배정해두었고 1만 5천건 단위로 분할하여 작업을 진행   
    혹시 메모리 에러가 발생하면 hip_size를 조절하거나, 분할 단위를 더 축소하는 것이 좋을듯 합니다.
3. 검색한 결과 수 대비 결과량이 적을 때 
    블로그 내부적으로 내용을 복사해가는 것을 방지해놨기 때문으로 추정. 이에 딱히 대처방법은 없을것으로 보임

# 주요 함수 naver_blog_crawling
```python 
def naver_blog_crawling(keyword, start_num=1, end_num=101, date_option=0, date_from='', date_to='', save=True):
    '''네이버 블로그 크롤링 함수
    네이버 블로그 검색결과를 크롤링하며, 1페이지당 10개씩을 검색한다
    
    Parameters
    ----------
    keyword(string) : 검색하고 싶은 키워드를 넣는다 "keyword +필수어" 형태로 필수단어 추가 가능
    start_num(int) : (default = 1)  시작할 위치, 1로 끝나는 단위 추천
    end_num(int) : (default = 101) 끝나는 위치, 1로 끝나는 단위 추천
    date_option(int) : (default = 0) 주어지는 숫자에 의해 검색방법이 변경됨
                         0 : 전체, 2 : 1일, 3 : 1주, 4 : 1개월, 6 : 6개월, 7 : 1년, 8 : 기간지정
    date_from(YYYYMMDD) : (default = "") date_option이 8일때 사용 검색 시작일자를 지정
    date_to(YYYYMMDD) : (default = ""), date_option이 8일때 사용 검색 마지막일자를 지정
    save(bool) : (default = True)csv로 저장 여부 결정
    
    Returns 
    -------
    crawling_df : DataFrame
        post_dates title  full_text         url
      0 2010-01-01 title  [full_text]       http://blog.naver.com/PostView.nhn?blogId=wend...  
    
    real_length : int
        crawling_df의 row수 
    '''
```

# 업데이트 종료후 후기
    꾸준하게 업데이트 해왔던 코드기 때문에 다소 애착이 있고 나중에 활용할 기회가 다시금 있기를 바람.  
    아쉬운 점은 Okt의 사용자사전을 사용법을 잘 익히지 못해서 적용을 못했다는 점
    그리고 텍스트마이닝은 정말 해도 해도 끝이 없다는 느낌...
    
    끝나도 끝이아니다...!

# 참고
[네이버블로그크롤러](https://github.com/xotrs/naver-blog-crawler)

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
    형용사추가, 불용어(stopword.xlsx) 밖으로 꺼냄, 다수의 날짜로 크롤링가능
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
    검색시 연도별, 월별 검색가능하게 변경 (검색결과 1000건이상 불가)
    간 단계별 저장위치, 저장방식 f-sting으로 변경 (기존: .format)
* 20-06-08 각 단어에 따른 불용어 사전(custom_sw.json) 추가
    특정단어에 따른 불용어가 발생할 것으로 추정하여 추가 ex) keyword : "양양", stopword : "양양군","강원도" 
* 20-06-09 konply(OKT) -> ckonply로 대체  
    사용자정의사전(단어사전.xlsx) 이용하기 위함  
    토큰화종합시 filtering(filtering.xlsx) 추가 [본디 크롤링종합에서 진행하나, 보다 확실히 하기 위함]  
    토큰화종합시 종합된 결과 확인가능한 DataFrame 생성  
    워드클라우드 gif파일로 저장방식 추가 [가시성 상승]  
    워드클라우드 주변공백 제거 (bbox_inches='tight')  
* 20-06-15 docstring 작성  
    각 단계별 함수에 대한 docstring 작성  
    함수화되어있지 않은 부분 수정  
    네트워크분석 최적화진행  
* 20-06-17 네트워크분석   
    네트워크분석 최적화 진행  
    1차적으로 마무리  
* 20-06-19 4단계 수정
    merge할 keyword가 없는 경우 누락되는 경우 수정

* 21-01-12 블로그 검색방식이 변경됨  
기존 page넘어가는 방식에서 드래그로 글이 추가되는 형태로 변경.  
따라서 상호작용이 가능한 셀레니움 코드 추가.   
0.5초 간격으로 40번 내려가면 최대 1천개에 도달(time.sleep 더 줄여도 로딩이 느려서 스크롤 횟수 증가)  
스크롤시 최대개수를 초과하면 10개씩 반복되므로 이를 방지   
시작동. 셀레니움때문에 속도가 매우 하락한것으로 추정됨
