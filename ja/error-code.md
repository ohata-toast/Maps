## Application Service > Maps > エラーコード

## APIエラーコード
|resultCode|	resultMessage|	説明|	備考|
|:---:|:---:|:---:|:---:|
|0|	|成功|	共通|
|100|Result Not Found|		結果なし|	検索専用|
|101|Argument Error|	パラメータエラー|	共通|
|102|Internal Server Error|サーバーエラー|	検索専用|
|201|	Searching for Security| POI	セキュリティ施設|	検索専用|
|202|	Longitude/Latitude |経緯度|	検索専用|
|203|	Mobile Phone Number|携帯電話番号|	検索専用|
|204|	Invalid Query|その他入力範囲エラー|	検索専用|
|205|	POI not in given Admin|結果なし(地域設定)|	検索専用|
|206|	POI not in given Area|結果なし(領域設定)|	検索専用|
|207|	POI not in given Category|結果なし(分類設定)|	検索専用|
|208|	Neighbor Search Only|結果なし(周辺検索のみ入力)|	検索専用|
|209|	Neighbor Search not Found|結果なし(周辺 + キーワード検索結果なし)|	検索専用|
|300|	AppKey Error|アプリケーションキー認証エラー	|共通|
|501|	Unknown Fail|失敗(unknown)|探索専用|
|502|	Apply Smart Re-navigation|Smart再探索適用|探索専用|
|503|	Canceled navigation by user | ユーザーによる探索キャンセル |探索専用|
|504|	Error due to Checksum | チェックサムエラー |探索専用|
|517|	Memory allocation failure | メモリ割り当て失敗 |探索専用|
|518|	File open failure | ファイルを開くのに失敗 |探索専用|
|519|	File read failure|ファイル読み込み失敗|探索専用|
|520|	File write failure|ファイル書き込み失敗|探索専用|
|521|	Socket connection failure |ソケット接続失敗|探索専用|
|532|	Request parameter is invalid | リクエストパラメータが有効ではない |探索専用|
|533|	The starting point is not selected, or the wrong starting point |出発地が選択されていないか、無効な出発地|探索専用|
|534|	Destination is not selected or wrong destination |目的地が選択されていないか、無効な目的地 |探索専用|
|535|	Wrong stopover |無効な経由地|探索専用|
|536|	Link Projection failure | Link Projection |探索専用|
|537|	Exceeding the navigational distance (1000km, walking navigation: 20km) | 探索可能距離超過(1000km、徒歩探索：20km) |探索専用|
|538|	Exceeds the number of expandable nodes | 拡張可能ノード数超過 |探索専用|
|539|	Expansion failure | 拡張失敗 |探索専用|
|540|	Expansion failure due to inactivity or traffic control | 特別な事情や交通規制による拡張失敗 |探索専用|
|541|	Expansion failure due to vehicle height/weight restrictions near the starting point | 出発地付近の車両高さまたは重量制限で拡張失敗 |探索専用|
|542|	Expansion failed due to a part-time curfew near the departure point | 出発地付近の時間制通行禁止により拡張失敗 |探索専用|
|543|	The destination is a physical island road, and there are no established ferry routes. | 目的地が物理的島で、フェリー航路がない |探索専用|
|544|	The departure or destination is a logical (transportation) island, and there are more than one destination |出発地または目的地が論理的(交通)島で、目的地が2個以上の場合 |探索専用|
|545| No data requested | リクエストしたデータがない |探索専用|
