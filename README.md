```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
import platform

from matplotlib import font_manager, rc
plt.rcParams['axes.unicode_minus'] = False

if platform.system() == 'Darwin':
    rc('font', family='AppleGothic')
elif platform.system() == 'Windows':
    path = "c:/Windows/Fonts/malgun.ttf"
    font_name = font_manager.FontProperties(fname=path).get_name()
    rc('font', family=font_name)
else:
    print('Unknown system... sorry~~~~')
```
# 서울특별시 주유소 판매가격 

# 1. 데이터 불러오기


```python
# 상반기 주유소 판매 데이터 불러오기

first = pd.read_csv("../data/상반기 주유소 판매가격.csv", encoding="cp949")
first
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190101</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190102</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190103</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190104</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190105</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>90585</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20190626</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1529</td>
      <td>1389</td>
      <td>0</td>
    </tr>
    <tr>
      <th>90586</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20190627</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1529</td>
      <td>1389</td>
      <td>0</td>
    </tr>
    <tr>
      <th>90587</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20190628</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1529</td>
      <td>1389</td>
      <td>0</td>
    </tr>
    <tr>
      <th>90588</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20190629</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1529</td>
      <td>1389</td>
      <td>0</td>
    </tr>
    <tr>
      <th>90589</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20190630</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1529</td>
      <td>1389</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>90590 rows × 11 columns</p>
</div>




```python
second = pd.read_csv("../data/하반기 주유소 판매가격.csv", encoding="cp949")
second
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190701</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1777</td>
      <td>1577</td>
      <td>1477</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190702</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1777</td>
      <td>1577</td>
      <td>1477</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190703</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1777</td>
      <td>1577</td>
      <td>1477</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190704</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1777</td>
      <td>1577</td>
      <td>1477</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190705</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1777</td>
      <td>1577</td>
      <td>1477</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191227</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191228</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191229</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191230</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191231</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
  </tbody>
</table>
<p>91124 rows × 11 columns</p>
</div>




```python
# 상반기 판매가격 데이터 프레임 결측치 조회
first[first.isna()].count()
```




    번호       0
    지역       0
    상호       0
    주소       0
    기간       0
    상표       0
    셀프여부     0
    고급휘발유    0
    휘발유      0
    경유       0
    실내등유     0
    dtype: int64




```python
# 하반기 판매가격 데이터 프레임 결측치 조회
second[second.isna()].count()
```




    번호       0
    지역       0
    상호       0
    주소       0
    기간       0
    상표       0
    셀프여부     0
    고급휘발유    0
    휘발유      0
    경유       0
    실내등유     0
    dtype: int64



# 2. 데이터 결합


```python
# 상반기와 하반기 데이터를 상하로 결합
df = pd.concat([first,second])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190101</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190102</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190103</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190104</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190105</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191227</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191228</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191229</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191230</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191231</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 11 columns</p>
</div>




```python
a = df.groupby(by=['지역', '상호']).count()
a.groupby(by='지역').count()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
    </tr>
    <tr>
      <th>지역</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>서울 강남구</th>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
      <td>41</td>
    </tr>
    <tr>
      <th>서울 강동구</th>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
    </tr>
    <tr>
      <th>서울 강북구</th>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>서울 강서구</th>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
      <td>35</td>
    </tr>
    <tr>
      <th>서울 관악구</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>서울 광진구</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>서울 구로구</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>서울 금천구</th>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>서울 노원구</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>서울 도봉구</th>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
      <td>19</td>
    </tr>
    <tr>
      <th>서울 동대문구</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>서울 동작구</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
    <tr>
      <th>서울 마포구</th>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>서울 서대문구</th>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
    </tr>
    <tr>
      <th>서울 서초구</th>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
    </tr>
    <tr>
      <th>서울 성동구</th>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
      <td>17</td>
    </tr>
    <tr>
      <th>서울 성북구</th>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
      <td>23</td>
    </tr>
    <tr>
      <th>서울 송파구</th>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
    </tr>
    <tr>
      <th>서울 양천구</th>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
      <td>26</td>
    </tr>
    <tr>
      <th>서울 영등포구</th>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
    </tr>
    <tr>
      <th>서울 용산구</th>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
      <td>15</td>
    </tr>
    <tr>
      <th>서울 은평구</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>서울 종로구</th>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
      <td>9</td>
    </tr>
    <tr>
      <th>서울 중구</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
    <tr>
      <th>서울 중랑구</th>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



