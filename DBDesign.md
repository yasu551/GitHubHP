# Table of contents

- Ch. 1 DBを制する者はsystemを制す
- Ch. 2 論理設計と物理設計
- Ch. 3 論理設計と正規化；なぜtableは分割する必要があるのか?
- Ch. 4 ER図；複数tableの関係を表現する
- Ch. 5 論理設計とperformance；正規化の欠点と非正規化
- Ch. 6 DBとperformance
- Ch. 7 論理設計とbad know-how
- Ch. 8 論理設計のgray know-how
- Ch. 9 一歩進んだ論理設計；SQLで木構造を扱う

# Ch. 1 DBを制する者はsystemを制す

- 1-1 systemとDB
- 1-2 DBあれこれ
- 1-3 system開発の工程と設計
- 1-4 設計工程とDB

学習のpoints
- DBとDBMSは異なる
    - DB: dataの集積を指す論理的概念
    - DBMS: DBを実装したSW
- DB設計を制する者はsystem開発を制す
    - systemはdataのformatに合わせて作られる
- DB設計時、DBは次の３層にわけて考える
    - 外部schema
    - 概念schema
    - 内部schema


## 1-1　systemとDB

- data: ある形式に揃えられた事実
- 情報: dataからある文脈・観点に従って集約・加工したもの

user -dataを登録-> DBMS -情報を抽出-> user
                            |
                            観点・文脈

## 1-2 DBあれこれ

## 1-3 system開発の工程と設計

## 1-4 設計工程とDB

Schema: DBのdata構造やformat
- 外部schema: userが使う機能とinterfaceの定義するschema
    - Viewに相当する
    - 外部model: 外部schemaに基づいてsystemを記述したmodel
- 概念schema: dataの要素、およびdata同士の関係を定義するschema
    - 開発者から見たDB
    - 論理data model: 概念schemaに基づいてsystemを記述したmodel
- 内部schema: 論理data modelをDBMS内に格納する方法を定義するschema
    - DBMSから見たDB
    - 物理deta model: 内部schemaに基づいてsystemを記述したmodel

概念schemaがあることにより、data独立性が保証される。

Data独立性: schema間の独立性
- 論理的data独立性
- 物理的data独立性

# Ch. 2 論理設計と物理設計

DB設計では、論理設計(概念schema)と物理設計(内部schema)を行う。
次の要件を満たすために、注意すべきことを述べる: 信頼性（可用性）, 性能, capacity

- 2-1 概念schemaと論理設計
- 2-2 内部schemaと物理設計
- 2-3 backup設計
- 2-4 recovery設計

学習のpoint
- 論理設計は物理設計に先立つ
- DBMSの設計者は、file levelで物理設計を考える
- Sizingは難しい
- RAIDは、信頼性、性能、財布を考慮する
- backup and recoveryは重要。

## 2-1 概念schemaと論理設計

論理設計：概念schemaを定義すること。物理層の制約にとらわれないで定義する。

DB設計の手順
1. 概念schema(論理設計)
2. 内部schema(物理設計)

料理に合わせて器を決める；概念schemaに合わせて内部schemaを決める

### 論理設計のstep: 保存すべきdataとそのformatを決める

1. entityの抽出
2. entityの定義
3. 正規化
4. ER図の作成

### Entityの抽出
Entity: dataの集合体
- 物理的実体：顧客、社員、店舗、車
- 仮想的実体：税、会社、注文履歴

### Entityの定義: entityが保持すべきdataを決めること

属性(attribute): entityが持つdata

### 正規化: entityをsmoothに利用できるように整理する作業

dataの登録・変更・削除が整合的に行えるように、entityのformatを整理する

### ER図の作成

ER図：entity間の関係性を表す図

## 2-2 内部schemaと物理設計

物理設計：dataを格納するための物理的領域や格納方法を決めること；論理設計の結果をもとに

### 物理設計のstep

1. table定義
2. index定義
3. HWのsizing
4. storageの冗長構成決定
5. fileの物理配置決定

### table定義: 概念schemaをtable単位に変換すること
ER model(論理model) -> table定義 -> table(物理model)

### index定義: dataの索引を決める

索引の利用により、検索時間が短縮する

### HWのsizing

- systemで利用するdata sizeを見積もり、それに十分な容量のstorageを選定する
- systemが十分な性能を発揮できるだけのspecのCPUやmemoryを持ったserverを選定する

性能問題のほとんどは、storageのI/O neckにより引き起こされる。

次のものの間にtrade-offが存在する
- dataの整合性
- performance

Capacity sizing
- systemで利用するdata量: 論理設計終了時にDB内に格納するdata量を算出する
    - 次のもののdata量: table, text, image, HTML
- service終了時のdata増加率
    - 増加率の見積もりが難しい場合は、以下のapproach
        - 安全率を大きくとって、余裕をもたせたsizingを行う
        - 仮に後で容量が不足した場合に、簡単に記憶装置を追加できるような構成にしておく

