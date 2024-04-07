pip install beautifulsoup4

pip install requests

import requests

from bs4 import BeautifulSoup as bs

response = requests.get("https://www.ytn.co.kr/news/list.php?mcd=0102")

print(response.status_code)

soup = bs(response.text, 'html.parser')

print(response.text)

print(response.content)

news_list = soup.select('#container  div  div.content  div  div.news_list_wrap  div > div.text_area > div.title > a')

cafe_list = soup.select('#main-area > div:nth-child(4) > table > tbody > tr:nth-child(1) > td.td_article > div.board-list > div > a ')

print(news_list)

for item in news_list:
    news_title = item.get_text().strip()
    print(news_title) # soup으로 성분을 추출한것을 text부분만 얻어서 출력

print(news_list) # 성분 전체를 출력

pip show pandas

pip show openpyxl

pip install pandas

pip install openpyxl

import pandas as pd

data_list = []

for news_now in news_list:
    news_text = news_now.get_text(strip=True)
    data_list.append({"Extracted data": news_text}) 

for news in news_list:
    news_now = news.get_text()
    # href_value = news['href']
    print("제목: {}".format(news_now)) # ,href_value, 링크: {}

df = pd.DataFrame(data_list)
df['제목'] = news_list
#df['href'] = href_value
df.to_excel('news_list.xlsx', index=False)



