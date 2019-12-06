
## 테스트 설명

### 테스트 툴

호스트 (싱글 코어 1G), Tencent Cloud CDN.

### 테스트 방법

업계에서 통용되는 기본 속도 테스트 방법을 사용하며 서비스 제작사는 TINGYUN입니다.

### 파라미터 테스트

| 테스트 시간   | 2019-05-21 07:45 ~ 2019-05-21 19:15           |
| ---------- | --------------------------------------------- |
| 테스트 도시   | 전체                                          |
| 테스트 ISP | China Unicom, China Telecom, China Mobile                  |
| 원본 서버 링크   | http://*/simptab-wallpaper-20190520181120.png |
| CDN 링크    | http://*/simptab-wallpaper-20190520181120.png |

## 결과 분석

### 지연시간 성능 곡선

단위: 초

![딜레이 그래프](https://main.qcloudimg.com/raw/af4a2f1a8c977561950de6349f9ee755.jpg)

### 가용성 곡선

단위: %

![새로운 가용성 그래프](https://main.qcloudimg.com/raw/e868c5fc16cb145e785620091e1a10e5.jpg)

### 도표 분석

<table>
   <tr>
      <td rowspan="2">모니터링 작업</td>
      <td rowspan="2">모니터링 포인트</td>
      <td colspan="5">성능(초)</td>
      <td colspan="5">가용성(%)</td>
   </tr>
   <tr>
      <td colspan="1">평균값</td>
      <td colspan="2">가장좋음</td>
      <td colspan="2">가장나쁨</td>
      <td colspan="1">평균값</td>
      <td colspan="2">가장좋음</td>
      <td colspan="2">가장나쁨</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>2235</td>
      <td>  0.196</td>
      <td>05월 21일 07:45</td>
      <td>  0.117</td>
      <td>05월 21일 12:15</td>
      <td>  0.313</td>
      <td> 99.996</td>
      <td>05월 21일 07:45</td>
      <td>100.00</td>
      <td>05월 21일 08:45</td>
      <td> 99.91</td>
   </tr>
   <tr>
      <td>원본 서버</td>
      <td>2177</td>
      <td>  0.933</td>
      <td>05월 21일 10:45</td>
      <td>  0.635</td>
      <td>05월 21일 08:15</td>
      <td>  1.827</td>
      <td> 99.035</td>
      <td>05월 21일 07:45</td>
      <td>100.00</td>
      <td>05월 21일 11:15</td>
      <td> 97.65</td>
   </tr>
</table>

### 데이터 세부사항

<table>
   <tr>
      <td rowspan="2">시간</td>
      <td colspan="3">CDN</td>
      <td colspan="3">원본 서버</td>
   </tr>
   <tr>
      <td>성능(초)</td>
      <td>가용성(%)</td>
      <td>모니터링 포인트</td>
      <td>성능(초)</td>
      <td>가용성(%)</td>
      <td>모니터링 포인트</td>
   </tr>
   <tr>
      <td>05월 21일 07:45</td>
      <td>  0.117</td>
      <td>100.00</td>
      <td> 98</td>
      <td>  0.945</td>
      <td>100.00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>05월 21일 08:15</td>
      <td>  0.160</td>
      <td>100.00</td>
      <td> 91</td>
      <td>  1.827</td>
      <td> 98.86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>05월 21일 08:45</td>
      <td>  0.135</td>
      <td> 99.91</td>
      <td> 92</td>
      <td>  0.645</td>
      <td>100.00</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>05월 21일 09:15</td>
      <td>  0.240</td>
      <td>100.00</td>
      <td> 97</td>
      <td>  0.821</td>
      <td> 98.95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>05월 21일 09:45</td>
      <td>  0.190</td>
      <td>100.00</td>
      <td> 95</td>
      <td>  1.315</td>
      <td> 98.80</td>
      <td> 83</td>
   </tr>
   <tr>
      <td>05월 21일 10:15</td>
      <td>  0.158</td>
      <td>100.00</td>
      <td> 95</td>
      <td>  0.745</td>
      <td> 98.95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>05월 21일 10:45</td>
      <td>  0.170</td>
      <td>100.00</td>
      <td> 90</td>
      <td>  0.635</td>
      <td>100.00</td>
      <td> 89</td>
   </tr>
   <tr>
      <td>05월 21일 11:15</td>
      <td>  0.123</td>
      <td>100.00</td>
      <td> 90</td>
      <td>  0.692</td>
      <td> 97.65</td>
      <td> 85</td>
   </tr>
   <tr>
      <td>05월 21일 11:45</td>
      <td>  0.246</td>
      <td>100.00</td>
      <td> 96</td>
      <td>  0.653</td>
      <td>100.00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>05월 21일 12:15</td>
      <td>  0.313</td>
      <td>100.00</td>
      <td> 89</td>
      <td>  0.763</td>
      <td> 97.83</td>
      <td> 92</td>
   </tr>
   <tr>
      <td>05월 21일 12:45</td>
      <td>  0.258</td>
      <td>100.00</td>
      <td> 92</td>
      <td>  1.181</td>
      <td>100.00</td>
      <td> 93</td>
   </tr>
   <tr>
      <td>05월 21일 13:15</td>
      <td>  0.175</td>
      <td>100.00</td>
      <td> 95</td>
      <td>  1.122</td>
      <td> 97.67</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>05월 21일 13:45</td>
      <td>  0.173</td>
      <td>100.00</td>
      <td> 97</td>
      <td>  1.148</td>
      <td> 98.89</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>05월 21일 14:15</td>
      <td>  0.257</td>
      <td>100.00</td>
      <td> 81</td>
      <td>  1.083</td>
      <td>100.00</td>
      <td> 81</td>
   </tr>
   <tr>
      <td>05월 21일 14:45</td>
      <td>  0.214</td>
      <td>100.00</td>
      <td>103</td>
      <td>  1.044</td>
      <td>100.00</td>
      <td> 97</td>
   </tr>
   <tr>
      <td>05월 21일 15:15</td>
      <td>  0.240</td>
      <td>100.00</td>
      <td> 92</td>
      <td>  0.737</td>
      <td> 97.98</td>
      <td> 99</td>
   </tr>
   <tr>
      <td>05월 21일 15:45</td>
      <td>  0.169</td>
      <td>100.00</td>
      <td> 94</td>
      <td>  0.969</td>
      <td> 98.85</td>
      <td> 87</td>
   </tr>
   <tr>
      <td>05월 21일 16:15</td>
      <td>  0.146</td>
      <td>100.00</td>
      <td> 93</td>
      <td>  0.769</td>
      <td> 98.86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>05월 21일 16:45</td>
      <td>  0.269</td>
      <td>100.00</td>
      <td> 91</td>
      <td>  0.724</td>
      <td>100.00</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>05월 21일 17:15</td>
      <td>  0.181</td>
      <td>100.00</td>
      <td> 91</td>
      <td>  1.072</td>
      <td> 98.02</td>
      <td>101</td>
   </tr>
   <tr>
      <td>05월 21일 17:45</td>
      <td>  0.208</td>
      <td>100.00</td>
      <td> 96</td>
      <td>  1.000</td>
      <td>100.00</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>05월 21일 18:15</td>
      <td>  0.219</td>
      <td>100.00</td>
      <td> 94</td>
      <td>  0.744</td>
      <td> 98.86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>05월 21일 18:45</td>
      <td>  0.119</td>
      <td>100.00</td>
      <td> 81</td>
      <td>  0.841</td>
      <td> 98.84</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>05월 21일 19:15</td>
      <td>  0.212</td>
      <td>100.00</td>
      <td>102</td>
      <td>  0.981</td>
      <td> 97.87</td>
      <td> 94</td>
   </tr>
   <tr>
      <td>평균/합계</td>
      <td>  0.196</td>
      <td> 99.996</td>
      <td>2235</td>
      <td>  0.933</td>
      <td> 99.04</td>
      <td>2177</td>
   </tr>
   <tr>
      <td>포인트 제거</td>
      <td colspan="3">  0</td>
      <td colspan="3">  0</td>
   </tr>
</table>
