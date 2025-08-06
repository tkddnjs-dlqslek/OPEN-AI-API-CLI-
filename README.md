# 📌 # 경제 기사 크롤링 + 텍스트 증강/요약/분류 => EXCEL/SLACK 등에 저장

설명: 이 프로젝트는 경제 기사 요약 워크플로우입니다.  
---

## 📁 파일 구성

- `crawling.py` : 대한경제 사이트에서 selenium으로 기사 데이터를 크롤링 / time.sleep()을 너무 짧게 조정하면 다음 페이지로 넘어가기 전에 코드가 실행되는 경우가 있어 여유가 되면 길게 조정하는 것이 좋음. 만약 크롤링이 제대로 되지 않는다면 time.sleep을 더 길게 조정하면 됨
- '실시간 경제 기사 데이터.xlsx' : crawling.py로 크롤링한 데이터를 엑셀 파일로 저장
<br/><br/>


- `categorized.py` : 크롤링한 기사 데이터에 분류 기준 슬라이드를 categories 슬라이드에 대분류 저장(금리상승, 금리하락, 금리유지 등). 또한 기사 데이터에 칼럼을 추가하여 어떤 분야 관련한 기사인지 기입.
- 'filtered_실시간_경제_기사_데이터.xlsx' : categorized.py로 전처리한 기사 데이터 
<br/><br/>


- `classify_article.py` : 로컬 환경 변수에서 OPEN AI API KEY를 가져오도록 했음, 자체적으로 API KEY를 넣으면 실행가능(gpt-4o-mini 모델이 가성비가 제일 좋아 선정)
- 1) 기사에 가장 중요한 텍스트를 키워드로 추출하도록 키워드 추출 함수를 추가
  2) 기사의 본문 내용이 너무 빈약할 경우를 대비해서 본문 내용을 1000자까지 늘려 작성하도록 텍스트 증강 함수를 추가
  3) 기사의 제목/본문/키워드를 토대로 categories 대분류에 따라 분류함, [category1, reason1], [category2, reason2] => [분류, 분류 이유] 해당 형식으로 2개 추출되도록 조정했다. 처음 분류된게 잘못 분류될 수 있음을 고려
  4) 최빈 카테고리와 희귀 카테고리를 선정해 현재 시의성이 높고 낮은 주제를 각각 찾을 수도 있다.
 <br/><br/>

## EX)
<img width="1456" height="663" alt="image" src="https://github.com/user-attachments/assets/3dd585ce-6a27-4b66-91b3-85beac908647" />
1) 키워드 출력
2) 증강된 기사 출력
3) 요약본은 바로 엑셀 파일에 저장

## 📦 사용된 기술

- Python, Selenium
- OPENAI API
- CLI(Command Line Interface)

---

<br/><br/><br/>
1) 라이브러리 이름 yaml 아니고 pyyaml임
2) CLI라서 categorized.py는 terminal에서 실행해야됨 ex) python classify_article.py --indir "filtered_실시간_경제_기사_데이터.xlsx" --sheet_name "Sorted_Data" --categories "기사카테고리" --categories_sheet_name "categories"
   
라이선스: 없음