# 3. 데이터 가공 및 분석


```python
# 데이터 프레임 정보 조회
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 181714 entries, 0 to 91123
    Data columns (total 11 columns):
     #   Column  Non-Null Count   Dtype 
    ---  ------  --------------   ----- 
     0   번호      181714 non-null  object
     1   지역      181714 non-null  object
     2   상호      181714 non-null  object
     3   주소      181714 non-null  object
     4   기간      181714 non-null  int64 
     5   상표      181714 non-null  object
     6   셀프여부    181714 non-null  object
     7   고급휘발유   181714 non-null  int64 
     8   휘발유     181714 non-null  int64 
     9   경유      181714 non-null  int64 
     10  실내등유    181714 non-null  int64 
    dtypes: int64(5), object(6)
    memory usage: 16.6+ MB
    


```python
# 상표 컬럼의 고유값 조회
df['상표'].unique()
```




    array(['SK에너지', 'GS칼텍스', 'S-OIL', '현대오일뱅크', '알뜰주유소', 'NH-OIL', '알뜰(ex)',
           '자가상표'], dtype=object)




```python
# 지역 컬럼의 고유값 조회
df['지역'].unique()
```




    array(['서울 강남구', '서울 강동구', '서울 강북구', '서울 강서구', '서울 관악구', '서울 광진구',
           '서울 구로구', '서울 금천구', '서울 노원구', '서울 도봉구', '서울 동대문구', '서울 동작구',
           '서울 마포구', '서울 서대문구', '서울 서초구', '서울 성동구', '서울 성북구', '서울 송파구',
           '서울 양천구', '서울 영등포구', '서울 용산구', '서울 은평구', '서울 종로구', '서울 중구',
           '서울 중랑구'], dtype=object)




```python
# 지역 컬럼의 값을 이용하여 시와 구를 분리
df['시'] = df['지역'].str.split(" ").str[0]
df['구'] = df['지역'].str.split(" ").str[1]
df
    
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190101</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190102</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190103</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190104</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190105</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191227</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191228</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191229</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191230</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191231</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울</td>
      <td>중랑구</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 13 columns</p>
</div>




```python
# 시 컬럼의 서울을 서울특별시로 변환
df['시'] = '서울특별시'
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190101</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190102</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190103</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190104</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>20190105</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191227</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191228</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191229</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191230</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>20191231</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 13 columns</p>
</div>




```python
# 기간 컬럼을 datetime 형식으로 변경
# df['기간']= df['기간'].astype('datetime64') 이거도 됨
df['기간']=pd.to_datetime(df['기간'],format='%Y%m%d')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-01</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-02</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-03</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-04</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-05</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-27</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-28</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-29</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-30</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-31</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 13 columns</p>
</div>




