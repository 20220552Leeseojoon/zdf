# zdf

import pandas as pd
import matplotlib.pyplot as plt
import requests

# 대한민국과 프랑스의 최신 코로나 확진자 데이터 URL (CSV 형태)
# 실제로 데이터를 제공하는 API나 링크를 사용할 수 있습니다.
# 예시로 아래 링크를 사용합니다 (예시 데이터입니다. 실제 사용 시 변경 필요).

# 대한민국 COVID-19 데이터 (수정 필요)
korea_data_url = "https://example.com/korea_covid_data.csv"
# 프랑스 COVID-19 데이터 (수정 필요)
france_data_url = "https://example.com/france_covid_data.csv"

# 데이터를 pandas로 불러옵니다.
korea_data = pd.read_csv(korea_data_url)
france_data = pd.read_csv(france_data_url)

# 가정: 데이터에 'date', 'total_cases', 'population' 컬럼이 있다고 가정합니다.
# 대한민국과 프랑스의 각 날짜별 총 인구 대비 확진자 수 비율을 계산합니다.

# 대한민국의 확진자 수 비율
korea_data['case_ratio'] = korea_data['total_cases'] / korea_data['population'] * 100

# 프랑스의 확진자 수 비율
france_data['case_ratio'] = france_data['total_cases'] / france_data['population'] * 100

# 날짜를 기준으로 그래프를 그리기 전에 날짜 형식을 맞춥니다.
korea_data['date'] = pd.to_datetime(korea_data['date'])
france_data['date'] = pd.to_datetime(france_data['date'])

# 그래프 생성
plt.figure(figsize=(12, 6))

# 대한민국 그래프
plt.plot(korea_data['date'], korea_data['case_ratio'], label='Korea', color='blue')

# 프랑스 그래프
plt.plot(france_data['date'], france_data['case_ratio'], label='France', color='red')

# 그래프 제목과 레이블
plt.title('COVID-19 Case Ratio (Daily Cases per Million People)', fontsize=14)
plt.xlabel('Date', fontsize=12)
plt.ylabel('Case Ratio (%)', fontsize=12)

# 그래프 레전드
plt.legend()

# 그래프 표시
plt.grid(True)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
