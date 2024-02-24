---
title : "Python 기간 날짜 데이터 생성하기"
date : 2024-02-25 00:50:00 +0900
categories : [Python, Functions]
tags : [python func, 기간 날짜 데이터 생성하기] # 소문자만 가능
image :
  path : /static/thumbnail_imgs/python_date_range_thumbnail.png # 썸네일로 사용할 이미지 링크 넣기
  width : 600
  height : 500
  alt : Python Date Range Thumbnail Image
---

안녕하세요. 오늘은 Python 코드를 이용하여 기간 날짜 데이터를 만드는 방법에 대해 공유하도록 하겠습니다.
기간 날짜는 Date Range라고 부르며 시계열 데이터 처리에 자주 사용하는 기능입니다.


### 1. Date Range란?

---

Date Rnage란 아래 그림과 같이 특정 날짜가 아닌 일정 기간 동안의 날짜를 말합니다.

![img.png](/assets/img/post_imgs/2024-02-25-PythonDateRange/img.png)

### 2. Date Range를 사용하는 이유?

---

Date Range는 Python을 처음 공부하거나 이론 중심으로 배울 때는 잘 사용하지 않습니다.
그러나 실무에서는 자주 사용하게 되는데 주로 시계열 데이터를 다룰 때 사용하게 됩니다.

시계열 데이터에 Date Range를 사용한다고 하면 이해가 잘 안되는 분들이 있을 겁니다. 시계열 데이터에는 날짜 데이터가 있기 때문이죠.
시계열 데이터 분석이나 처리에 대해 공부해 보신 분들은 시계열 데이터에 있는 날짜를 이용하여 데이터 처리를 해보셨을 겁니다.
그렇다면 어떤 상황일 때 Date Range를 사용하게 될까요?

Date Range를 사용해야 하는 상황을 예로 들어 설명해보겠습니다.
아래 이미지 형식과 같이 주식 데이터를 API로 수신받아 일자별로 가공처리하여 적재한다고 가정해보겠습니다.
 
![img_1.png](/assets/img/post_imgs/2024-02-25-PythonDateRange/img_1.png)

가공 처리 전 주식 데이터에는 날짜, 가격, 거래량 정보가 있습니다.
단순하게 생각하면 주식 데이터에 있는 날짜를 기준으로 데이터를 가공 처리해도 될 것처럼 보이지만 주식 데이터에 있는 날짜로 데이터를 처리할 경우 중간에 날짜가 빠지기라도 한다면 빠진 상태로 가공 처리되어 적재될 것입니다.
만약 데이터가 누락된 상태로 사용자가 중요한 업무에 사용하게 된다면 어떻게 될까요?

데이터가 소규모라면 육안으로 확인이 가능하겠지만 대용량일 경우 발견하기가 쉽지 않고 누락된 데이터로 의사결정을 하게 될 것입니다.
또 누락된 데이터가 그대로 적재되어 데이터 품질에 악영향을 준다면 사용자는 데이터를 신뢰하지 않을 것입니다.
이때 Date Range를 사용하면 더 쉽게 누락된 데이터를 찾을 수 있고 처리하여 대응할 수 있습니다.
일자별 주식 데이터에 사전에 만들어둔 Date Range를 조인하여 사용한다면 날짜가 누락된 부분은 빈 공간으로 보여지게 될 것입니다.
빈 공간이 있을때 특정 조건을 걸어 처리하고 매뉴얼화한다면 사용자는 더 올바르게 사용할 수 있을 것입니다. 
 
![img_2.png](/assets/img/post_imgs/2024-02-25-PythonDateRange/img_2.png)

### 3. Date Range 사용하는 방법

---

[방법1. pandas 라이브러리의 date_range 함수를 사용]
```py
import pandas as pd
pd.date_range(start="2024-01-01", end="2024-01-05")
```

[출력결과]
![img.png](/assets/img/post_imgs/2024-02-25-PythonDateRange/img_4.png)


[방법2. 직접 함수로 구현]
```py

from datetime import datetime, timedelta

def date_range(start: str,
               end: str) -> list:

    dates = list()
    delta = timedelta(days=1)
    start_dt = datetime.strptime(start, '%Y-%m-%d').date()
    end_dt = datetime.strptime(end, '%Y-%m-%d').date()

    while start_dt <= end_dt:
        dates.append(datetime.strftime(start_dt, '%Y%m%d'))
        start_dt += delta

    return dates

```

[출력결과]
![img.png](/assets/img/post_imgs/2024-02-25-PythonDateRange/img_3.png)


### 4. 마치며

---
보다 정확한 데이터 처리를 위해 시계열 데이터를 다룰 때 Date Range를 활용하면 더 좋을 것 같습니다.
블로그 내용 중 궁금한 점이 있다면 아래 코멘트로 글 남겨주시면 답변드리도록 하겠습니다.
이상으로 오늘의 포스팅을 마치겠습니다.
감사합니다.

 