```python
# 기간 컬럼에서 dt 타입을 이용하여 년, 월, 일, 요일 컬럼 생성
import datetime as dt
df['년'] = df['기간'].dt.year
df['월'] = df['기간'].dt.month
df['일'] = df['기간'].dt.day
df['요일'] = df['기간'].dt.strftime('%A')
df['요일(number)'] = df['기간'].dt.strftime('%w')
df['주차'] = df['기간'].dt.strftime('%W')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
      <th>요일</th>
      <th>요일(number)</th>
      <th>주차</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-01</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-02</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>2</td>
      <td>Wednesday</td>
      <td>3</td>
      <td>00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-03</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>3</td>
      <td>Thursday</td>
      <td>4</td>
      <td>00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-04</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>4</td>
      <td>Friday</td>
      <td>5</td>
      <td>00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-05</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>5</td>
      <td>Saturday</td>
      <td>6</td>
      <td>00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-27</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>27</td>
      <td>Friday</td>
      <td>5</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-28</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>28</td>
      <td>Saturday</td>
      <td>6</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-29</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>29</td>
      <td>Sunday</td>
      <td>0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-30</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>30</td>
      <td>Monday</td>
      <td>1</td>
      <td>52</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-31</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>0</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>31</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 19 columns</p>
</div>




```python
# 휘발유 가격이 비싼 5개 판매가격을 출력하세요.
df.sort_values(by=['휘발유'], ascending=False).head(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
      <th>요일</th>
      <th>요일(number)</th>
      <th>주차</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>86620</th>
      <td>A0000767</td>
      <td>서울 중구</td>
      <td>서남주유소</td>
      <td>서울 중구 통일로 30</td>
      <td>2019-09-24</td>
      <td>SK에너지</td>
      <td>일반</td>
      <td>2649</td>
      <td>2356</td>
      <td>2196</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>중구</td>
      <td>2019</td>
      <td>9</td>
      <td>24</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>



# --------------------------------------------------------------------------------------------------------


```python
# a = df.pivot_table(index=['요일'], values=['휘발유', '고급휘발유', '경유']).sort_values('요일')
# plt.figure(figsize=(12,6))
# plt.subplot(1,3,1)
# sns.barplot(x=a.index, y=a['휘발유'])
# plt.xticks(rotation=45)
# plt.subplot(1,3,2)
# sns.barplot(x=a.index, y=a['고급휘발유'])
# plt.xticks(rotation=45)
# plt.subplot(1,3,3)
# sns.barplot(x=a.index, y=a['경유'])
# plt.xticks(rotation=45)
# plt.tight_layout()
# plt.show()
```


```python
# plt.figure(figsize=(10,8))
# plt.subplot(3,1,1)
# sns.barplot(x=df['구'], y=df['고급휘발유'])
# plt.xticks(rotation=45)

# plt.subplot(3,1,2)
# sns.barplot(x=df['구'], y=df['휘발유'])
# plt.xticks(rotation=45)

# plt.subplot(3,1,3)
# sns.barplot(x=df['구'], y=df['경유'])
# plt.xticks(rotation=45)
# plt.tight_layout()
# plt.show()
```


```python
# df.groupby(by=['지역', '상표', '셀프여부']).agg('mean').iloc[:,:4]
# b = df.pivot_table(index=['지역', '상표'])
# b
# plt.figure(figsize=(20,10))
# sns.pointplot(x='상표', y='휘발유', data=b, hue='셀프여부')
# plt.show()
# df.groupby(by=['지역', '셀프여부']).agg('mean')
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
      <th>요일</th>
      <th>요일(number)</th>
      <th>주차</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-01</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-02</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>2</td>
      <td>Wednesday</td>
      <td>3</td>
      <td>00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-03</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>3</td>
      <td>Thursday</td>
      <td>4</td>
      <td>00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-04</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>4</td>
      <td>Friday</td>
      <td>5</td>
      <td>00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-05</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>5</td>
      <td>Saturday</td>
      <td>6</td>
      <td>00</td>
    </tr>
  </tbody>
</table>
</div>




```python
newdf = df.pivot_table(index=['구', '상호'], values=['경유', '휘발유','고급휘발유'])
a = df['구'].unique() #['%s' % str(t) for t in list(df['구'].unique())]
ls = [newdf.loc[i].index.shape[0] for i in a]
new_dict = {'구' : a, '개수' : ls}
new_df = pd.DataFrame(new_dict)
new_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>구</th>
      <th>개수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강동구</td>
      <td>17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강북구</td>
      <td>13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강서구</td>
      <td>35</td>
    </tr>
    <tr>
      <th>4</th>
      <td>관악구</td>
      <td>18</td>
    </tr>
    <tr>
      <th>5</th>
      <td>광진구</td>
      <td>18</td>
    </tr>
    <tr>
      <th>6</th>
      <td>구로구</td>
      <td>22</td>
    </tr>
    <tr>
      <th>7</th>
      <td>금천구</td>
      <td>13</td>
    </tr>
    <tr>
      <th>8</th>
      <td>노원구</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>도봉구</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10</th>
      <td>동대문구</td>
      <td>22</td>
    </tr>
    <tr>
      <th>11</th>
      <td>동작구</td>
      <td>10</td>
    </tr>
    <tr>
      <th>12</th>
      <td>마포구</td>
      <td>13</td>
    </tr>
    <tr>
      <th>13</th>
      <td>서대문구</td>
      <td>16</td>
    </tr>
    <tr>
      <th>14</th>
      <td>서초구</td>
      <td>39</td>
    </tr>
    <tr>
      <th>15</th>
      <td>성동구</td>
      <td>17</td>
    </tr>
    <tr>
      <th>16</th>
      <td>성북구</td>
      <td>23</td>
    </tr>
    <tr>
      <th>17</th>
      <td>송파구</td>
      <td>33</td>
    </tr>
    <tr>
      <th>18</th>
      <td>양천구</td>
      <td>26</td>
    </tr>
    <tr>
      <th>19</th>
      <td>영등포구</td>
      <td>32</td>
    </tr>
    <tr>
      <th>20</th>
      <td>용산구</td>
      <td>15</td>
    </tr>
    <tr>
      <th>21</th>
      <td>은평구</td>
      <td>18</td>
    </tr>
    <tr>
      <th>22</th>
      <td>종로구</td>
      <td>9</td>
    </tr>
    <tr>
      <th>23</th>
      <td>중구</td>
      <td>12</td>
    </tr>
    <tr>
      <th>24</th>
      <td>중랑구</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>

```python
import folium
import json

geo_path = '../data/d/municipalities-geo-simple.json'
geo_str = json.load(open(geo_path, encoding='utf-8'))
loca = pd.read_excel('../data/d/seoul_data.xlsx')
loca1 = loca.pivot_table(index='구', values=['lat', 'lng'])
loca2 = loca1.merge(new_df, on='구')
loca2

# center = [37.541, 126.986]
# m1 = folium.Map(location=center, zoom_start=10.5)
# # m2 = folium.Map(location=center, zoom_start=10.5)
# # m3 = folium.Map(location=center, zoom_start=10.5)

# choropleth = folium.Choropleth(
#         geo_data=geo_str,
#         data=new_df,
#         columns=('구','개수'),
#         key_on='feature.properties.name',
#         fill_color='Reds',
#         legend_name='구별 주유소 개수').add_to(m1)

# choropleth.geojson.add_child(
#     folium.features.GeoJsonTooltip(['name'],labels=False)
# )

# for i in range(25) :
#     lat = float(loca2['lat'][i])
#     lng = float(loca2['lng'][i])
#     ct = [lat, lng]
#     folium.CircleMarker(location=[lat, lng], radius=float(loca2['개수'][i]*1.3), popup=loca2['구'][i], color='blue', fill_color='blue').add_to(m1)
# m1


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>구</th>
      <th>lat</th>
      <th>lng</th>
      <th>개수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구</td>
      <td>37.497852</td>
      <td>127.058985</td>
      <td>41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강동구</td>
      <td>37.538333</td>
      <td>127.136160</td>
      <td>17</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강북구</td>
      <td>37.633471</td>
      <td>127.022860</td>
      <td>13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강서구</td>
      <td>37.553281</td>
      <td>126.838471</td>
      <td>35</td>
    </tr>
    <tr>
      <th>4</th>
      <td>관악구</td>
      <td>37.477717</td>
      <td>126.940236</td>
      <td>18</td>
    </tr>
    <tr>
      <th>5</th>
      <td>광진구</td>
      <td>37.543421</td>
      <td>127.082546</td>
      <td>18</td>
    </tr>
    <tr>
      <th>6</th>
      <td>구로구</td>
      <td>37.494748</td>
      <td>126.870968</td>
      <td>22</td>
    </tr>
    <tr>
      <th>7</th>
      <td>금천구</td>
      <td>37.460753</td>
      <td>126.895418</td>
      <td>13</td>
    </tr>
    <tr>
      <th>8</th>
      <td>노원구</td>
      <td>37.646325</td>
      <td>127.069495</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>도봉구</td>
      <td>37.666747</td>
      <td>127.045062</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10</th>
      <td>동대문구</td>
      <td>37.579257</td>
      <td>127.045836</td>
      <td>22</td>
    </tr>
    <tr>
      <th>11</th>
      <td>동작구</td>
      <td>37.507589</td>
      <td>126.943898</td>
      <td>10</td>
    </tr>
    <tr>
      <th>12</th>
      <td>마포구</td>
      <td>37.552542</td>
      <td>126.928698</td>
      <td>13</td>
    </tr>
    <tr>
      <th>13</th>
      <td>서대문구</td>
      <td>37.571826</td>
      <td>126.945768</td>
      <td>16</td>
    </tr>
    <tr>
      <th>14</th>
      <td>서초구</td>
      <td>37.484865</td>
      <td>127.018679</td>
      <td>39</td>
    </tr>
    <tr>
      <th>15</th>
      <td>성동구</td>
      <td>37.554585</td>
      <td>127.037287</td>
      <td>17</td>
    </tr>
    <tr>
      <th>16</th>
      <td>성북구</td>
      <td>37.591508</td>
      <td>127.019798</td>
      <td>23</td>
    </tr>
    <tr>
      <th>17</th>
      <td>송파구</td>
      <td>37.503889</td>
      <td>127.118049</td>
      <td>33</td>
    </tr>
    <tr>
      <th>18</th>
      <td>양천구</td>
      <td>37.527627</td>
      <td>126.853749</td>
      <td>26</td>
    </tr>
    <tr>
      <th>19</th>
      <td>영등포구</td>
      <td>37.522779</td>
      <td>126.899471</td>
      <td>32</td>
    </tr>
    <tr>
      <th>20</th>
      <td>용산구</td>
      <td>37.535886</td>
      <td>126.975835</td>
      <td>15</td>
    </tr>
    <tr>
      <th>21</th>
      <td>은평구</td>
      <td>37.605389</td>
      <td>126.920936</td>
      <td>18</td>
    </tr>
    <tr>
      <th>22</th>
      <td>종로구</td>
      <td>37.577927</td>
      <td>126.982328</td>
      <td>9</td>
    </tr>
    <tr>
      <th>23</th>
      <td>중구</td>
      <td>37.562656</td>
      <td>126.990495</td>
      <td>12</td>
    </tr>
    <tr>
      <th>24</th>
      <td>중랑구</td>
      <td>37.602433</td>
      <td>127.092026</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>




```python
a = df.pivot_table(index=['요일'], values=['휘발유', '고급휘발유', '경유']).sort_values('요일')
plt.figure(figsize=(12,6))
plt.subplot(1,3,1)
sns.barplot(x=a.index, y=a['휘발유'])
plt.xticks(rotation=45)
plt.subplot(1,3,2)
sns.barplot(x=a.index, y=a['고급휘발유'])
plt.xticks(rotation=45)
plt.subplot(1,3,3)
sns.barplot(x=a.index, y=a['경유'])
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```


    
![png](https://user-images.githubusercontent.com/44217050/152714600-3cf39dad-6268-4639-94e5-a782f2c98f1a.png)
    



```python
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
sns.barplot(x=df['구'], y=df['고급휘발유'])
plt.xticks(rotation=45)

plt.subplot(3,1,2)
sns.barplot(x=df['구'], y=df['휘발유'])
plt.xticks(rotation=45)

plt.subplot(3,1,3)
sns.barplot(x=df['구'], y=df['경유'])
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```


    
![png](output_27_0.png)
    



```python
a = df.pivot_table(index=['요일(number)'], values=['휘발유', '고급휘발유', '경유']).sort_values('요일(number)')
plt.figure(figsize=(12,20))

plt.subplot(3,1,1)
plt.ylim((1566.7,1567.9))
sns.pointplot(x=a.index, y=a['휘발유'])
plt.xticks(rotation=45)

plt.subplot(3,1,2)
plt.ylim((1839.4,1840.1))
sns.pointplot(x=a.index, y=a['고급휘발유'])
plt.xticks(rotation=45)

plt.subplot(3,1,3)
plt.ylim((1435.1,1436))
sns.pointplot(x=a.index, y=a['경유'])
plt.xticks(rotation=45)


plt.tight_layout()
plt.show()
# 0은 일요일 ~ 6 토요일

```


    
![png](output_28_0.png)
    



```python
b = df.pivot_table(index=['월'], values=['휘발유', '고급휘발유', '경유']).sort_values('월')
plt.figure(figsize=(12,6))
plt.subplot(1,3,1)

sns.pointplot(x=b.index, y=b['휘발유'])
plt.xticks(rotation=45)
plt.subplot(1,3,2)

sns.pointplot(x=b.index, y=b['고급휘발유'])
plt.xticks(rotation=45)
plt.subplot(1,3,3)

sns.pointplot(x=b.index, y=b['경유'])
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()

```


    
![png](output_29_0.png)
    



```python
plt.subplot(1,2,1)
sns.kdeplot(df['고급휘발유'])
plt.subplot(1,2,2)
sns.kdeplot(df[df['고급휘발유'] != 0]['고급휘발유'])
median_value1 = df[df['고급휘발유'] != 0]['고급휘발유'].median() # 고급휘발유의 중앙값
print('중앙값 : {}'.format(median_value1))
plt.tight_layout()
plt.show()
```

    중앙값 : 1807.0
    


    
![png](output_30_1.png)
    



```python
df.loc[(df.고급휘발유 == 0), '고급휘발유']= median_value1
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
      <th>요일</th>
      <th>요일(number)</th>
      <th>주차</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-01</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-02</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>2</td>
      <td>Wednesday</td>
      <td>3</td>
      <td>00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-03</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>3</td>
      <td>Thursday</td>
      <td>4</td>
      <td>00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-04</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>4</td>
      <td>Friday</td>
      <td>5</td>
      <td>00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-05</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>5</td>
      <td>Saturday</td>
      <td>6</td>
      <td>00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-27</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>27</td>
      <td>Friday</td>
      <td>5</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-28</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>28</td>
      <td>Saturday</td>
      <td>6</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-29</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>29</td>
      <td>Sunday</td>
      <td>0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-30</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>30</td>
      <td>Monday</td>
      <td>1</td>
      <td>52</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-31</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>31</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 19 columns</p>
</div>




```python
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
sns.barplot(x=df['구'], y=df['고급휘발유'], hue=df['상표'])
plt.xticks(rotation=45)
plt.ylim((1600,2250))

plt.scatter()

plt.subplot(3,1,2)
sns.barplot(x=df['구'], y=df['휘발유'])
plt.xticks(rotation=45)
plt.ylim((1000,2050))


plt.subplot(3,1,3)
sns.barplot(x=df['구'], y=df['경유'])
plt.xticks(rotation=45)
plt.ylim((800,2000))

plt.tight_layout()
plt.show()
```


    
![png](output_32_0.png)
    


# -------------------------------------------------------------------------------------



```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>번호</th>
      <th>지역</th>
      <th>상호</th>
      <th>주소</th>
      <th>기간</th>
      <th>상표</th>
      <th>셀프여부</th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>시</th>
      <th>구</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
      <th>요일</th>
      <th>요일(number)</th>
      <th>주차</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-01</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>1</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-02</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>2</td>
      <td>Wednesday</td>
      <td>3</td>
      <td>00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-03</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>3</td>
      <td>Thursday</td>
      <td>4</td>
      <td>00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-04</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>4</td>
      <td>Friday</td>
      <td>5</td>
      <td>00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A0006039</td>
      <td>서울 강남구</td>
      <td>(주)동하힐탑셀프주유소</td>
      <td>서울 강남구 논현로 640</td>
      <td>2019-01-05</td>
      <td>SK에너지</td>
      <td>셀프</td>
      <td>1673</td>
      <td>1465</td>
      <td>1365</td>
      <td>0</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>2019</td>
      <td>1</td>
      <td>5</td>
      <td>Saturday</td>
      <td>6</td>
      <td>00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>91119</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-27</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>27</td>
      <td>Friday</td>
      <td>5</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91120</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-28</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>28</td>
      <td>Saturday</td>
      <td>6</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91121</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-29</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>29</td>
      <td>Sunday</td>
      <td>0</td>
      <td>51</td>
    </tr>
    <tr>
      <th>91122</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-30</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>30</td>
      <td>Monday</td>
      <td>1</td>
      <td>52</td>
    </tr>
    <tr>
      <th>91123</th>
      <td>A0032659</td>
      <td>서울 중랑구</td>
      <td>지에스칼텍스㈜ 소망주유소</td>
      <td>서울 중랑구 망우로 475</td>
      <td>2019-12-31</td>
      <td>GS칼텍스</td>
      <td>셀프</td>
      <td>1807</td>
      <td>1540</td>
      <td>1389</td>
      <td>1100</td>
      <td>서울특별시</td>
      <td>중랑구</td>
      <td>2019</td>
      <td>12</td>
      <td>31</td>
      <td>Tuesday</td>
      <td>2</td>
      <td>52</td>
    </tr>
  </tbody>
</table>
<p>181714 rows × 19 columns</p>
</div>




```python
abcd = df[df['구']=='강남구']
```


```python
plt.figure(figsize=(10,8))
plt.subplot(3,1,1)
sns.barplot(x='구', y='고급휘발유', hue='상표', data=abcd)
plt.xticks(rotation=45)
plt.ylim((1600,2250))

plt.subplot(3,1,2)
sns.barplot(x=df['구'], y=df['휘발유'])
plt.xticks(rotation=45)
plt.ylim((1000,2050))


plt.subplot(3,1,3)
sns.barplot(x=df['구'], y=df['경유'])
plt.xticks(rotation=45)
plt.ylim((800,2000))

plt.tight_layout()
plt.show()
```


    
![png](output_36_0.png)
    



```python
abbb = df.groupby(by=['구']).agg('mean')
abbb.sort_values(by=['고급휘발유'], ascending=False).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
      <th>년</th>
      <th>월</th>
      <th>일</th>
    </tr>
    <tr>
      <th>구</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>중구</th>
      <td>2205.325148</td>
      <td>1976.948052</td>
      <td>1835.953011</td>
      <td>795.981110</td>
      <td>2019.0</td>
      <td>6.440142</td>
      <td>15.703424</td>
    </tr>
    <tr>
      <th>용산구</th>
      <td>2148.446038</td>
      <td>1882.049825</td>
      <td>1754.390329</td>
      <td>588.170803</td>
      <td>2019.0</td>
      <td>6.540357</td>
      <td>15.718882</td>
    </tr>
    <tr>
      <th>종로구</th>
      <td>2043.347985</td>
      <td>1838.554945</td>
      <td>1696.179182</td>
      <td>701.580586</td>
      <td>2019.0</td>
      <td>6.519231</td>
      <td>15.697192</td>
    </tr>
    <tr>
      <th>강남구</th>
      <td>1929.332123</td>
      <td>1713.093581</td>
      <td>1577.055491</td>
      <td>310.218127</td>
      <td>2019.0</td>
      <td>6.508392</td>
      <td>15.715695</td>
    </tr>
    <tr>
      <th>마포구</th>
      <td>1903.492718</td>
      <td>1689.755616</td>
      <td>1554.821772</td>
      <td>547.525056</td>
      <td>2019.0</td>
      <td>6.357196</td>
      <td>15.682301</td>
    </tr>
  </tbody>
</table>
</div>




```python
abbc = df.groupby(by=['구', '상표']).agg('mean').iloc[:,:4]
abbc
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>고급휘발유</th>
      <th>휘발유</th>
      <th>경유</th>
      <th>실내등유</th>
    </tr>
    <tr>
      <th>구</th>
      <th>상표</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">강남구</th>
      <th>GS칼텍스</th>
      <td>1896.024740</td>
      <td>1687.445077</td>
      <td>1551.164523</td>
      <td>432.204107</td>
    </tr>
    <tr>
      <th>S-OIL</th>
      <td>1912.889041</td>
      <td>1684.525114</td>
      <td>1553.113242</td>
      <td>31.232877</td>
    </tr>
    <tr>
      <th>SK에너지</th>
      <td>1968.370642</td>
      <td>1746.478287</td>
      <td>1610.112080</td>
      <td>329.904434</td>
    </tr>
    <tr>
      <th>현대오일뱅크</th>
      <td>1882.935890</td>
      <td>1684.545753</td>
      <td>1544.669041</td>
      <td>304.279452</td>
    </tr>
    <tr>
      <th>강동구</th>
      <th>GS칼텍스</th>
      <td>1806.974781</td>
      <td>1549.105811</td>
      <td>1412.408991</td>
      <td>666.003289</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">중랑구</th>
      <th>GS칼텍스</th>
      <td>1795.540762</td>
      <td>1467.271554</td>
      <td>1327.095601</td>
      <td>611.894428</td>
    </tr>
    <tr>
      <th>S-OIL</th>
      <td>1807.000000</td>
      <td>1473.182410</td>
      <td>1332.210098</td>
      <td>753.773073</td>
    </tr>
    <tr>
      <th>SK에너지</th>
      <td>1817.654306</td>
      <td>1480.476675</td>
      <td>1349.468301</td>
      <td>587.559809</td>
    </tr>
    <tr>
      <th>알뜰주유소</th>
      <td>1807.000000</td>
      <td>1382.555556</td>
      <td>1263.296296</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>현대오일뱅크</th>
      <td>1807.000000</td>
      <td>1435.509589</td>
      <td>1283.619178</td>
      <td>943.315068</td>
    </tr>
  </tbody>
</table>
<p>114 rows × 4 columns</p>
</div>




```python
k = df.pivot_table(index=['구','상표'], values=['고급휘발유', '휘발유','경유'])
a = df['구'].unique()

plt.figure(figsize=(15,15))
plt.title('지역별 상표-고급휘발유 가격')

for i, j in enumerate(a) :
    plt.subplot(5,5,i+1)
    plt.xticks(rotation=45)
    kk = k.loc[j]
    plt.bar(kk.index, kk['고급휘발유'], width=0.4)
    plt.title(j)
    plt.tight_layout()

```


    
![png](output_39_0.png)
    



```python
# abcd = df[df['구']=='강남구']
# kk = df[df['구']=='마포구'].loc[:,['구', '고급휘발유','셀프여부']]
# kk

# sns.violinplot(data=kk, x="구", y="고급휘발유", hue="셀프여부",
#                split=True, inner="quart", linewidth=1,
#                palette={"셀프": "b", "일반": ".85"})
# sns.despine(left=True)
# plt.figure(figsize=(50,50))
# plt.show()

a = df['구'].unique()
plt.figure(figsize=(50,80))

for i, j in enumerate(a) :
    try:
        plt.subplot(7,4,i+1)
        plt.xticks(rotation=45)
        kk = df[df['구']==j].sort_values(by=['셀프여부'])
        sns.violinplot(data=kk, x='구', y="고급휘발유", hue="셀프여부",
                       split=True, inner="quart", linewidth=1,
                       palette={"셀프": "b", "일반": ".85"})
        plt.title(j)
        plt.tight_layout()
    except:
        plt.title(j)
        sns.violinplot(data=kk, x='구', y="고급휘발유",
                       split=True, inner="quart", linewidth=1,
                      color=".85")
```


    
![png](output_40_0.png)
    



```python
a = df['구'].unique()
plt.figure(figsize=(10,50))
for i, j in enumerate(a) :
    try:
        plt.subplot(13,2,i+1) # 행, 열 ,번호
        kk = df[df['구']==j].sort_values(by=['셀프여부'])
        sns.violinplot(data=kk, x='구', y="고급휘발유", hue="셀프여부",
                       split=True, inner="quart", linewidth=1,
                       palette={"셀프": "r", "일반": ".85"})
        plt.title(j)
        plt.tight_layout()
    except:
        sns.violinplot(data=kk, x='구', y="고급휘발유", 
                       split=True, inner="quart", linewidth=1,
                      color=".85")
        plt.title(j)
```


    
![png](output_41_0.png)
    

