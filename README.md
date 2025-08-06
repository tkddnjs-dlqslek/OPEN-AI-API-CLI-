# 📌 # 경제 기사 크롤링 + 텍스트 증강/요약/분류 => EXCEL/SLACK 등에 저장

설명: 이 프로젝트는 경제 기사 요약 워크플로우입니다.  
---

## 📁 파일 구성

- `crawling.py` : 대한경제 사이트에서 selenium으로 기사 데이터를 크롤링 / time.sleep()을 너무 짧게 조정하면 다음 페이지로 넘어가기 전에 코드가 실행되는 경우가 있어 여유가 되면 길게 조정하는 것이 좋음. 만약 크롤링이 제대로 되지 않는다면 time.sleep을 더 길게 조정하면 됨
- '실시간 경제 기사 데이터.xlsx' : crawling.py로 크롤링한 데이터를 엑셀 파일로 저장
<br/><br/>

- '주담대dataset.xlsx' : 미리 대분류를 지정해놓은 엑셀 파일 저장 / categories 슬라이드에 대분류 저장(금리상승, 금리하락, 금리유지 등)
- `classify_article.py` : 로컬 환경 변수에서 OPEN AI API KEY를 가져오도록 했음, 자체적으로 API KEY를 넣으면 실행가능(gpt-4o-mini 모델이 가성비가 제일 좋아 선정)
- 1) 기사에 가장 중요한 텍스트를 키워드로 추출하도록 키워드 추출 함수를 추가
  2) 기사의 본문 내용이 너무 빈약할 경우를 대비해서 본문 내용을 1000자까지 늘려 작성하도록 텍스트 증강 함수를 추가
  3) 기사의 제목/본문/키워드를 토대로 categories 대분류에 따라 분류함, [category1, reason1], [category2, reason2] => [분류, 분류 이유] 해당 형식으로 2개 추출되도록 조정했다. 처음 분류된게 잘못 분류될 수 있음을 고려
  4) 최빈 카테고리와 희귀 카테고리를 선정해 현재 시의성이 높고 낮은 주제를 각각 찾을 수도 있다.
 <br/><br/>
 
- `categorized.py` : 회귀 모델(XGBoost, LM) 학습 및 평가

---

## 🚀 실행 방법

1. 필요한 라이브러리 설치:
    ```bash
    pip install -r requirements.txt
    ```

2. 순서대로 실행:
    ```bash
    python 01_crawler.py
    python 02_preprocess.py
    python 03_modeling.py
    python 04_visualize.py
    ```

3. 결과는 `output/` 폴더에 저장됩니다.

---

## 📦 사용된 기술

- Python, Selenium, BeautifulSoup
- Google Vision API, KLUE-RoBERTa
- XGBoost, Scikit-learn
- Tableau

---



# 로컬 사용법
1. AI 분석기능 사용하려면 OpenAI 에서 API키 발급받아서 app.js에 입력 (브라우저에 입력해서 쓰는건 유출 위험있으니 use at your own risk)
2. Chrome 확장기능 페이지에서 개발자모드 켜기
3. '압축해제된 확장프로그램 로드' 버튼 눌러서 app.js, manifest.json 들어있는 폴더 올리기 
4. 유튜브 가서 사용
<br/><br/><br/>

![sample1](https://github.com/user-attachments/assets/ca68624e-6864-4d1f-85b2-094862855f5b)

<br/><br/><br/>
라이선스: 없음