Performance sizing
- 性能要件
    - 処理時間：特定の処理が終了するまでにかかる時間
    - throughput: 単位時間あたりの処理回数; TPSを使う
- resource使用量の基礎数値：新規systemをzeroから構築するときに必要になる数値
    - 処理に対するHW resourceの消費量の相関関係を知りたい
    - Resource消費量を推定する方法
        - 類似sytemのdataを流用する
        - 開発初期にprototype systemを構築し、性能検証を実施する

Sizingには不確定要因(risk)がついてまわる
- performance
- capacity

安全率とscalabilityに留意したsizingを行う必要がある。

RAID(Redundant Array of Independent Disks): systemの信頼性（可用性）、性能を高める技術
- 複数diskを束ねて仮想的に1つのstorageとする技術；まとめられたdiskをRAID groupとよぶ
- 基本的な考え方：複数diskに同じdataを書き込む
- storageを冗長化することで、信頼性が高まる。
- 複数diskにdataを分散させる。これにより、disk I/Oが分散され、性能が向上する

DB物理設計では、RAIDに関して以下のことを考える必要がある
- 当該dataに求められるものはなにか；信頼性？性能？
- 採用するRAID level
- RAIDを構成するdisk本数

RAID level
- RAID0(striping): dataを異なるdiskに分散させる。冗長性はない
    - disk本数が増えれば、I/O性能は向上する
- RAID1(merroring): 2本のdiskに全く同じdataをもたせる。性能は向上しない
    - disk本数が増えれば、信頼性は向上する
- RAID5(parity分散): dataともにparityと呼ばれる誤り符号訂正符号を分散して格納する。
    - diskが壊れても、parityから実dataを復元できる
    - １本までならば、diskを保全できる
    - disk本数が増えるほど読み出し性能が向上する
    - 書き込み性能は高くない；parityの計算を行うため
- RAID10: RAID1のgroupを２つ作り、そのgroupを使ってRAID0をつくる
    - stripingして2本にdataを分散させる。そして、それぞれをmerroringする。
    - 欠点：costが高い；最低４本必要

勘所：最低でもRAID5で構成する。資金に余裕があればRAID10。

### Fileの物理配置

DBに格納されるfileの種類
- data file
- index file
- system file
- 一時file: 次のようなdataを一時保存する
    - sub-queryにより展開されたdata
    - group by句やdistinctを利用したときのsort data
- log file: 変更情報を蓄えるfile；蓄えられた変更情報を一括でdata fileに反映させる

この５つのfileの物理配置を考える際、最も重要なことはsizeと性能である。
性能を最も上げるためには、各fileを異なるRAID groupに配置する必要がある。
costを下げたければ、I/O costが低いfilesを一つにまとめる。

## 2-3 backup設計

Data損失事故を起こさないための必要な設計方針
- 極力dataを失わないように設計する；RAID設計
- Dataを復旧できるように設計する；backup設計とrecovery設計

Backup: file copy
- full backup(完全backup): すべてのdataをbackupする方法
    - 欠点
        - backupの時間が長い
        - HW resourceへの負荷が高い
            - storageにおけるdisk I/O , server CPU and memoryの使用量が増える
        - service停止が必要
- differential backup(差分backup): 前回のfull backupからの差分をbackupする方法
    - full backupから変更履歴をbackupする；log file(transaction log)をbackupする
    - 利点：backup data量やbackup時間が減る。full backupと比較して
    - data復旧には、前回のfull backupと直近のlog fileが必要
    - 欠点：復旧に手間がかかる
- incremental backup(増分backup): 前回の任意のbackupからの差分をbackupする方法
    - 利点: backup data量やbackup時間が減る。differential backupと比較して
    - 欠点: 復旧手順が複雑になる

**backup costが低いほどrecovery costは高い**

### Backup方式の選択方法

考慮points
1. 復旧の必要があるか？いつの状態に復旧させる必要があるか？
2. backupに使用できる時間(backup window)
3. recoveryに使用できる時間(recovery window)
4. 何世代までのdataを残す必要があるか？(保管用の媒体sizeに影響)

選択肢
1. backupしない；backup file以外からdataを復旧させる手段がある場合
    - 入力fileをsystemからもう一度登録することで、dataが復旧される場合
2. full backupのみ
    - backup data size, backup windowが大きくなる
    - 最新の状態に戻せない
3. full backup + 差分backup
4. full backup + 増分backup

## 2-4 recovery設計

Backup fileだけでは、dataを障害発生前の状態に戻すことはできない。
次の2つのことをすることで、障害直前の状態のdataに復旧できる
1. restore: backup fileを戻す
2. recovery: backupしていたtransaction logを適用して変更分を反映させる
3. roll forward: DB serverに残っているtransaction logを適用する

# Ch. 3 論理設計と正規化；なぜtableは分割する必要があるのか?

DBに格納されるdataを整合的に保持するための方法論を身につける。
正規化の目的と理論を理解することで。

