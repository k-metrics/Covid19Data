Covid19 Data
================

本リポジトリでは公開されている Covid19
関連のデータを日次で収集してるリポジトリです。したがいまして個々のデータの著作権は原著作者にあります。個々のデータのライセンに関しては以下のリンク先を参照してください。

  - [Covid19Japan License for
    data](https://github.com/reustle/covid19japan-data/blob/master/LICENSE_for_data)
  - [Googleの利用規約（COVID-19
    感染予測データ](https://policies.google.com/terms?hl=ja)
  - [新型コロナウイルス関連データ・ダウンロードサービス利用規約（NHK）](https://www3.nhk.or.jp/news/special/coronavirus/data/rules.html)

　

## データ

現状では手動トリガーにて取得しているために取得時間はバラバラです（取得後に更新されている可能性があります）。

| ファイル名                              | 内容                      | Encode |
| ---------------------------------- | ----------------------- | ------ |
| covid19japan\_YYYY-MM-DD.csv       | 加工済個票データ                | UTF-8  |
| covid19japan\_YYYY-MM-DD.json      | Covid19Japanのオリジナルデータ   | UTF-8  |
| covid19japan\_YYYY-MM-DD\_json.csv | 上記をCSV形式に変換したもの         | UTF-8  |
| Google\_Forecast\_YYYY-MM-DD.csv   | Googleの予測データ            | UTF-8  |
| NHK\_YYYY-MM-DD.csv                | NHKの都道府県別日時集計（単日・累計）データ | UTF-8  |

`YYYY-MM-DD`は取得日

　

### 加工済個票データ

[Covid19 Japan](https://covid19japan.com/) が GitHub にて公開している
[JSON形式の個票データ（CC
BY-NC 4.0）](https://github.com/reustle/covid19japan-data/tree/master/docs/patient_data)に都道府県関連情報を連結し、必要最低限の項目に絞ったデータです。連結処理にハードルを感じている方はこの加工済個票データを利用してください。

    ##    patientId       date gender detectedPrefecture patientStatus   knownCluster
    ## 1         15 2020-01-15      M           Kanagawa     Recovered           <NA>
    ## 2       TOK1 2020-01-24      M              Tokyo     Recovered           <NA>
    ## 3       TOK2 2020-01-25      F              Tokyo     Recovered           <NA>
    ## 4         18 2020-01-26      M              Aichi          <NA>           <NA>
    ## 5         19 2020-01-28      M              Aichi  Hospitalized           <NA>
    ## 6         20 2020-01-28      M               Nara          <NA>           <NA>
    ## 7       HKD1 2020-01-28      F           Hokkaido    Discharged           <NA>
    ## 8       OSK1 2020-01-29      F              Osaka  Hospitalized           <NA>
    ## 9          1 2020-01-30      M        Unspecified    Discharged Charter Flight
    ## 10        23 2020-01-30      M                Mie     Recovered           <NA>
    ##    confirmedPatient    residence ageBracket     pref     region population
    ## 1              TRUE         <NA>         30 神奈川県   関東地方       9177
    ## 2              TRUE Wuhan, China         40   東京都   関東地方      13822
    ## 3              TRUE Wuhan, China         30   東京都   関東地方      13822
    ## 4              TRUE Wuhan, China         40   愛知県   中部地方       7537
    ## 5              TRUE Wuhan, China         40   愛知県   中部地方       7537
    ## 6              TRUE         Nara         60   奈良県   近畿地方       1339
    ## 7              TRUE Wuhan, China         40   北海道 北海道地方       5286
    ## 8              TRUE        Osaka         40   大阪府   近畿地方       8813
    ## 9              TRUE Wuhan, China         50     <NA>       <NA>         NA
    ## 10             TRUE          Mie         50   三重県   近畿地方       1791

　  
加工済個票のフォーマットは下記の通りです。

| 列名（変量名）            | データ形式      | 説明                                                                                           |
| ------------------ | ---------- | -------------------------------------------------------------------------------------------- |
| patientId          | String     | 陽性判定者の識別情報（厚生労働省のIDとは異なる）                                                                    |
| date               | YYYY-MM-DD | 陽性判定の報告日（検査日ではない）                                                                            |
| gender             | String     | 陽性者の性別（非公開あり）                                                                                |
| detectedPrefecture | String     | 報告主体（都道府県ならびに空港検疫など）                                                                         |
| patientStatus      | String     | 陽性者の状態（[詳細](https://github.com/reustle/covid19japan-data/blob/master/README_data_format.md)） |
| knownCluster       | String     | 陽性者のクラスタに関する情報                                                                               |
| confirmedPatient   | boolean    | FALSEの場合は重複報告などの可能性あり                                                                        |
| residence          | String     | 陽性者の居住地（非公開あり）                                                                               |
| ageBracket         | Numeric    | 陽性者の年代（非公開あり）                                                                                |
| pref               | String     | `detectedPrefecture` の日本語都道府県名                                                               |
| region             | String     | 都道府県の八地方区分名                                                                                  |
| population         | Numeric    | H30年時点の推計人口（単位は千人、出典：統計局）                                                                    |

　  
オリジナルデータのデータフォーマットについては
[こちら](https://github.com/reustle/covid19japan-data/blob/master/README_data_format.md)
を参照してください。なお、オリジナルデータをRを用いて直接読み込みたい場合には、以下のコードを利用してください。

``` r
library(tidyverse)
library(jsonlite)
"https://raw.githubusercontent.com/reustle/covid19japan-data/master/docs/patient_data/latest.json" %>% 
  jsonlite::fromJSON()
```

　  
都道府県地方区分などのデータは下記のリンクから参照してください。  
　

### その他データ

関連データは以下から入手可能です。

  - [Google COVID-19
    感染予測(日本版)](https://datastudio.google.com/u/0/reporting/8224d512-a76e-4d38-91c1-935ba119eb8f/page/ncZpB?s=nXbF2P6La2M)
  - [都道府県地方区分ならびに推計人口](https://gist.github.com/k-metrics/9f3fc18e042850ff24ad9676ac34764b)
  - [新型コロナウイルス対策ダッシュボード](https://www.stopcovid19.jp/)
      - [新型コロナウイルス対策病床オープンデータ](https://docs.google.com/spreadsheets/d/1u0Ul8TgJDqoZMnqFrILyXzTHvuHMht1El7wDZeVrpp8/edit#gid=0)
  - [新型コロナウィルス感染速報](https://covid-2019.live/)
  - [NHK集計データ](https://www3.nhk.or.jp/n-data/opendata/coronavirus/nhk_news_covid19_prefectures_daily_data.csv)
  - [埼玉県オープンデータ（個票）](https://opendata.pref.saitama.lg.jp/data/dataset/covid19-jokyo)
  - [東京都オープンデータ（個票）](https://stopcovid19.metro.tokyo.lg.jp/data/130001_tokyo_covid19_patients.csv)
  - [神奈川県オープンデータ（個票）](https://www.pref.kanagawa.jp/osirase/1369/data/csv/patient.csv)
  - [大阪府オープンデータ（集計）](https://covid19-osaka.info/data/summary.csv)
  - [兵庫県オープンデータ（集計）](https://web.pref.hyogo.lg.jp/kk03/documents/yousei.xlsx)
  - [COVID-19 Data Repository, CSSE Johns Hopkins
    University](https://github.com/CSSEGISandData/COVID-19)

　

## 注意事項・免責事項

  - 本リポジトリは予告なく内容を変更する場合があります
  - 各データの著作権は原著作者にあります
  - 各データを利用したことにより利用者または第三者に損害などが発生しても当方は損害賠償その他一切の責任を負いません

　

Enjoy\!

-----

[CC 4.0
BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.ja),
Sampo Suzuki (Update: 2021-02-23 16:40:25)
