## Application Service > Maps > API v3.0ガイド

inaviの長年培ったナビエンジン技術を利用した検索、Geocoding、Reverse Geocoding、経路検索(ルート検索)、Static Map APIの使用方法について説明します。

## API共通情報

### 事前準備

* APIを使用するにはアプリケーションキーが必要です。
* アプリケーションキーは、**NHN Cloud Console**上部の**URL & Appkey**メニューで確認できます。

### リクエスト共通情報

#### URL情報

| 環境 | ドメイン                          |
| ---- | -------------------------------- |
| Real | https://kr1-maps.api.nhncloudservice.com |

#### Header情報

| Header 名   | 値                             |
| ---- | -------------------------------- |
| User-Agent | `Windows`, `Android`, `Mac OS` |

### レスポンス共通情報

#### 検索API

* すべてのAPIリクエストに「200 OK」でレスポンスします。詳細なレスポンス結果はレスポンス本文のヘッダを参照します。

```
{
	"header": {
		"isSuccessful": true,
		"resultCode": 0,
		"resultMessage": ""
	}
}
```

## 検索

### 1\. 統合検索

* 商号名、電話番号、住所などのキーワードで統合情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/searches?query={query}&coordtype={coordtype}&startposition={startposition}&reqcount={reqcount}&spopt={spopt}&radius={radius}&admcode={admcode}&depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&sortopt={sortopt}&catecode={catecode}&addrext={addrext} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前        | タイプ | 要否 | 有効範囲 | 説明                                   |
| ------------- | ------ | ----- | ----- | ---------------------------------------- |
| query         | String | 必須 |       | 検索ワード                                  |
| coordtype     | String | 任意 |       | 座標形式<br>0：TW座標<br>1：WGS84座標<br>2：TM座標 |
| startposition | String | 任意 |       | 検索開始位置<br>0：最初の位置、未入力の時は0で照会 |
| reqcount      | String | 任意 |       | 検索リクエスト数<br>0に設定するとMax Countを返す     |
| spopt         | String | 任意 |       | 空間検索オプション<br>0：空間検索を使用しない<br>1：Extent検索<br>2：Range検索<br>* spopt値が未設定の場合は0に設定 |
| radius        | String | 任意 |       | 半径<br>spopt値が2の場合、使用<br>メートル単位          |
| admcode       | String | 任意 |       | 行政コード                                |
| depth         | String | 選択     |           | 下位施設要求水準<br>0: 0 POI表示時、親/Subを区分せずに全て表示<br>1: 1 POI表示時、親POIのみ表示してSub-POIはカウントのみ提供<br>2: 2 POI表示時、親POI下位にSub-POIを別途グループ化して表示<br>3: 3 POI表示時、親POI下位にSub-POIを別途グループ化して表示、<br> Sub-POI内に下位Sub-POIが存在する場合、下位depth 表示<br>※オプション選択がない場合Defaultは0に設定される |
| x1            | String | 任意 |       | x1座標<br>spopt値が0の場合、基準点x座標<br>spopt値が1の場合、Extentの左上x座標<br>spopt値が2の場合、基準点x座標 |
| y1            | String | 任意 |       | y1座標<br>spopt値が0の場合、基準点y座標<br>spopt値が1の場合、Extentの左上y座標<br>spopt値が2の場合、基準点y座標 |
| x2            | String | 任意 |       | x2座標<br>spopt値が1の場合、Extentの右下x座標、spopt値が2の場合、使用しない |
| y2            | String | 任意 |       | y2座標<br>spopt値が1の場合、Extentの右下y座標、spopt値が2の場合、使用しない |
| sortopt       | String | 任意 |       | ソートoption<br>1：名称順ソート<br>2：距離順ソート(座標を入力した場合)<br>3：名前マッチ(座標を入力した場合、座標から距離順で追加ソート)<br>4：検索ワード重みソート(エンジン基準)<br>* sortopt値が未設定の場合、4に設定 |
| addrext       | String | 任意     |           | 地番/建物番号拡張検索オプション<br>0:正確に一致<br>1: 敷地番号拡張<br>2: 本地番拡張<br>* オプション選択がない場合、Defaultは0に設定される |


#### レスポンス