- 3-1 tableとは
- 3-2 tableの構成要素
- 3-3 正規化とは
- 3-4 第1正規形
- 3-5 第2正規形; 部分関数従属
- 3-6 第3正規形; 推移的関数従属
- 3-7 Boyce/Codd 正規形
- 3-8 第4正規形
- 3-9 第5正規形
- 3-10 正規化についてのまとめ

学習のpoints
- RDBにおけるtable: 同じ種類のものの集合
- Key: ある情報を引き出すための鍵；主keyが最も重要
- 正規化: dataの冗長性をなくす作業；目的：更新時のdata不整合を防止する
- 関数従属を理解するためには、keyが重要

## 3-1 tableとは

Table: 共通点を持ったrecordの集合

**Table名はすべて複数形または複数名詞でかける。そうでなければ、そのtableにはどこか間違いがある**

Tableは、現実世界と結びついた意味を持っている必要がある。
この基本から足を踏み外すと問題が生じる；Ch. 7-8参照

## 3-2 tableの構成要素

構成要素
- 行: tableの横のdataの組
- 列: tableの縦のdataの組
- Key: あるrecordsを特定するbための鍵
    - 主key(primary key): 一意に識別できる列の組み合わせ
        - tableにおいて必ず１つだけ存在する
    - 候補key(candidate key): 主keyとして利用可能なkey
    - super key: 主keyと非主key列の組み合わせ
    - 外部key(foregin key): 他のtableと関係をもつkey
        - あるtableの列に対して、参照整合性制約をかける
        - 親tableに存在しないものは、子tableでは使えない
        - dataの削除は、子から親の順で行う
        - cascade: 親tableの参照されてるkeyを変更・削除したら、子tableにその変更・削除による影響を反映させる

**keyとなる列には、表記体系の定まった固定長文字列を用いる**

制約
- NOT NULL制約
    - 列に可能な限り、これをつける
- 一意制約: ある列の組について一意性を求める制約
- CHECK制約: ある列の取りうる値の範囲を制限するための制約

table名のnamespace: domain, schema

関係と表は異なるものである

||関係|表|
|-|-|-|
|重複するrecodeは存在してよい|No|Yes|
|recodeは上下の順序をもつ|No|Yes|
|列は左右の順序をもつ|No|Yes|

## 3-3 正規化とは

正規化: あるruleに従った形に整理する
正規形: 以下を満たすためのdata形式
- dataが冗長でない
- dataに一貫性がある

冗長性: 1つの情報が複数のtableに存在する
非一貫性: 複数tableに存在する同一dataに整合性がない


## 3-4 第1正規形

定義: 1つのcellには、1つの値しか含まない

第1正規形: scalar値から構成されるtable

第1正規化する理由：主keyが各列の値を一意に特定できない

正規化: tableのすべての列が関数従属性を満たすように整理すること
関数従属性(functional dependency): X列の値を決めれば、Y列の値が１つに定まる性質

## 3-5 第2正規形; 部分関数従属

第2正規化: table内の部分関数従属を解消し、完全関数従属のみのtableをつくること
部分関数従属：主keyの一部の列に対して、ある列が従属していること

第2正規化の方法；table分割
1. 部分関数従属の関係にあるkey列と従属列を見つける
2. そのkey列と従属列をとりだし、それらからなるtableをつくる

第２正規化する理由: 依存関係のないdataに対して考える必要がなくなる
第２正規化: 複数entitiesを別々のtableに分割すること

無損失分解: 情報を完全に保存したままtableを分解すること
可逆的(reversible)操作: 操作する前の状態に戻せる操作

第2正規化は可逆的であるため、それをする前の状態に戻せる。

## 3-6 第3正規形; 推移的関数従属

推移的関数従属: table内部に存在する段階的な従属関係
                    これ
                    |
{主key} -> {非主key} -> {非主key}
{会社コード, 社員ID} -> {部署コード}　-> {部署名}

第3正規形: 推移的関数従属がない第2正規形

## 3-7 Boyce-Codd 正規形(BCNF)

BCNF: 非keyからkeyへの関数従属がない第3正規形

PK={社員ID,チームコード｝
PK -> チーム補佐
チーム補佐 -> チームコード

BCNF出ないときに、発生する問題
- チーム補佐が担当チームを変える場合、複数行の更新が発生する(dataの冗長性)
- 社員がチームに参加するまで、チーム補佐とチームの関連を登録できない
- 社員がチームから外れたときにレコードを削除すると、チーム補佐とチームの関連も削除される危険がある

table間の関係性が1対多になるように、tableを複数のtablesに分解する。
参照先のkeyが一意である必要がある。

## 3-8 第4正規形
関連entity: entity同士の関連を表現するentity

## 3-9 第5正規形
## 3-10 正規化についてのまとめ

# Ch. 4 ER図；複数tableの関係を表現する

# Ch. 5 論理設計とperformance；正規化の欠点と非正規化

# Ch. 6 DBとperformance

# Ch. 7 論理設計とbad know-how

# Ch. 8 論理設計のgray know-how

# Ch. 9 一歩進んだ論理設計；SQLで木構造を扱う