##### レスポンス本文

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    },
    "search": {
        "result": true,
        "type": 0,
        "totalcount": 1,
        "count": 1,
        "poitotalcount": 1,
        "poicount": 1,
        "ucp_poitotalcount": 0,
        "ucp_poicount": 0,
        "tel_poitotalcount": 0,
        "tel_poicount": 0,
        "admtotalcount": 0,
        "admcount": 0,
        "reftotalcount": 0,
        "refcount": 0,
        "res_type": "YYYY",
        "poi": [
            {
                "poiid": 4722977,
                "depth": 0,
                "dpx": "169031",
                "dpy": "517906",
                "rpx": "169039",
                "rpy": "517941",
                "name1": "Samhwan HIPEX",
                "name2": "ハイペックス",
                "name3": "SamhwanハイPEX",
                "name4": "ハイPEX",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "京畿道城南市盆唐区三坪洞",
                "roadname": "京畿道城南市盆唐区板橋駅路",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "130301",
                "catename": "企業",
                "dp_catecode": "150",
                "userid": "",
                "imagecount": 0,
                "userimagecount": 0,
                "badgeflag": false,
                "distance": 0,
                "tel": "",
                "islandmark": false,
                "updateTS": "2017-10-12 00:00:00",
                "data_source": "Thinkware",
                "hasoildata": false,
                "hasdetailinfo": false,
                "hassubpoi": true,
                "subpoi": {
                    "count": 5,
                    "poi": [
                        {
                            "poiid": 4828295,
                            "depth": 1,
                            "dpx": "169031",
                            "dpy": "517910",
                            "rpx": "169039",
                            "rpy": "517941",
                            "name1": "A棟",
                            "name2": "Samhwan HIPEX A棟",
                            "name3": "",
                            "name4": "",
                            "admcode": "4113510900",
                            "jibun": "678",
                            "address": "京畿道城南市盆唐区三坪洞",
                            "roadname": "京畿道城南市盆唐区板橋駅路",
                            "roadjibun": "240",
                            "detailaddress": "",
                            "catecode": "130301",
                            "catename": "企業",
                            "dp_catecode": "150",
                            "userid": "",
                            "imagecount": 0,
                            "userimagecount": 0,
                            "badgeflag": false,
                            "distance": 0,
                            "tel": "",
                            "islandmark": false,
                            "updateTS": "2017-10-13 00:00:00",
                            "hasoildata": false,
                            "hasdetailinfo": false,
                            "hassubpoi": true,
                            "subpoi": {
                                "count": 36,
                                "poi": [
                                    {
                                        "poiid": 4722978,
                                        "depth": 2,
                                        "dpx": "169039",
                                        "dpy": "517941",
                                        "rpx": "169039",
                                        "rpy": "517941",
                                        "name1": "入口",
                                        "name2": "",
                                        "name3": "",
                                        "name4": "",
                                        "admcode": "4113510900",
                                        "jibun": "678",
                                        "address": "京畿道城南市盆唐区三坪洞",
                                        "roadname": "",
                                        "roadjibun": "",
                                        "detailaddress": "",
                                        "catecode": "181100",
                                        "catename": "道路施設",
                                        "dp_catecode": "000",
                                        "userid": "",
                                        "imagecount": 0,
                                        "userimagecount": 0,
                                        "badgeflag": false,
                                        "distance": 0,
                                        "tel": "",
                                        "islandmark": false,
                                        "updateTS": "2017-10-13 00:00:00",
                                        "hasoildata": false,
                                        "hasdetailinfo": false,
                                        "hassubpoi": false
                                    },
		....
		]
	}
}
```

##### フィールド

| 名前                           | タイプ  | 説明                                   |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | ヘッダ領域                                |
| header.isSuccessful              | Boolean | 成否                                |
| header.resultCode                | Integer | 失敗コード                                |
| header.resultMessage             | String  | 失敗メッセージ                               |
| search                           | Object  | 本文領域                                |
| search.result                    | Boolean | 成否                                |
| search.type                      | Integer | 0：一般検索<br>1：Reference検索        |
| search.totalcount                | Integer | 全体検索結果対象数                        |
| search.count                     | Integer | 検索結果数                              |
| search.poitotalcount             | Integer | 全体検索結果対象数(Thinkware POI)            |
| search.poicount                  | Integer | 検索結果数(Thinkware POI)                  |
| search.tel_poitotalcount         | Integer | 全体検索結果対象数(Tel POI)                  |
| search.tel_poicount              | Integer | 検索結果数(Tel POI)                        |
| search.ucp_poitotalcount         | Integer | 全体検索結果対象数(User POI)                 |
| search.ucp_poicount              | Integer | 検索結果数(User POI)                       |
| search.admtotalcount             | Integer | ADM全体検索結果対象数                    |
| search.admcount                  | Integer | ADM検索結果数                          |
| search.reftotalcount             | Integer | ref全体検索結果対象数                    |
| search.refcount                  | Integer | ref検索結果数                          |
| search.res_type                  | String  | 検索結果Type名称<br>名称、カテゴリー、住所、電話番号順<br>(例) NYNN：名称No、カテゴリーYES、住所NO、電話番号NO |
| search.poi                       | Array   | POI検索結果リスト                         |
| search.poi[0].poiid              | Integer | POI ID                                   |
| search.poi[0].depth              | String  | POI depth                                |
| search.poi[0].dpx                | String  | display x座標(WGS84の場合longitude)         |
| search.poi[0].dpy                | String  | display y座標(WGS84の場合latitude)          |
| search.poi[0].rpx                | String  | 探索x座標(WGS84の場合longitude)              |
| search.poi[0].rpy                | String  | 探索y座標(WGS84の場合latitude)               |
| search.poi[0].name1              | String  | 正式名称                                |
| search.poi[0].name2              | String  | 略称                                |
| search.poi[0].name3              | String  | 拡張名称1                                  |
| search.poi[0].name4              | String  | 拡張名称2                                  |
| search.poi[0].admcode            | String  | 行政コード                                |
| search.poi[0].address            | String  | 住所                                   |
| search.poi[0].jibun              | String  | 地番                                    |
| search.poi[0].roadname           | String  | 新しい住所道路名                               |
| search.poi[0].roadjibun          | String  | 新しい住所地番                                |
| search.poi[0].detailaddress      | String  | 詳細住所                                |
| search.poi[0].catecode           | String  | 分類コード                                |
| search.poi[0].catename           | String  | 分類名称                                |
| search.poi[0].dp_catecode        | String  | DP分類コード                             |
| search.poi[0].distance           | Integer | 座標との距離(該当する時のみ)                          |
| search.poi[0].tel                | String  | 電話番号                                 |
| search.poi[0].hasoildata         | Boolean | ガソリン価格データ有無                          |
| search.poi[0].hasdetailinfo      | Boolean | 詳細情報有無                           |
| search.poi[0].hassubpoi          | Boolean | 下位施設有無                          |
|| search.poi[0].islandmark         | Boolean | ランドマークかどうか                               |
| search.poi[0].updateTS           | String  | 最終変更日時(Y4-MM-DD HH：mm：ss)フォーマット        |
| search.poi[0].imagecount         | Integer | POIイメージ数                            |
| search.poi[0].oildata            | Object  | ガソリン価格データ情報                            |
| search.poi[0].oildata.g_price    | Integer | レギュラー価格                               |
| search.poi[0].oildata.hg_price   | Integer | ハイオク価格                            |
| search.poi[0].oildata.d_price    | Integer | 軽油価格                                |
| search.poi[0].oildata.l_price    | Integer | LPG価格                               |
| search.poi[0].oildata.updatetime | String  | アップデート時間                              |
| search.poi[0].oildata.priceinfo  | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| search.poi[0].oildata.wash       | Boolean | 洗車施設有無                              |
| search.poi[0].oildata.fix        | Boolean | 整備可否                              |
| search.poi[0].oildata.mart       | Boolean | 売店有無                                 |
| search.poi[0].subpoi             | Object  | 下位施設情報                            |
| search.poi[0].subpoi.count       | Integer | 下位施設の数                             |
| search.poi[0].subpoi.poi         | Array   | POI情報と同じ                            |
| search.tel                       | Array   | TEL検索結果リスト(POI情報と同じ)                |
| search.adm                       | Array   | ADM検索結果リスト                         |
| search.adm[0].type               | String  | 検索type<br>1：行政系検索<br>2：地番検索<br>3：新住所検索 |
| search.adm[0].posx               | String  | x座標(WGS84の場合longitude)                 |
| search.adm[0].posy               | String  | y座標(WGS84の場合latitude)                  |
| search.adm[0].admcode            | String  | 行政コード                                 |
| search.adm[0].address            | String  | 住所                                   |
| search.adm[0].jibun              | String  | 地番                                    |
| search.adm[0].roadname           | String  | 新住所道路名                               |
| search.adm[0].roadjibun          | String  | 新住所地番                                |
| search.adm[0].accuracy           | Integer | 地番の正確度<br>0：正確検索<br>1：枝番拡張<br>2：親番拡張 |
| search.hasgasstation             | Boolean | ガソリン価格情報提供有無                           |
| search.oilprice                  | Object  | ガソリン価格情報                                |
| search.oilprice.max_g_price      | Integer | 最高レギュラー価格                            |
| search.oilprice.min_g_price      | Integer | 最低レギュラー価格                            |
| search.oilprice.avg_g_price      | Integer | 平均レギュラー価格                            |
| search\.oilprice\.max\_hg\_price | Integer | 最高ハイオク価格                         |
| search\.oilprice\.min\_hg\_price | Integer | 最低ハイオク価格                         |
| search\.oilprice\.avg\_hg\_price | Integer | 平均ハイオク価格                         |
| search.oilprice.max_d_price      | Integer | 最高軽油価格                             |
| search.oilprice.min_d_price      | Integer | 最低軽油価格                             |
| search.oilprice.avg_d_price      | Integer | 平均軽油価格                             |
| search.oilprice.max_l_price      | Integer | 最高LPG価格                            |
| search.oilprice.min_l_price      | Integer | 最低LPG価格                            |
| search.oilprice.avg_l_price      | Integer | 平均LPG価格                            |


### 2\. 推薦ワード検索

* 検索ワードの推薦ワードを検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/proposers?query={query} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明                 |
| ----- | ------ | ----- | ----- | ---------------------- |
| query | String | 必須 | 50バイト | ハングル/英語/数字50バイト(ハングル25文字) |

#### レスポンス

##### レスポンス本文

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "proposer": {
    "result": true,
    "count": 10,
    "keyword": [
      {
        "keyword": "パンギョ駅",
        "frequency": 3729938
      },
      {
        "keyword": "パンギョ",
        "frequency": 3729326
      },
      {
        "keyword": "パンギョIC",
        "frequency": 3729362
      },
      {
        "keyword": "パンギョ図書館",
        "frequency": 3729514
      },
      {
        "keyword": "パンギョウォンマウル",
        "frequency": 3730051
      },
      {
        "keyword": "パンギョロッテマート",
        "frequency": 3729602
      },
      {
        "keyword": "パンギョInnovalley",
        "frequency": 3730186
      },
      {
        "keyword": "パンギョ博物館",
        "frequency": 3729654
      },
      {
        "keyword": "パンギョ中学校",
        "frequency": 3730256
      },
      {
        "keyword": "パンギョマリオット",
        "frequency": 3729626
      }
    ]
  }
}
```

##### フィールド

| 名前                        | タイプ  | 説明    |
| ----------------------------- | ------- | --------- |
| header                        | Object  | ヘッダ領域 |
| header.isSuccessful           | Boolean | 成否 |
| header.resultCode             | Integer | 失敗コード |
| header.resultMessage          | String  | 失敗メッセージ |
| proposer                      | Object  | 本文領域 |
| proposer.result               | Boolean | 成否 |
| proposer.count                | Integer | 推薦検索ワード数 |
| proposer.keyword              | Array   | 推薦検索ワードリスト |
| proposer.keyword[0].keyword   | String  | 推薦検索ワード |
| proposer.keyword[0].frequency | Integer | 照会頻度 |

### 3\. POI詳細検索

* POIの詳細情報を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/pois?poiid={poiid} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明                                   |
| ----- | ------ | ----- | ----- | ---------------------------------------- |
| poiid | String | 必須 | 186個 | POI ID<br>poiidをセパレータ","で区切って入力<br>(複数可能186個まで)<br>例) poiid=123,234,567 |

#### レスポンス

##### レスポンス本文

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "poi": {
    "result": true,
    "totalcount": 2,
    "count": 2,
    "poiinfo": [
      {
				"poiid": 510835.0,
        "dpx": "127.059664",
        "dpy": "37.508629",
        "rpx": "127.059089",
        "rpy": "37.508779",
        "name1": "現代百貨店(貿易センター店)",
        "name2": "現代百貨店貿易センター店",
        "name3": "貿易センター現代百貨店",
        "name4": "",
        "admcode": "1168010500",
        "jibun": "159-7",
        "address": "ソウル特別市江南区三成洞",
        "roadname": "ソウル特別市江南区三成洞テヘラン路",
        "roadjibun": "517",
        "detailaddress": "",
        "fulladdress": "ソウル特別市江南区三成洞159-7 ",
        "zip": "",
        "homepage": "http://www.e-hyundai.com",
        "email": "",
        "howtogo": "",
        "tel1": "025522233",
        "tel2": "",
        "fax1": "",
        "fax2": "",
        "catecode": "110102",
        "catename": "ショッピング",
        "dp_catecode": "250",
        "icode": "493-070-3606",
        "externallink": [],
        "detail_count": 10,
        "etc_count": 2,
        "imagecount": 0,
        "badgeflag": false,
        "detailinfo": [
          {
            "name": "休業日",
            "value": "毎月2回休業"
          },
          {
            "name": "営業時間",
            "value": "10:30~20:00"
          },
          {
            "name": "駐車",
            "value": "1400台可能"
          },
          {
            "name": "駐車料",
            "value": "1万KRW以上購入時、1時間無料"
          },
          {
            "name": "付帯施設1",
            "value": "エメラルドホール(イベントホール)"
          },
          {
            "name": "付帯施設2",
            "value": "テラスガーデン"
          },
          {
            "name": "規模",
            "value": "地上10階地下4階"
          },
          {
            "name": "フロア情報1",
            "value": "1階名品雑貨/2階ファッション雑貨"
          },
          {
            "name": "フロア情報2",
            "value": "3～4階女性衣類/6階ゴルフウェア"
          },
          {
            "name": "フロア情報3",
            "value": "9階飲食店街/10階催事場"
          }
        ],
        "etcinfo": [
          {
            "name": "その他1",
            "value": "金融の中心地であるテヘラン路の中心部に位置"
          },
          {
            "name": "その他2",
            "value": "全世界から韓国を訪ねる観光客を満足させる韓国流通のショーウィンドウ"
          }
        ],
        "hasoildata": false
      },
      ....
    ]
  }
}
```

##### フィールド

| 名前                             | タイプ  | 説明                                   |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                           |
| header.isSuccessful                | Boolean | 成否                           |
| header.resultCode                  | Integer | 失敗コード                           |
| header.resultMessage               | String  | 失敗メッセージ                          |
| poi                                | Object  | 本文領域                           |
| poi.result                         | Boolean | 成否                           |
| poi.totalcount                     | Integer | 全体検索結果対象数                    |
| poi.count                          | Integer | 検索結果数                          |
| poi.poiinfo                        | Array   | POI検索結果リスト                    |
| poi.poiinfo[0].poiid               | Integer | POI ID                                   |
| poi.poiinfo[0].dpx                 | String  | display x座標(WGS84の場合longitude)         |
| poi.poiinfo[0].dpy                 | String  | display y座標(WGS84の場合latitude)          |
| poi.poiinfo[0].rpx                 | String  | 探索x座標(WGS84の場合longitude)              |
| poi.poiinfo[0].rpy                 | String  | 探索y座標(WGS84の場合latitude)               |
| poi.poiinfo[0].name1               | String  | 正式名称                             |
| poi.poiinfo[0].name2               | String  | 略称                             |
| poi.poiinfo[0].name3               | String  | 拡張名称1                                  |
| poi.poiinfo[0].name4               | String  | 拡張名称2                                  |
| poi.poiinfo[0].admcode             | String  | 行政コード                           |
| poi.poiinfo[0].jibun               | String  | 地番                                |
| poi.poiinfo[0].address             | String  | 住所                              |
| poi.poiinfo[0].roadname            | String  | 新住所の道路名                           |
| poi.poiinfo[0].roadjibun           | String  | 新住所の地番                            |
| poi.poiinfo[0].detailaddress       | String  | 詳細住所                           |
| poi.poiinfo[0].catecode            | String  | 分類コード                           |
| poi.poiinfo[0].catename            | String  | 分類名称                             |
| poi.poiinfo[0].fulladdress         | String  | 全体住所(行政住所+地番+詳細住所)                      |
| poi.poiinfo[0].zip                 | String  | 郵便番号                            |
| poi.poiinfo[0].homeage             | String  | Webサイトurl                                 |
| poi.poiinfo[0].email               | String  | メール                             |
| poi.poiinfo[0].howtogo             | String  | 交通手段                               |
| poi.poiinfo[0].tel1                | String  | 電話番号1                                   |
| poi.poiinfo[0].tel2                | String  | 電話番号2                                   |
| poi.poiinfo[0].fax1                | String  | Fax番号1                                   |
| poi.poiinfo[0].fax2                | String  | Fax番号2                                   |
| poi.poiinfo[0].icode               | String  | ICODE                                    |
| poi.poiinfo[0].detail_count        | Integer | 分類詳細項目数                       |
| poi.poiinfo[0].etc_count           | Integer | 分類その他項目数                       |
| poi.poiinfo[0].imagecount          | Integer | POIイメージ数                        |
| poi.poiinfo[0].hasoildata          | Boolean | ガソリン価格データの有無                      |
| poi.poiinfo[0].detailinfo          | Array   | 分類詳細項目                        |
| poi.poiinfo[0].detailinfo[0].name  | String  | 分類詳細項目説明                     |
| poi.poiinfo[0].detailinfo[0].value | String  | 分類詳細項目内容                     |
| poi.poiinfo[0].etcinfo             | Array   | 分類その他項目                        |
| poi.poiinfo[0].etcinfo[0].name     | String  | 分類その他項目説明                     |
| poi.poiinfo[0].etcinfo[0].value    | String  | 分類その他項目内容                     |
| poi.poiinfo[0].oildata             | Object  | ガソリン価格データ情報                       |
| poi.poiinfo[0].oilda.tag_price     | Integer | レギュラー価格                          |
| poi.poiinfo[0].oilda.hg_price      | Integer | ハイオク価格                        |
| poi.poiinfo[0].oilda.d_price       | Integer | 軽油価格                           |
| poi.poiinfo[0].oilda.l_price       | Integer | LPG価格                          |
| poi.poiinfo[0].oilda.updatetime    | String  | アップデート時間                         |
| poi.poiinfo[0].oilda.priceinfo     | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| poi.poiinfo[0].oilda.wash          | Boolean | 洗車施設有無                          |
| poi.poiinfo[0].oilda.fix           | Boolean | 整備可否                          |
| poi.poiinfo[0].oilda.mart          | Boolean | 売店有無                             |

### 4\. POI下位施設検索

* 特定POIの下位施設を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/sub-pois?poiid={poiid}&x1={x1}&y1={y1} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前 | タイプ | 要否 | 有効範囲                           | 説明         |
| ----- | ------ | ----- | ---------------------------------------- | ------------------- |
| poiid | String | 必須 |                                          | POI ID<br>複数サポートされない |
| x1    | String | 任意 | 現在地またはマップ中心座標<br>x、y座標がすべてNULLまたは0の場合、距離計算を実行しない |                     |
| x1    | String | 任意 | 現在地またはマップ中心座標<br>x、y座標がすべてNULLまたは0の場合、距離計算を実行しない |                     |

#### レスポンス

##### レスポンス本文

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
	"subpoi": {
        "result": true,
        "totalcount": 1,
        "count": 1,
        "poi": [
            {
                "poiid": 1415980,
                "depth": 1,
                "dpx": "127.110862",
                "dpy": "37.402334",
                "rpx": "127.110862",
                "rpy": "37.402334",
                "name1": "正門",
                "name2": "THINKWARE正門",
                "name3": "",
                "name4": "",
                "admcode": "4113510900",
                "jibun": "678",
                "address": "京畿道城南市盆唐区三坪洞",
                "roadname": "京畿道城南市盆唐区板橋駅路",
                "roadjibun": "240",
                "detailaddress": "",
                "catecode": "181100",
                "catename": "道路施設",
                "dp_catecode": "000",
                "userid": "",
                "imagecount": 0,
                "userimagecount": 0,
                "badgeflag": false,
                "distance": 12164030,
                "tel": "",
                "islandmark": false,
                "visitscore": "0",
                "landmarkscore": "0",
                "popularity": false,
                "pop_tv": false,
                "pop_sns": false,
                "pop_hot": false,
                "pop_hit": false,
                "pop_top": "",
                "updateTS": "1970-01-01 09:00:00",
                "hasoildata": false,
                "hasdetailinfo": false,
                "hassubpoi": false
            }...
    		]
  	}
}
```

##### フィールド

| 名前                      | タイプ | 説明                              |
| -------------------------------- | ------- | ---------------------------------------- |
| header                           | Object  | ヘッダ領域                           |
| header.isSuccessful              | Boolean | 成否                           |
| header.resultCode                | Integer | 失敗コード                           |
| header.resultMessage             | String  | 失敗メッセージ                          |
| subpoi                           | Object  | 本文領域                           |
| subpoi.result                    | Boolean | 成否                           |
| subpoi.totalcount                | Integer  | 全体検索結果対象数                          |
| subpoi.count                     | Integer  | 検索結果数                               |
| subpoi.poi                       | Array   | POI検索結果リスト                    |
| subpoi.poi[0].poiid              | Integer | POI ID                                   |
| subpoi.poi[0].depth              | String  | POI depth                                |
| subpoi.poi[0].dpx                | String  | display x座標(WGS84の場合、longitude)         |
| subpoi.poi[0].dpy                | String  | display y座標(WGS84の場合、latitude)          |
| subpoi.poi[0].rpx                | String  | 探索x座標(WGS84の場合、longitude)              |
| subpoi.poi[0].rpy                | String  | 探索y座標(WGS84の場合、latitude)               |
| subpoi.poi[0].name1              | String  | 正式名称                              |
| subpoi.poi[0].name2              | String  | 略称                              |
| subpoi.poi[0].name3              | String  | 拡張名称1                                    |
| subpoi.poi[0].name4              | String  | 拡張名称2                                    |
| subpoi.poi[0].admcode            | String  | 行政コード                            |
| subpoi.poi[0].address            | String  | 住所                              |
| subpoi.poi[0].jibun              | String  | 地番                                |
| subpoi.poi[0].roadname           | String  | 新住所の道路名                           |
| subpoi.poi[0].roadjibun          | String  | 新住所の地番                            |
| subpoi.poi[0].detailaddress      | String  | 詳細住所                            |
| subpoi.poi[0].catecode           | String  | 分類コード                            |
| subpoi.poi[0].catename           | String  | 分類名称                              |
| subpoi.poi[0].dp_catecode        | String  | DP分類コード                         |
| subpoi.poi[0].distance           | Integer | 座標との距離(該当する時のみ)                         |
| subpoi.poi[0].tel                | String  | 電話番号                            |
| subpoi.poi[0].hasoildata         | Boolean | ガソリン価格データの有無                      |
| subpoi.poi[0].hasdetailinfo      | Boolean | 詳細情報の有無                        |
| subpoi.poi[0].hassubpoi          | Boolean | 下位施設の有無                        |
| subpoi.poi[0].adv_count          | Boolean | 広告コード数                          |
| subpoi.poi[0].islandmark         | Boolean | ランドマークかどうか                           |
| subpoi.poi[0].updateTS           | String  | 最終変更日時(Y4-MM-DD HH:mm:ss)フォーマット    |
| subpoi.poi[0].data_source        | String  | POI作成情報区分(Thinkware/Tel/User)        |
| subpoi.poi[0].badgeflag          | Boolean | バッジ有無(Not Yet: FALSE, Badged: TRUE)      |
| subpoi.poi[0].userid             | String  | POI登録ユーザーID (UCPの場合にのみ)                |
| subpoi.poi[0].imagecount         | Integer | POIイメージ数                        |
| subpoi.poi[0].oildata            | Object  | ガソリン価格データ情報                       |
| subpoi.poi[0].oildata.g_price    | Integer | レギュラー価格                          |
| subpoi.poi[0].oildata.hg_price   | Integer | ハイオク価格                        |
| subpoi.poi[0].oildata.d_price    | Integer | 軽油価格                           |
| subpoi.poi[0].oildata.l_price    | Integer | LPG価格                          |
| subpoi.poi[0].oildata.updatetime | String  | Update時間                       |
| subpoi.poi[0].oildata.priceinfo  | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| subpoi.poi[0].oildata.wash       | Boolean | 洗車施設有無                            |
| subpoi.poi[0].oildata.fix        | Boolean | 整備可否                            |
| subpoi.poi[0].oildata.mart       | Boolean | 売店有無                              |
| subpoi.poi[0].AdInfo             | Array   | 広告コードリスト                        |
| subpoi.poi[0].AdInfo[0].ADCODE   | Integer | 広告コード<br>1～99まで付与可能(最大99個)              |
| subpoi.poi[0].subpoi             | Object  | 下位施設情報                       |
| subpoi.poi[0].subpoi.count       | Integer | subpoi数                         |
| subpoi.poi[0].subpoi.poi         | Array   | POI情報と同じ                        |

### 5\. 座標変換

* WGS84 ⇔ TM座標間の変換値を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/trans-coordinates?coordtype={coordtype}&x={x}&y={y} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前 | タイプ | 要否 | 有効範囲                        | 説明                          |
| --------- | ------ | ----- | ------------------------------------- | ------------------------------------ |
| coordtype | String | 必須 |                                       | 0：WGS84 → TM <br> 1：TM → WGS84 |
| x         | String | 必須 | 現在地またはマップ中心座標<br>WGS84座標またはTM座標 |                                      |
| y         | String | 必須 | 現在地またはマップ中心座標<br>WGS84座標またはTM座標 |                                      |

#### レスポンス

##### レスポンス本文

```
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": ""
  },
  "coordinate": {
    "coordtype": "WGS84",
    "x": "128.662952",
    "y": "38.058678"
  }
}
```





##### フィールド

| 名前          | タイプ | 説明 |
| -------------------- | ------- | -------- |
| header               | Object  | ヘッダ領域 |
| header.isSuccessful  | Boolean | 成否 |
| header.resultCode    | Integer | 失敗コード |
| header.resultMessage | String  | 失敗メッセージ |
| coordinate           | Object  | 本文領域 |
| coordinate.coordtype | String  | 変換座標形式 |
| coordinate.x         | String  | 変換x座標 |
| coordinate.y         | String  | 変換y座標 |

### 6\. 周辺カテゴリー検索

* 基準座標を基準とした周辺カテゴリー検索機能をサポートします。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/nearby-category-searches?depth={depth}&x1={x1}&y1={y1}&x2={x2}&y2={y2}&radius={radius}&catecode={catecode}&coordtype={coordtype}&reqcount={reqcount}  |

[Path parameter]

| 名前   | タイプ   | 要否 | 有効範囲 | 説明   |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須  |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前      | タイプ   | 要否 | 説明                                 |
| --------- | ------ | ----- |  ------------------------------------ |
| catecode         | String | 必須 | カテゴリーコード |
| spopt         | Integer | 必須 | 1：Extent(x1,y1,x2,y2) <br> 2：半径検索(x1,y1,radius)                                   |
| x1         | String | 必須(spopt参照)    | 基準x1座標 |
| y1         | String | 必須(spopt参照)    | 基準y1座標 |
| x2         | String | 必須(spopt参照)    | 基準x2座標 |
| y2         | String | 必須(spopt参照)    | 基準y2座標 |
| radius         | String | 必須(spopt参照)    | 半径(m) |
| depth | String | 任意  | 0：全体depth <br> 1： depth1 <br> 2： depth2 <br> 3： depth3|
| sortopt | String | 任意  | ソートオプション <br> 1：距離順 <br> 2：名称順<br> 3：レギュラー価格順(ガソリンスタンド検索時) <br> 4：ハイオク価格順(ガソリンスタンド検索時)<br> 5：軽油価格順(ガソリンスタンド検索時)<br> 6：LPG価格順(ガソリンスタンド検索時)<br> 7：スコア順|
| reqcount | String | 任意  | 表示する検索結果数|

#### レスポンス

##### レスポンス本文

```
{
	"cate": {
			"result": true,
			"totalcount": 10,
			"count": 10,
			"poi": [
					{
							"poiid": 717788,
							"depth": 0,
							"dpx": "127.110762",
							"dpy": "37.402184",
							"rpx": "127.110862",
							"rpy": "37.402334",
							"name1": "THINKWARE (株)",
							"name2": "inavi(本社)",
							"name3": "THINKWARE",
							"name4": "INAVI",
							"admcode": "4113510900",
							"jibun": "678",
							 "address": "京畿道城南市盆唐区三坪洞",
							"roadname": "京畿道城南市盆唐区板橋駅路",
							"roadjibun": "240",
							"detailaddress": "Samhwan HIPEX A棟8階、9階",
							"catecode": "130600",
							"catename": "企業",
							"dp_catecode": "000",
							"userid": "",
							"imagecount": 0,
							"userimagecount": 0,
							"badgeflag": false,
							"distance": 27,
							"tel": "1577-4242",
							"islandmark": true,
							"visitscore": "35.74",
							"landmarkscore": "10",
							"popularity": false,
							"pop_tv": false,
							"pop_sns": false,
							"pop_hot": false,
							"pop_hit": false,
							pop_top": "京畿_、盆唐区_2",
							"updateTS": "2019-12-12 00:00:00",
							"hasoildata": false,
							"hasdetailinfo": true,
							"hassubpoi": true,
							"subpoi": {
									"count": 1
							}
					}
        ],
        "hasgasstation": false
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                               | タイプ    | 説明                                     |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                                  |
| header.isSuccessful                | Boolean | 成否                                  |
| header.resultCode                  | Integer | 失敗コード                                  |
| header.resultMessage               | String  | 失敗メッセージ                                 |
| cate                                | Object  | 本文領域                                  |
| cate.result                         | Boolean | 成否                                  |
| cate.totalcount                     | Integer | 全体検索結果対象数                          |
| cate.count                          | Integer | 検索結果数                                |
| cate.poi                        | Array   | POI検索結果リスト                           |
| cate.poi[0].poiid               | Integer | POI ID                                   |
| cate.poi[0].depth             | String  | POI下位施設depth                                 |
| cate.poi[0].dpx                 | String  | display x座標(WGS84の場合longitude)         |
| cate.poi[0].dpy                 | String  | display y座標(WGS84の場合latitude)          |
| cate.poi[0].rpx                 | String  | 探索x座標(WGS84の場合longitude)              |
| cate.poi[0].rpy                 | String  | 探索y座標(WGS84の場合latitude)               |
| cate.poi[0].name1               | String  | 正式名称                                  |
| cate.poi[0].name2               | String  | 縮約名称                                  |
| cate.poi[0].name3               | String  | 拡張名称1                                  |
| cate.poi[0].name4               | String  | 拡張名称2                                  |
| cate.poi[0].admcode             | String  | 行政コード                                  |
| cate.poi[0].jibun               | String  | 地番                                      |
| cate.poi[0].address             | String  | 住所                                     |
| cate.poi[0].roadname            | String  | 新住所の道路名                                 |
| cate.poi[0].roadjibun           | String  | 新住所の地番                                  |
| cate.poi[0].detailaddress       | String  | 詳細住所                                  |
| cate.poi[0].catecode            | String  | 分類コード                                  |
| cate.poi[0].catename            | String  | 分類名称                                  |
| cate.poi[0].tel                | String  | 電話番号1                                   |
| cate.poi[0].distance                | Integer  | 距離                                 |
| cate.poi[0].imagecount          | Integer | POIイメージ数                              |
| cate.poi[0].hasoildata          | Boolean | ガソリン価格データ存在有無                            |
| cate.poi[0].oildata             | Object  | ガソリン価格データ情報                              |
| cate.poi[0].oilda.tag_price     | Integer | レギュラー価格                                 |
| cate.poi[0].oilda.hg_price      | Integer | ハイオク価格                               |
| cate.poi[0].oilda.d_price       | Integer | 軽油価格                                  |
| cate.poi[0].oilda.l_price       | Integer | LPG価格                                 |
| cate.poi[0].oilda.updatetime    | String  | アップデート時間                                |
| cate.poi[0].oilda.priceinfo     | String  | 最高、最低ガソリン価格情報<br>(H：最高、L：最低、X：該当なし)<br>レギュラー、ハイオク、軽油、LPG順 |
| cate.poi[0].oilda.wash          | Boolean | 洗車施設有無                                |
| cate.poi[0].oilda.fix           | Boolean | 整備可否                                |
| cate.poi[0].oilda.mart          | Boolean | 売店有無                                   |
| cate.poi[0].hassubpoi          | Boolean | 下位施設データ存在有無         |
| cate.poi[0].subpoi          | Object | 下位施設情報                               |
| cate.poi[0].subpoi.count          | Integer | 下位施設数                                |
| cate.poi[0].subpoi.poi          | Array |  POI情報と同じ                           |

### 7\. 空間検索

* 入力された行政コードおよび行政名称をポリゴン座標で返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/adminToPolygon  |

[Path parameter]

| 名前   | タイプ   | 必須かどうか | 有効範囲 | 説明   |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須  |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前      | タイプ   | 必須かどうか | 説明                                 |
| --------- | ------ | ----- |  ------------------------------------ |
| coordtype         | Integer | 必須 | 座標タイプ<br>Default：1 <br> 0：TW <br> 1：WGS84 |
| mode         | Integer | 必須 | 照会区域範囲 <br> 0: ALL <br>          |
| query         | String | 必須 | 行政コードおよび行政名称 |


#### レスポンス

##### レスポンス本文

```
{
    "polygon": {
        "result": true,
        "count": 1,
        "polygondata": [
            {
                "admincode": "4136025921",
                "count": 1,
                "polygonlist": [
                    {
                        "count": 413,
                        "polygon": [
                            {
                                "x": 127.207296,
                                "y": 37.665605
                            },
                            {
                                "x": 127.208346,
                                "y": 37.665080
                            },
                            ...
                        ]
                    }
                ]
            }
        ]
    },
    "header": {
     "isSuccessful": true,
     "resultCode": 0,
     "resultMessage": ""
    }
}
```

##### フィールド

| 名前                               | タイプ    | 説明                                     |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                                  |
| header.isSuccessful                | Boolean | 成否                                  |
| header.resultCode                  | Integer | 失敗コード                                  |
| header.resultMessage               | String  | 失敗メッセージ                                 |
| polygon                         | Object | 本文領域                                   |
| polygon.result                         | Boolean | 成否                                   |
| polygon.count                          | Integer | 検索結果数                                |
| polygon.polygondata                        | Array   | ポリゴンデータ                            |
| polygon.polygondata[0].admincode               | String | 検索したAdminCode値(modeによって桁数が変わる)                                   |
| polygon.polygondata[0].count             | Integer  | ポリゴン数                          |
| polygon.polygondata[0].polygonlist     | Array  | ポリゴン        |
| polygon.polygondata[0].polygonlist[0].count     | Integer  | ポイント数     |
| polygon.polygondata[0].polygonlist[0].polygon     | Array  | ポリゴン座標リスト     |
| polygon.polygondata[0].polygonlist[0].polygon[0].x     | Integer  | x座標     |
| polygon.polygondata[0].polygonlist[0].polygon[0].y   | Integer  | y座標     |


### 8\. ポリゴン内の行政/法定洞検索

* 入力されたポリゴン座標を行政コードで返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/polygonToAdmin  |

[Path parameter]

| 名前   | タイプ   | 必須かどうか | 有効範囲 | 説明   |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須  |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前      | タイプ   | 必須かどうか | 説明                                 |
| --------- | ------ | ----- |  ------------------------------------ |
| coordtype         | Integer | 必須 | 座標タイプ<br>Default：1 <br> 0：TW <br> 1：WGS84 |
| polygon     | Array  |必須 | ポリゴン座標リスト    |
| polygon[0].x   | Integer  | 必須| x座標    |
| polygon[0].y   | Integer  | 必須 | y座標    |



#### レスポンス

##### レスポンス本文

```
{
    "header": {
            "isSuccessful": true,
            "resultCode": 0,
            "resultMessage": ""
    },
    "adm": {
        "result": true,
        "admincodes": {
            "count": 3,
            "admincodelist": [
                {
                    "AdminCode": "4136025921",
                    "Address": "京畿道南楊州市眞乾邑サヌンリ"
                },
                {
                    "AdminCode": "4136025926",
                    "Address": "京畿道南楊州市 眞乾邑ソンヌンリ"
                },
                {
                    "AdminCode": "4136025900",
                    "Address": "京畿道南楊州市 眞乾邑"
                }
            ]
        }
    }
}
```

##### フィールド

| 名前                                | タイプ     | 説明                                      |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                                   |
| header.isSuccessful                | Boolean | 成否                                   |
| header.resultCode                  | Integer | 失敗コード                                   |
| header.resultMessage               | String  | 失敗メッセージ                                  |
| adm                         | Object | 本文領域                                   |
| adm.result                         | Boolean | 成否                                   |
| adm.count                          | Integer | 検索結果数                                 |
| adm.polygondata                        | Array   | ポリゴンデータ                            |
| adm.polygondata[0].admincode               | String | 検索したAdminCode値(modeによって桁数が変化する)                                   |
| adm.polygondata[0].count             | Integer  | ポリゴン数                           |
| adm.polygondata[0].polygonlist     | Array  | ポリゴン        |
| adm.polygondata[0].polygonlist[0].count     | Integer  | ポイント数      |
| adm.polygondata[0].polygonlist[0].polygon     | Array  | ポリゴン座標リスト     |
| adm.polygondata[0].polygonlist[0].polygon[0].x     | Integer  | x座標     |
| adm.polygondata[0].polygonlist[0].polygon[0].y   | Integer  | y座標     |

### 9\. 建物群入口点照会

* 入力されたポリゴン座標に該当する入口点の数と座標を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/searchEntryPoint  |

[Path parameter]

| 名前    | タイプ    | 必須かどうか | 有効範囲 | 説明    |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須   |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前       | タイプ    | 必須かどうか | 説明                                  |
| --------- | ------ | ----- |  ------------------------------------ |
| coordtype         | Integer | 選択  | 座標タイプ<br>Default: 1 <br> 0: TW <br> 1: WGS84 |
| type     | Integer  |選択 | 今後機能追加予定<br>現在は動作に影響なし      |
| posX   | String  | 必須| x座標     |
| posY   | String  | 必須 | y座標     |



#### レスポンス

##### レスポンス本文

```
{
    "data": {
        "result": true,
        "count": 5,
        "entrypoints": [
            {
                "x": 126.936249,
                "y": 37.54713,
                "type": 0
            },
            {
                "x": 126.935912,
                "y": 37.547139,
                "type": 0
            },
            {
    "x": 126.936687,
                "y": 37.547097,
                "type": 0
            },
            {
                "x": 126.936674,
                "y": 37.546655,
                "type": 0
            },
            {
                "x": 126.936099,
                "y": 37.546389,
                "type": 0
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""                        
    }
}
```

##### フィールド

| 名前                               | タイプ    | 説明                                     |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                                  |
| header.isSuccessful                | Boolean | 成否                                  |
| header.resultCode                  | Integer | 失敗コード                                  |
| header.resultMessage               | String  | 失敗メッセージ                                 |
| data                         | Object | 本文領域                                   |
| data.result                         | Boolean | 成否                                   |
| data.count                          | Integer | 照会された建物群の入口点の数                                 |
| data.entrypoints                        | Object   | 照会された建物群の入口点座標リスト                            |
| data.entrypoints[0].x               | Double | x座標                                  |
| data.entrypoints[0].y             | Double  | y座標                          |
| data.entrypoints[0].type     | Integer  | 今後機能追加予定        |

### 10\. 住所検証

* 入力された住所を検証します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/addr-searches  |

[Path parameter]

| 名前   | タイプ   | 必須かどうか | 有効範囲 | 説明   |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須  |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前      | タイプ   | 必須かどうか | 説明                                 |
| --------- | ------ | ----- |  ------------------------------------ |
| addr     | String  | 必須 | 検索する住所    |
| coordtype         | String | 選択 | 座標タイプ<br>Default: 1 <br> 0: TW <br> 1: WGS84 |
| startposition   | String  | 任意 | 検索開始位置<br>0:最初の位置、未入力時は0で照会    |
| reqcount   | String  | 任意 | 検索リクエスト数<br>0に設定時は最大数を返す     |
| posx     | String  | 任意 | X座標     |
| posy     | String  | 任意 | Y座標     |


#### レスポンス

##### レスポンス本文

```
{
    "search": {
        "data": [
            {
                "posx": "127.110662",
                "posy": "37.402125",
                "address": "京畿道城南市盆唐区板橋駅路240",
                "admcode": "4113510900"
            }
        ],
        "count": 1
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                               | タイプ    | 説明                                     |
| ---------------------------------- | ------- | ---------------------------------------- |
| header                             | Object  | ヘッダ領域                                  |
| header.isSuccessful                | Boolean | 成否                                  |
| header.resultCode                  | Integer | 失敗コード                                  |
| header.resultMessage               | String  | 失敗メッセージ                                 |
| search                         | Object | 本文領域                                  |
| search.data                         | Array | 検索結果                                  |
| search.data[0].posx                          | String | x座標                               |
| search.data[0].posy                        | String | y座標                           |
| search.data[0].address               | String | 住所                                 |
| search.data[0].admcode             | String  | 行政コード                          |
| search.data[0].distance             | Double  | 入力された座標との距離(単位：m)<br>(posx、posy入力時に出力)                            |
| search.count             | Integer  | 検索結果数                          |

## Reverse Geocoding API

### 1\. 座標検索\(座標→住所\)

* 座標(TW座標/WGS84座標)で住所を検索します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/addresses?posX={posX}&posY={posY}&coordtype={coordtype} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Query Parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明                              |
| --------- | ------ | ----- | ----- | ---------------------------------------- |
| posX      | String | 必須 |       | x座標                            |
| posY      | String | 必須 |       | y座標                            |
| coordtype | String | 任意 |       | リクエスト座標形式<br>0：TW座標<br>1：WGS84座標<br>未入力時、TW座標基準検索 |

#### レスポンス

##### レスポンス本文

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    },
    "location": {
        "result": true,
        "hasAdmAddress": true,
        "adm": {
            "posx": "127.110425",
            "posy": "37.402109",
            "address": "京畿道城南市盆唐区サムピョン洞",
            "distance": 0,
            "bldname": "Samhwan HIPEXA洞",
            "admcode": "4113510900",
            "postcode": "13493",
            "jibun": "678",
            "roadname": "京畿道城南市盆唐区パンギョ駅路",
            "roadjibun": "240"
        },
        "adm_address": {
            "address": "京畿道城南市盆唐区サムピョン洞",
            "admcode": "4113565500",
            "address_category3": "サムピョン洞",
            "address_category4": "",
            "jibun": "678",
            "address_category1": "京畿道",
            "address_category2": "城南市盆唐区",
            "cut_address": "京畿城南市盆唐区サムピョン洞"
        },
        "legal_address": {
            "address": "京畿道城南市盆唐区サムピョン洞",
            "admcode": "4113510900",
            "address_category3": "サムピョン洞",
            "address_category4": "",
            "jibun": "678",
            "address_category1": "京畿道",
            "address_category2": "城南市盆唐区",
            "cut_address": "京畿城南市盆唐区サムピョン洞"
        }
    }
}
```

##### フィールド
| 名前                    | タイプ     | 説明                                      |
| ---------------------- | ------- | ---------------------------------------- |
| header                 | Object  | ヘッダ領域                                   |
| header.isSuccessful    | Boolean | 成否                                   |
| header.resultCode      | Integer | 失敗コード                                   |
| header.resultMessage   | String  | 失敗メッセージ                                  |
| location               | Object  | 本文領域                                   |
| location.result        | Boolean | 成否                                   |
| location.adm.posx      | String  | x座標                                    |
| location.adm.posy      | String  | y座標                                    |
| location.adm.distance   | String  | 距離(m)                                    |
| location.adm.bldname   | String  | 建物名                                   |
| location.adm.admcode   | String  | 行政コード                                   |
| location.adm.postcode   | String  | 郵便番号                                   |
| location.adm.jibun     | String  | 地番                                       |
| location.adm.roadname  | String  | 新住所の道路名                                 |
| location.adm.roadjibun | String  | 新住所の地番                                  |
| location.adm_address           | Object  | 行政洞住所情報                         |
| location.adm_address.admcode   | String  | 行政コード                                   |
| location.adm_address.postcode   | String  | 郵便番号                                   |
| location.adm_address.address   | String  | 住所                                      |
| location.adm_address.jibun     | String  | 地番                                      |
| location.adm_address.address_category1     | String  |  道/市                     |
| location.adm_address.address_category2     | String  |  市/郡/区                  |
| location.adm_address.address_category3     | String  |  邑/面/洞                |
| location.adm_address.address_category4     | String  |  里                 |
| location.adm_address.cut_address     | String  |                         |
| location.legal_address           | Object  | 法定洞住所情報                          |
| location.legal_address.admcode   | String  | 法定コード                                   |
| location.legal_address.address   | String  | 住所                                      |
| location.legal_address.jibun     | String  | 地番                                      |
| location.legal_address.address_category1     | String  | 道/市                      |
| location.legal_address.address_category2     | String  | 市/郡/区                     |
| location.legal_address.address_category3     | String  | 邑/面/洞                     |
| location.legal_address.address_category4     | String  | 里                      |
| location.legal_address.cut_address     | String  |                         |



## 探索

### 1\. 経路探索

* 出発地と目的地(経由地オプション)座標を利用して探索した詳細情報と経路情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-normal?option={option}&coordType={coordType}&carType={carType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&saveFile={saveFile}&useTaxifare={useTaxifare}&searchByAddress={searchByAddress}&usageType={usageType}&carHeight={carHeight}&carWeight={carWeight}&useStartDirection={useStartDirection} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前   | タイプ | 要否 | 有効範囲 | 説明                                   |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須 |       | 出発地x座標                             |
| startY   | String | 必須 |       | 出発地y座標                             |
| endX     | String | 必須 |       | 到着地x座標                             |
| endY     | String | 必須 |       | 到着地y座標                             |
| via1X    | String | 任意 |       | 経由地1 x座標                           |
| via1Y    | String | 任意 |       | 経由地1 y座標                           |
| via2X    | String | 任意 |       | 経由地2 x座標                           |
| via2Y    | String | 任意 |       | 経由地2 y座標                           |
| via3X    | String | 任意 |       | 経由地3 x座標                           |
| via3Y    | String | 任意 |       | 経由地3 y座標                           |
| via4X    | String | 任意 |       | 経由地4 x座標                           |
| via4Y    | String | 任意 |       | 経由地4 y座標                           |
| via5X    | String | 任意 |       | 経由地5 x座標                           |
| via5Y    | String | 任意 |       | 経由地5 y座標                           |
| option   | String | 必須 |       | 経路検索オプション<br>探索オプション1つのみ可能<br>例) option=real_traffic<br>real_traffic：リアルタイム推薦1<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic2：リアルタイム推薦2<br>short\_distance\_priority：短距離<br>motorcycle：二輪車<br>recommendation：推薦 |
| carType   | Integer | 任意 |       | 料金所費用計算のための車種(1～6)、default：1 |
| coordType   | String | 必須 |       | input、output座標タイプ、1つのみ入力可能(TW、WGS84) |
| guideTop	|Integer| 任意 ||表示する案内情報数 |
| groupByTrafficColor	| Boolean| 任意| |詳細経路リスト(paths)情報を交通色別にグルーピングして返すかどうか	|
| saveFile	| Boolean| 任意| |経路周辺POI検索のためのbinaryファイルを保存するかどうか	|
| useTaxifare   | Integer | 選択 |       | 予想タクシー料金照会有無<br>例) useTaxifare=1<br>0：未使用<br> 1：一般タクシー<br>2：模範タクシー |
| searchByAddress   | Boolean | 選択  |       | 住所ベースの経路探索を行うか<br>Default：false |
| usageType   | Integer | 選択  |       | 車両の用途<br>Default：0<br>一般：0<br>タクシー：1<br>(パス探索オプションがrecommendationの場合にのみ適用) |
| carHeight   | Integer | 選択 |       | 車両の高さ情報<br>Default: 0 |
| carWeight   | Integer | 選択 |       | 車両の重量情報<br>Default: 0 |
| useStartDirection   | Boolean | 任意   |       | 出発地座標基準探索方向指定機能を使用するか<br>Default: false |



#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": {
            "file_name": "",
            "toll_fee": 0.0,
            "taxiFare": 3500,
            "paths": [
                {
                    "coords": [
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        ...
                    ],
                    "speed": -1.0,
                    "distance": 258.0,
                    "spend_time": 96.0,
                    "road_code": 5.0,
                    "traffic_color": "#d73a76"
                },
                ...
            ],
            "guides": [
                {
                    "name": "Subuchon-gil",
                    "distance": 440.0,
                    "speed": -1.0,
                    "road_code": 5.0,
                    "score": 880.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        {
                            "x": 127.5313243125899,
                            "y": 37.40142475251763
                        },
                        ...
                    ],
                    "traffic_color": ""
                },
              ...
            ],
            "option": "real_traffic",
            "spend_time": 240.0,
            "distance": 858.0
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                      | タイプ  | 説明                                   |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                |
| header.isSuccessful         | Boolean | 成否                                |
| header.resultCode           | Integer | 失敗コード                                |
| header.resultMessage        | String  | 失敗メッセージ                               |
| route			                  | Object  | 本文領域                                |
| route.data                   | Object  | 経路情報                                |
| route.data.file_name          | String | 経路周辺のPOI検索のためのbinaryファイル名            |
| route.data.option              | String | 探索オプション                    |
| route.data.spend_time           | Integer | 所要時間(秒)                              |
| route.data.distance           | Integer | 距離(m)                          |
| route.data.toll_fee    | Integer | 料金所の料金                         |
| route.data.taxiFare    | Integer | 予想タクシー料金                            |
| route.data.paths	 | Array | 詳細経路リスト                         |
| route.data.paths[0].coords | Array | 詳細座標リスト                        |
| route.data.paths[0].coords[0].x   | Double | x座標                         |
| route.data.paths[0].coords[0].y         | Double | y座標                     |
| route.data.paths[0].speed          | Integer | 速度                               |
| route.data.paths[0].spend_time          | Integer | 所要時間(秒)                                   |
| route.data.paths[0].distance             | Integer | 距離(m)                        |
| route.data.paths[0].road_code             | Integer | 道路種別コード                    |
| route.data.paths[0].traffic_color       | String | 道路交通色                     |
| route.data.guides       | Array | 主要道路情報リスト                    |
| route.data.guides[0].coords       | Array | 詳細座標リスト                    |
| route.data.guides[0].coords[0].x       | Array | x座標                    |
| route.data.guides[0].coords[0].y       | Array | y座標                    |
| route.data.guides[0].distance       | Integer | 距離(m)                        |
| route.data.guides[0].name       | String | 道路名                     |
| route.data.guides[0].road_code       | Integer | 道路種別コード                    |
| route.data.guides[0].score       | Integer | 比重                     |
| route.data.guides[0].speed       | Integer | 速度(km)                       |
| route.data.guides[0].type       | String | 道路タイプ                    |
| route.data.guides[0].traffic_color       | String | 道路交通色                     |



### 2\. 経路検索の要約

* 出発地と目的地(経由地オプション)座標を利用して、探索された要約情報(距離、時間、探索オプション)情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-summary?option={option}&coordType={coordType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&carHeight={carHeight}&carWeight={carWeight}&useStartDirection={useStartDirection} |

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前   | タイプ | 要否 | 有効範囲 | 説明                                   |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須 |       | 出発地x座標                             |
| startY   | String | 必須 |       | 出発地y座標                             |
| endX     | String | 必須 |       | 到着地x座標                             |
| endY     | String | 必須 |       | 到着地y座標                             |
| via1X    | String | 任意 |       | 経由地1 x座標                           |
| via1Y    | String | 任意 |       | 経由地1 y座標                           |
| via2X    | String | 任意 |       | 経由地2 x座標                           |
| via2Y    | String | 任意 |       | 経由地2 y座標                           |
| via3X    | String | 任意 |       | 経由地3 x座標                           |
| via3Y    | String | 任意 |       | 経由地3 y座標                           |
| via4X    | String | 任意 |       | 経由地4 x座標                           |
| via4Y    | String | 任意 |       | 経由地4 y座標                           |
| via5X    | String | 任意 |       | 経由地5 x座標                           |
| via5Y    | String | 任意 |       | 経由地5 y座標                           |
| option   | String | 必須 |       | 経路検索オプション<br>検索オプションをカンマ（,）区切りでリクエスト<br>例) option=real_traffic,real_traffic2<br>real_traffic：リアルタイム推薦1<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic2：リアルタイム推薦2<br>short\_distance\_priority：短距離<br>motorcycle:二輪車 |
| coordType   | String | 必須 |       | input、output座標タイプ、1つのみ入力可能(TW、WGS84) |
| carHeight   | Integer | 選択 |       | 車両の高さ情報<br>Default: 0 |
| carWeight   | Integer | 選択 |       | 車両の重量情報<br>Default: 0 |
| useStartDirection   | Boolean | 任意   |       | 出発地座標基準探索方向指定機能を使用するか<br>Default: false |


#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": [
            {
                "option": "real_traffic",
                "spend_time": 240.0,
                "distance": 858.0
            },
            ...
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                      | タイプ  | 説明                                   |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                |
| header.isSuccessful         | Boolean | 成否                                |
| header.resultCode           | Integer | 失敗コード                                |
| header.resultMessage        | String  | 失敗メッセージ                               |
| route			                  | Object  | 本文領域                                |
| route.data                   | Array  | 経路情報                                |
| route.data[0].option              | String | 探索オプション                    |
| route.data[0].spend_time           | Integer | 所要時間(秒)                              |
| route.data[0].distance           | Integer | 距離(m)                          |


### 3\. 複数出発地経路検索の要約

* 1つ以上の複数出発地座標と1つの目的地座標を探索して、それぞれの時間と距離情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-start-multi-summary|

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前   | タイプ | 要否 | 有効範囲 | 説明                                   |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | 出発地情報Array (最大50個)                         |
| data[0].startX   | String | 必須 |       | 出発地x座標                             |
| data[0].startY   | String | 必須 |       | 出発地y座標                             |
| data[0].startIdx   | String | 必須 |       | 出発地識別ID                                 |
| endX     | String | 必須 |       | 到着地x座標                             |
| endY     | String | 必須 |       | 到着地y座標                             |
| orderby    | String | 必須 |       | ソート基準(<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)                               |
| coordType    | String | 必須 |       | 座標タイプ(TW、WGS84)
| resultCount    | Integer | 任意 |       | 結果表示数                            |


#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": [
            {
                "spend_time": 240.0,
                "distance": 858.0,
                "startX": "127.538593",
                "startY": "37.398322",
                "startIdx": "test"
            },
            {
                "spend_time": 960.0,
                "distance": 8289.0,
                "startX": "127.50940913221785",
                "startY": "37.44046992358892",
                "startIdx": "test2"
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                      | タイプ  | 説明                                   |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                |
| header.isSuccessful         | Boolean | 成否                                |
| header.resultCode           | Integer | 失敗コード                                |
| header.resultMessage        | String  | 失敗メッセージ                               |
| route			                  | Object  | 本文領域                                |
| route.data                   | Array  | 経路情報                                |
| route.data[0].spend_time           | Integer | 所要時間(秒)                              |
| route.data[0].distance           | Integer | 距離(m)                          |
| route.data[0].startX           | String | 出発地x座標                      |
| route.data[0].startY           | String | 出発地y座標                      |
| route.data[0].startIdx           | String | 出発地識別ID                          |



### 4\. 複数目的地経路検索の要約

* 1つの出発地座標と1つ以上の複数目的地座標を探索して、それぞれの時間と距離情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-end-multi-summary|

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前   | タイプ | 要否 | 有効範囲 | 説明                                   |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| data    | Array |     |       | 出発地情報Array (最大50個)                       |
| data[0].endX   | String | 必須 |       | 到着地x座標                             |
| data[0].endY   | String | 必須 |       | 到着地y座標                             |
| data[0].endIdx   | String | 必須 |       | 到着地識別ID                                 |
| startX     | String | 必須 |       | 出発地x座標                             |
| startY     | String | 必須 |       | 出発地y座標                             |
| orderby    | String | 必須 |       | ソート基準(<br> 0 : distance_desc<br>1 : distance_asc<br>2 : time_desc <br>3 : time_asc<br>)                               |
| coordType    | String | 必須 |       | 座標タイプ(TW、WGS84)
| resultCount    | Integer | 任意 |       | 結果表示数                            |


#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": [
            {
                "spend_time": 240.0,
                "distance": 858.0,
                "endX": "127.538593",
                "endY": "37.398322",
                "endIdx": "test"
            },
            {
                "spend_time": 1020.0,
                "distance": 8303.0,
                "endX": "127.50940913221785",
                "endY": "37.44046992358892",
                "endIdx": "test2"
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                      | タイプ  | 説明                                   |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                |
| header.isSuccessful         | Boolean | 成否                                |
| header.resultCode           | Integer | 失敗コード                                |
| header.resultMessage        | String  | 失敗メッセージ                               |
| route			                  | Object  | 本文領域                                |
| route.data                   | Array  | 経路情報                                |
| route.data[0].spend_time           | Integer | 所要時間(秒)                              |
| route.data[0].distance           | Integer | 距離(m)                          |
| route.data[0].endX           | String | 到着地x座標                      |
| route.data[0].endY           | String | 到着地y座標                      |
| route.data[0].endIdx           | String | 到着地識別ID                          |



### 5\. 経路予測探索

* 出発、到着予定時間を基準に予測到着時間および出発地と目的地(経由地オプション)座標を利用して探索された詳細情報と経路情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/route-time?startX={startX}&startY={startY}&endX={endX}&endY={endY}&type={type}&year={year}&month={month}&day={day}&hour={hour}&minutes={minutes}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&coordType={coordType}&carType={carType}&useTrafficColor={useTrafficColor}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&beforeCount={beforeCount}&afterCount={afterCount}&interval={interval}&useTaxifare={useTaxifare}&carHeight={carHeight}&carWeight={carWeight}&useStartDirection={useStartDirection}&usageType={usageType}|

[Path parameter]

| 名前 | タイプ | 要否 | 有効範囲 | 説明 |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前   | タイプ | 要否 | 有効範囲 | 説明                                   |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX    | String | 必須 |       | 出発地x座標
| startY    | String | 必須 |       | 出発地y座標
| endX   | String | 必須 |       | 到着地x座標                              |
| endY   | String | 必須 |       | 到着地y座標                              |
| type     | String | 必須 |       | 基準時間(出発、到着)<br> start：出発時間基準<br>end：到着時間基準                              |
| year     | Integer | 必須 |       | 基準年(ex.2019)                                 |
| month     | Integer | 必須 |       | 基準月                               |
| day    | Integer | 必須 |       | 基準日		|
| hour     | Integer | 必須 |       | 基準時間(時)                                 |
| minutes    | Integer | 必須 |       | 基準時間(分) 		|
| via1X   | String | 任意 |       | 経由地1 x座標                            |
| via1Y   | String | 任意 |       | 経由地1 y座標                            |
| via2X   | String | 任意 |       | 経由地2 x座標                            |
| via2Y   | String | 任意 |       | 経由地2 y座標                            |
| via3X   | String | 任意 |       | 経由地3 x座標                            |
| via3Y   | String | 任意 |       | 経由地3 y座標                            |
| via4X   | String | 任意 |       | 経由地4 x座標                            |
| via4Y   | String | 任意 |       | 経由地4 y座標                            |
| via5X   | String | 任意 |       | 経由地5 x座標                            |
| via5Y   | String | 任意 |       | 経由地5 y座標                            |
| coordType    | String | 任意 |       | 座標タイプ(tw, wgs84)<br> default : wgs84
| useTrafficColor   | Boolean | 任意 |       | 道路交通色返却有無(true、false)<br> defaut : false |
| guideTop   | Integer | 任意 |       | 表示する案内情報数 |
| carType   | Integer | 任意 |       | 料金所費用計算のための車種(1～6), default : 1 |
| groupByTrafficColor	| Boolean| 任意| | 詳細経路リスト(paths)情報を交通色別にグルーピングして返すかどうか	|
| beforeCount   | Integer | 任意 |       | 基準時間以前の時間の探索数 |
| afterCount   | Integer | 任意 |       | 基準時間以降の時間の探索数 |
| interval   | Integer | 任意 |       | 基準時間以前/以降の時間Interval(分) |
| useTaxifare   | Integer | 選択 |       | 予想タクシー料金照会を行うか<br>例) useTaxifare=1<br>0：未使用<br> 1：一般タクシー<br>2：模範タクシー<br>3：一般タクシーと模範タクシー |
| carHeight   | Integer | 選択 |       | 車両の高さ情報<br>Default: 0 |
| carWeight   | Integer | 選択 |       | 車両の重量情報<br>Default: 0 |
| useStartDirection   | Boolean | 任意   |       | 出発地座標基準探索方向指定機能を使用するか<br>Default: false |
| usageType   | Integer | 任意  |       | 車両用途<br>Default: 0<br>一般: 0<br>タクシー: 1 |

#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": {
            "distance": 22621.0,
            "spend_time": 1620.0,
            "toll_fee": 0.0,
						"taxiFare" : 3900,
            "times": [
                {
                    "index": -2.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 27.0
                    }
                },
                {
                    "index": -1.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 30.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 16.0,
                        "minutes": 57.0
                    }
                },
                {
                    "index": 0.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 27.0
                    }
                },
                {
                    "index": 1.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 30.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 17.0,
                        "minutes": 57.0
                    }
                },
                {
                    "index": 2.0,
                    "spend_time": 1620.0,
                    "distance": 0.0,
                    "start_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 18.0,
                        "minutes": 0.0
                    },
                    "end_time": {
                        "year": 2019.0,
                        "month": 11.0,
                        "day": 22.0,
                        "hour": 18.0,
                        "minutes": 27.0
                    }
                }
            ],
            "paths": [
                {
                    "coords": [
                        {
                            "x": 126.94730280056565,
                            "y": 37.38419119654106
                        },
                        {
                            "x": 126.94700283437736,
                            "y": 37.38395788491522
                        }
                    ],
                    "speed": -1.0,
                    "distance": 36.0,
                    "spend_time": 10.0,
                    "road_code": 5.0,
                    "traffic_color": "#989898"
                },
                {
                    "coords": [
                        {
                            "x": 126.94700283437736,
                            "y": 37.38395788491522
                        },
                        {
                            "x": 126.94650289104105,
                            "y": 37.383557922382955
                        }
                    ],
                    "speed": -1.0,
                    "distance": 63.0,
                    "spend_time": 20.0,
                    "road_code": 5.0,
                    "traffic_color": "#989898"
                },
                ...
            ],
            "guides": [
                {
                    "name": "京水大路",
                    "distance": 2401.0,
                    "speed": 53.0,
                    "road_code": 3.0,
                    "score": 14406.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 126.95508976578816,
                            "y": 37.37800871915593
                        },
                        {
                            "x": 126.95518976229994,
                            "y": 37.37780874413099
                        },
                        ...
                    ],
                    "traffic_color": "#00ff60"
                },
                {
                    "name": "峰潭果川路",
                    "distance": 13369.0,
                    "speed": 83.0,
                    "road_code": 2.0,
                    "score": 106952.0,
                    "type": "ROAD",
                    "coords": [
                        {
                            "x": 126.97727624066877,
                            "y": 37.34261321883654
                        },
                        {
                            "x": 126.97736373901714,
                            "y": 37.342388246474925
                        },
                        ...
                    ],
                    "traffic_color": "#00ff60"
                }
            ]
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                       | タイプ   | 説明                                    |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                |
| header.isSuccessful         | Boolean | 成否                                |
| header.resultCode           | Integer | 失敗コード                                |
| header.resultMessage        | String  | 失敗メッセージ                               |
| route			                  | Object  | 本文領域                                 |
| route.data                   | Object  | 経路情報                                 |
| route.data.file_name          | String | 経路周辺のPOI検索のためのbinaryファイル名             |
| route.data.option              | String | 探索オプション                     |
| route.data.spend_time           | Integer | 所要時間(秒)                              |
| route.data.distance           | Integer | 距離(m)                          |
| route.data.toll_fee    | Integer | 料金所の料金                          |
| route.data.taxiFare    | Integer | 予想タクシー料金                            |
| route.data.times	 | Array | 詳細経路リスト                          |
| route.data.times[0].index	 | Integer | 基準時間対比Index(0の場合は基準時間)       |
| route.data.times[0].spend_time	 | Integer | 所要時間(秒)       |
| route.data.times[0].start_time	 | Object | 出発時間    |
| route.data.times[0].start_time.year	 | Object | 年     |
| route.data.times[0].start_time.month	 | Object | 月     |
| route.data.times[0].start_time.day	 | Object | 日     |
| route.data.times[0].start_time.hour	 | Object | 時     |
| route.data.times[0].start_time.minutes	 | Object | 分     |
| route.data.times[0].end_time	 | Object | 到着時間    |
| route.data.times[0].end_time.year	 | Object | 年     |
| route.data.times[0].end_time.month	 | Object | 月     |
| route.data.times[0].end_time.day	 | Object | 日     |
| route.data.times[0].end_time.hour	 | Object | 時     |
| route.data.times[0].end_time.minutes	 | Object | 分     |
| route.data.paths	 | Array | 詳細経路リスト                          |
| route.data.paths[0].coords | Array | 詳細座標リスト                         |
| route.data.paths[0].coords[0].x   | Double | x座標                          |
| route.data.paths[0].coords[0].y         | Double | y座標                      |
| route.data.paths[0].speed          | Integer | 速度                                |
| route.data.paths[0].spend_time          | Integer | 所要時間(秒)                                   |
| route.data.paths[0].distance             | Integer | 距離(m)                        |
| route.data.paths[0].road_code             | Integer | 道路種別コード                     |
| route.data.paths[0].traffic_color       | String | 道路交通色                      |
| route.data.guides       | Array | 主要道路の情報リスト                     |
| route.data.guides[0].coords       | Array | 詳細座標リスト                     |
| route.data.guides[0].coords[0].x       | Array | x座標                     |
| route.data.guides[0].coords[0].y       | Array | y座標                     |
| route.data.guides[0].distance       | Integer | 距離(m)                        |
| route.data.guides[0].name       | String | 道路名                      |
| route.data.guides[0].road_code       | Integer | 道路種別コード                     |
| route.data.guides[0].score       | Integer | 比重                      |
| route.data.guides[0].speed       | Integer | 速度(km)                       |
| route.data.guides[0].type       | String | 道路タイプ                     |
| route.data.guides[0].traffic_color       | String | 道路交通色                      |


### 6\. 複数の経由地を追加100

* 出発地点から目的地までの経路を探索して探索した経路情報を返します。
* 経由地は最大100個まで追加できます。
* 経由地を6個以上指定する必要がある場合は使用することを推奨します。


#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| POST  | /maps/v3.0/appkeys/{appkey}/route-normal-via|

[Path parameter]

| 名前    | タイプ    | 要否 | 有効範囲 | 説明    |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須   |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前      | タイプ    | 要否 | 有効範囲 | 説明                                      |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須   |       | 出発地x座標                                |
| startY   | String | 必須   |       | 出発地y座標                                |
| endX     | String | 必須   |       | 到着地x座標                                |
| endY     | String | 必須   |       | 到着地y座標                                |
| option   | String | 必須  |       | 経路探索オプション<br>探索オプション','単位でリクエスト<br>例) option=real_traffic,real_traffic2<br>real_traffic：リアルタイム推薦1<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic2：リアルタイム推薦2<br>short\_distance\_priority：短距離<br>motorcycle：二輪車<br>recommendation：推薦 |
| coordType    | String | 必須   |       | 座標タイプ(TW, WGS84)
| viaList    | Array | 任意   |       | 経由地情報                              |
| via[0].viaX    | String | 任意   |       | 経由地x座標                              |
| via[0].viaY    | String| 任意   |       | 経由地y座標                              |
| useAngle    | String | 任意   |       | 出発地地点の走行方向オプション<br> (デフォルト値：false。 true：走行 方向優先、false：走行方向優先しない)                              |
| angle    | Integer | 任意   |       | 結果表示数                               |
| carType   | Integer | 任意   |       | 料金所費用計算のための車種(1～6)、デフォルト値：1 |
| guideTop	|Integer| 任意 ||表示する案内情報数 |
|groupByTrafficColor	| Boolean| 任意| |詳細経路リスト(paths)情報を道路交通色別にまとめて返すかどうか	|
| useTaxifare   | Integer | 任意  |       | 予想タクシー料金照会<br>例) useTaxifare=1<br>0：未使用<br> 1：一般タクシー<br>2：模範タクシー<br>3：一般タクシーと模範タクシー |
| useStartDirection    | Boolean | 任意   |       | 結果表示数                               |
| searchByAddress   | Boolean | 選択  |       | 住所ベースの経路探索を行うか<br>Default：false |
| usageType   | Integer | 選択  |       | 車両の用途<br>Default：0<br>一般：0<br>タクシー：1<br>(パス探索オプションがrecommendationの場合にのみ適用) |
| carHeight   | Integer | 選択 |       | 車両の高さ情報<br>Default: 0 |
| carWeight   | Integer | 選択 |       | 車両の重量情報<br>Default: 0 |

#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": {
            "file_name": "",
            "toll_fee": 500,
            "taxiFare": 44100,
            "paths": [
                {
                    "coords": [
                        {
                            "x": 126.98738167260602,
                            "y": 37.56100472071098
                        },
                        {
                            "x": 126.98745666577292,
                            "y": 37.561004722056495
                        },
                        {
                            "x": 126.98788162917526,
                            "y": 37.560929738395224
                        },
                        {
                            "x": 126.98810661103511,
                            "y": 37.56084641878082
                        },
                        {
                            "x": 126.98823160224156,
                            "y": 37.5607547650072
                        },
                        {
                            "x": 126.9882940996141,
                            "y": 37.56064644538208
                        }
                    ],
                    "speed": 30,
                    "distance": 95,
                    "spend_time": 12,
                    "road_code": 5,
                    "traffic_color": "#00ff60"
                } ...
            ],
            "guides": [
                {
                    "name": "漢南IC",
                    "distance": 0,
                    "speed": 0,
                    "road_code": 0,
                    "score": 0,
                    "type": "IC",
                    "coords": [
                        {
                            "x": 127.01735503801878,
                            "y": 37.522301421437476
                        }
                    ],
                    "traffic_color": ""
                }...
                ],
                "traffic_color": "#fff000"
                }
            ],
            "option": "real_traffic",
            "spend_time": 5580,
            "distance": 45931
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                         | タイプ     | 説明                                      |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                   |
| header.isSuccessful         | Boolean | 成否                                   |
| header.resultCode           | Integer | 失敗コード                                   |
| header.resultMessage        | String  | 失敗メッセージ                                  |
| route			                  | Object  | 本文領域                                   |
| route.data                   | Object  | 経路情報                                   |
| route.data.file_name          | String | 経路周辺POI検索のためのバイナリファイル名           |
| route.data.option              | String | 探索オプション                      |
| route.data.spend_time           | Integer | 所要時間(秒)                             |
| route.data.distance           | Integer | 距離(m)                          |
| route.data.total_fee    | Integer | 料金所の料金                            |
| route.data.taxiFare    | Integer | 予想タクシー料金                            |
| route.data.paths	 | Array | 詳細経路リスト                            |
| route.data.paths[0].coords | Array | 詳細座標リスト                          |
| route.data.paths[0].coords[0].x   | Double | x座標                           |
| route.data.paths[0].coords[0].y         | Double | y座標                       |
| route.data.paths[0].speed          | Integer | 速度                                  |
| route.data.paths[0].spend_time          | Integer | 所要時間(秒)                                  |
| route.data.paths[0].distance             | Integer | 距離(m)                        |
| route.data.paths[0].road_code             | Integer | 道路種別コード                       |
| route.data.paths[0].traffic_color       | String | 道路交通色                        |
| route.data.guides       | Array | 主要道路情報リスト                     |
| route.data.guides[0].coords       | Array | 詳細座標リスト                      |
| route.data.guides[0].coords[0].x       | Array | x座標                      |
| route.data.guides[0].coords[0].y       | Array | y座標                      |
| route.data.guides[0].distance       | Integer | 距離(m)                        |
| route.data.guides[0].name       | String | 道路名                        |
| route.data.guides[0].road_code       | Integer | 道路種別コード                       |
| route.data.guides[0].score       | Integer | 比重                        |
| route.data.guides[0].speed       | Integer | 速度(km)                       |
| route.data.guides[0].type       | String | 道路タイプ                       |
| route.data.guides[0].traffic_color       | String | 道路交通色                        |

### 7\.	経由地間の経路情報要約

* 出発地から目的地までの経路を探索して探索した経路情報を返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET,POST  | /maps/v3.0/appkeys/{appkey}/route-normal-summary?option={option}&coordType={coordType}&carType={carType}&startX={startX}&startY={startY}&endX={endX}&endY={endY}&via1X={via1X}&via1Y={via1Y}&via2X={via2X}&via2Y={via2Y}&via3X={via3X}&via3Y={via3Y}&via4X={via4X}&via4Y={via4Y}&via5X={via5X}&via5Y={via5Y}&guideTop={guideTop}&groupByTrafficColor={groupByTrafficColor}&saveFile={saveFile}&useTaxifare={useTaxifare}&searchByAddress={searchByAddress}&usageType={usageType}&carHeight={carHeight}&carWeight={carWeight}&useStartDirection={useStartDirection} |

[Path parameter]

| 名前   | タイプ   | 必須かどうか | 有効範囲 | 説明   |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須  |       | 固有のアプリケーションキー |

[Request Parameters]

| 名前     | タイプ   | 必須かどうか | 有効範囲 | 説明                                     |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| startX   | String | 必須  |       | 出発地x座標                               |
| startY   | String | 必須  |       | 出発地y座標                               |
| endX     | String | 必須  |       | 到着地x座標                               |
| endY     | String | 必須  |       | 到着地y座標                               |
| via1X    | String | オプション  |       | 経由地1 x座標                             |
| via1Y    | String | オプション  |       | 経由地1 y座標                             |
| via2X    | String | オプション  |       | 経由地2 x座標                             |
| via2Y    | String | オプション  |       | 経由地2 y座標                             |
| via3X    | String | オプション  |       | 経由地3 x座標                             |
| via3Y    | String | オプション  |       | 経由地3 y座標                             |
| via4X    | String | オプション  |       | 経由地4 x座標                             |
| via4Y    | String | オプション  |       | 経由地4 y座標                             |
| via5X    | String | オプション  |       | 経由地5 x座標                             |
| via5Y    | String | オプション  |       | 経由地5 y座標                             |
| option   | String | 必須 |       | 経路探索オプション<br>探索オプションは1つのみ可能<br>例) option=real_traffic<br>real_traffic：リアルタイム推薦1<br>real\_traffic\_freeroad：リアルタイム\(無料\)<br>real_traffic2：リアルタイム推薦2<br>short\_distance\_priority：短距離<br>motorcycle：二輪車<br>recommendation：推薦 |
| carType   | Integer | オプション  |       | 料金所費を計算するための車種(1～6)、デフォルト値：1 |
| coordType   | String | 必須  |       | input、output座標タイプ、1つのみ入力可能(TW、WGS84) |
| useTaxifare   | Integer | オプション |       | 予想タクシー料金照会を行うかどうか<br>例) useTaxifare=1<br>0：未使用<br>1：一般タクシー<br>2：模範タクシー<br>3：一般タクシーと模範タクシー |
| searchByAddress   | Boolean | 選択  |       | 住所ベースの経路探索を行うか<br>Default：false |
| usageType   | Integer | 選択  |       | 車両の用途<br>Default：0<br>一般：0<br>タクシー：1<br>(パス探索オプションがrecommendationの場合にのみ適用) |
| carHeight   | Integer | 選択 |       | 車両の高さ情報<br>Default: 0 |
| carWeight   | Integer | 選択 |       | 車両の重量情報<br>Default: 0 |
| useStartDirection   | Boolean | 任意   |       | 出発地座標基準探索方向指定機能を使用するか<br>Default: false |

#### レスポンス

##### レスポンス本文
```
{
    "route": {
        "data": {
            "option": "real_traffic",
            "spend_time": 6420,
            "distance": 57726,
            "toll_fee": 0,
            "totalTaxiFare": "57420,83100",
            "detailDistance": [
                {
                    "position": "0|1",
                    "distance": 31168
                },
                {
                    "position": "1|2",
                    "distance": 12934
                },
                {
                    "position": "2|3",
                    "distance": 13624
                }
            ]
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                        | タイプ    | 説明                                     |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                  |
| header.isSuccessful         | Boolean | 成否                                  |
| header.resultCode           | Integer | 失敗コード                                  |
| header.resultMessage        | String  | 失敗メッセージ                                 |
| route			                  | Object  | 本文領域                                  |
| route.data                   | Array  | 経路情報                                  |
| route.data[0].option              | String | 探索オプション                     |
| route.data[0].spend_time           | Integer | 所要時間(秒)                             |
| route.data[0].distance           | Integer | 距離(m)                          |
| route.data[0].toll_fee           | Integer | 距離(m)                          |
| route.data[0].totalTaxiFare           | Integer | 距離(m)                          |
| route.data[0].detailDistance           | Array | 経由地要約情報                        |
| route.data[0].detailDistance[0].position           | String | 位置<br>経由地が1個の場合、0\|1：出発地→経由地1, 1\|2：経由地1 →目的地         |
| route.data[0].detailDistance[0].distance           | Integer | 距離(m)            |

## W3W連動API

### 1\. W3W座標検索(座標 → 住所)

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/w3w-addresses?posX={posX}&posY={posY}|

[Path parameter]

| 名前    | タイプ    | 必須かどうか | 有効範囲 | 説明    |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須   |       | 固有のアプリケーションキー |

[Request Query Parameter]

| 名前      | タイプ    | 必須かどうか | 有効範囲 | 説明                                      |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| posX      | String | 必須     |           | x座標                                                      |
| posY      | String | 必須     |           | y座標                                                      |

#### レスポンス

##### レスポンス本文
```
{
    "address": {
        "result": true,
        "adm": {
            "what3words": "下げる.ベルト.調節",
            "posx": "127.110732",
            "posy": "37.402153",
            "address": "京畿道 城南市盆唐区三坪洞678",
            "roadname": "京畿道 城南市盆唐区パンギョ駅路240"
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                         | タイプ     | 説明                                      |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                   |
| header.isSuccessful         | Boolean | 成否                                   |
| header.resultCode           | Integer | 失敗コード                                   |
| header.resultMessage        | String  | 失敗メッセージ                                  |
| address			                  | Object  | 本文領域                                   |
| address.result                   | Boolean  | 成否                                 |
| address.adm                   | Array  | 住所情報                                  |
| address.adm[0].what3words              | String | what3wordsアドレス                      |
| address.adm[0].posx           | String | x座標                            |
| address.adm[0].posy           | String | y座標                         |
| address.adm[0].address           | String | 定洞の住所                         |
| address.adm[0].roadname           | String | 道路名の住所                       |

### 2\. W3Wおすすめワード検索

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/w3w-proposers?query={query}&posX={posX}&posY={posY}|

[Path parameter]

| 名前    | タイプ    | 必須かどうか | 有効範囲 | 説明    |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須   |       | 固有のアプリケーションキー |

[Request Query Parameter]

| 名前      | タイプ    | 必須かどうか | 有効範囲 | 説明                                      |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| query      | String | 必須     |           | what3wordsアドレス<br>(what3wordsフォームに従って2単語入力後、頭文字と単語入力必須<br>例)署名.増減.ㅇ/叫ぶ.孝子.牛)                                                     |
| posX      | String | 選択     |           | x座標                                                      |
| posY      | String | 選択     |           | y座標                                                      |

#### レスポンス

##### レスポンス本文
```
{
    "proposer": {
        "result": true,
        "what3words": [
            {
                "what3words": "署名.増減.今まで",
                "distance": 280,
                "address": "慶尚南道咸安郡"
            },
            {
                "what3words": "署名.同感.部位",
                "distance": 56,
                "address": "京畿道東豆市"
            },
            {
                "what3words": "署名.断言.今まで",
                "distance": 89,
                "address": "忠清北道清州市"
            }
        ]
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                         | タイプ     | 説明                                      |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                   |
| header.isSuccessful         | Boolean | 成否                                   |
| header.resultCode           | Integer | 失敗コード                                   |
| header.resultMessage        | String  | 失敗メッセージ                                  |
| proposer			                  | Object  | 本文領域                                   |
| proposer.result                   | Boolean  | 成否                                 |
| proposer.what3words                   | Array  | w3wおすすめワード 情報                                  |
| proposer.what3words[0].what3words              | String | what3wordsアドレス                      |
| proposer.what3words[0].distance           | double | posX, posY入力時、その座標からの距離<br>(posX, posY入力時に表示)                            |
| proposer.what3words[0].address           | String | 短縮アドレス                        |

### 3\. W3W最適地点検索

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/w3w-optposition-searches?query={query}|

[Path parameter]

| 名前    | タイプ    | 必須かどうか | 有効範囲 | 説明    |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須   |       | 固有のアプリケーションキー |

[Request Query Parameter]

| 名前      | タイプ    | 必須かどうか | 有効範囲 | 説明                                      |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| query | String | 必須    |        | what3wordsアドレス<br>(what3wordsフォームに従って3単語入力必須<br>例)署名.増減.お気に入り) |

#### レスポンス

##### レスポンス本文
```
{
    "search": {
        "result": true,
        "entrypoint": {
            "what3words": "署名.増減.お気に入り",
            "posx": "127.110876",
            "posy": "37.402324",
            "address": "京畿道 城南市盆唐区三坪洞678",
            "roadname": "京畿道 城南市盆唐区パンギョ駅路240"
        }
    },
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": ""
    }
}
```

##### フィールド

| 名前                         | タイプ     | 説明                                      |
| --------------------------- | ------- | ---------------------------------------- |
| header                      | Object  | ヘッダ領域                                   |
| header.isSuccessful         | Boolean | 成否                                   |
| header.resultCode           | Integer | 失敗コード                                   |
| header.resultMessage        | String  | 失敗メッセージ                                  |
| search			                  | Object  | 本文領域                                   |
| search.result                   | Boolean  | 成否                                 |
| search.entrypoint                   | Array  | 最適地点情報                                  |
| search.entrypoint[0].what3words              | String | what3wordsアドレス                      |
| search.entrypoint[0].posx           | String | x座標                            |
| search.entrypoint[0].posy           | String | y座標                         |
| search.entrypoint[0].address           | String | 法定洞の住所                         |
| search.entrypoint[0].roadname           | String | 道路名の住所                       |

## Static Map

### 1\. Static Map

* ユーザーが指定したマップ範囲の静的マップイメージを返します。

#### リクエスト

[URI]

| メソッド | URI                                      |
| ---- | ---------------------------------------- |
| GET  | /maps/v3.0/appkeys/{appkey}/static-maps?lon={lon}&lat{lat}&zoom={zoom}&bearing={bearing}&pitch={pitch}&width={width}&height={height}&x2={x2}&mx={mx}&my={my}&imgUrl={imgUrl}|

[Path parameter]

| 名前  | タイプ  | 要否 | 有効範囲 | 説明  |
| ------ | ------ | ----- | ----- | ------ |
| appkey | String | 必須 |       | 固有のアプリケーションキー |

[Request Query Parameter]

| 名前    | タイプ  | 要否 | 有効範囲 | 説明                                    |
| -------- | ------ | ----- | ----- | ---------------------------------------- |
| lon   | String | 必須 |       | リクエストするlongitude(経度)座標        |
| lat   | String | 必須 |       | リクエストするlatitude(緯度)座標          |
| zoom   | String | 任意 |       | リクエストする座標の拡大レベル                              |
| bearing     | String | 任意 |       | リクエストする座標の回転率                               |
| pitch     | String | 任意 |       | リクエストする座標の傾き(0～30)   |
| width    | String | 任意 |       | リクエストするイメージのwidth値 |
| height    | String | 任意 |       | リクエストするイメージのheight値 |
| x2    | String | 任意 |       | イメージサイズ * 2を返すかどうか |
| mx    | String | 任意 |       | マーカーを表示する座標(longitude)   |
| my    | String | 任意 |       | マーカーを表示する座標(latitude)   |
| imgUrl    | String | 任意 |       | マーカーを表示するイメージURL   |


#### レスポンス

##### レスポンス本文
<img src="http://static.toastoven.net/toastcloud/notice/20191029_Maps_new/map_static.png">
