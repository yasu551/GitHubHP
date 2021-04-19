- Ch. 1 小さくまとめてわかりやすくする
- Ch. 2 場合分けのlogicを整理する
- Ch. 3 業務logicをわかりやすく整理する
- Ch. 4 Domain modelの考え方で設計する
- Ch. 5 Application機能を組み立てる
- Ch. 6 DBの設計とdomain object
- Ch. 7 画面とdomain objectの設計を連動させる
- Ch. 8 Application間の連携
- Ch. 9 Object指向の開発process
- Ch. 10 Object指向設計の学び方と教え方

Object指向設計により、以下のような変更の大変さが減る。
- sourceのどこに何が書いてあるのか分かりづらい。
- 1つの修正のために、あっちこっち書き直す必要がある
- 少しの変更が、ありえない場所にまで影響を与える

Object指向設計は、以下のことをする設計法である。
- どこに何が書いてあるかを明らかにする
- 変更の影響を狭い範囲に閉じ込める
- 安定して動作する部品を柔軟に組み合わせる


# Ch. 1 小さくまとめてわかりやすくする

**まとめ**
- Object指向設計は変更を楽で安全にする工夫
- Codeの整理の基本は名前と段落
- 短いmethod、小さいclassを使ってcodeを整理する
- 値objectでわかりやすく安全にする
- collection objectで、複雑なlogicを集約して整理する
- class名やmethod名と業務の用語が一致するほど、programの意図がわかりやすくなり、変更が楽で安全になる

**設計**
- SW全体をすっきりした形に整えること
- どこに何が書いてあるかわかりやすくする
- 修正や拡張が楽で安全になるcodeを生み出す

**変更が大変なprogramの特徴**
- methodが長い; if文が入り組んだmethodは理解しにくい
- classが大きい; 関心事を詰め込みすぎ。class内部のfield-method間の関係性が不明瞭。
- 引数が多い; 引数の関係性が不明瞭。

**programの変更が楽になる書き方**
- 意味のわかり易い名前を使う; 業務で用いてる言葉を使うと変更がらくになる
- 長いmethodは、段落に分けて読みやすくする；空白行を入れる
- 目的ごとに変数を用意する；説明用の変数の導入
- 複数処理をmethodとして独立させる; methodの抽出
- 異なるclassの重複したcodeをなくす
    1. class A, Bのそれぞれで該当する段落をmethodに抽出する
    2. A, Bに参照関係があるなら、3へ(AがBを参照する)。そうでないなら、4へ。
    3. Aで抽出したmethod呼び出しを、Bのmethod呼び出しに書き換える。
    4. 共通method置き場として、別class Cを新たに作成する。そのclassに抽出したmethodを移動する。5へ。
    5. A, Bのmethod呼び出しを、それぞれCの共通methodを利用するように書き換える
- 狭い関心事に特化したclassにする; codeの見通しを良くし、変更をやりやすくする
    - Domain object: 業務の関心事に対するclass
    - 業務とprogramの構造が一致していれば、修正や拡張がしやすい。探しやすいので。
- methodは短く、classは小さく

**特定の目的に特化して、関連するdataとlogicをclassにまとめる**
- 値の範囲を制限する; intの範囲、Stringの使用可能文字列
- Value Object: 値の種類ごとの専用class
    - 不変にする
        - instance変数はconstractorでobjectの生成時に設定する
        - 
    - 別の値が必要になったら、新しく作成する

# Ch. 2 場合分けのlogicを整理する

**まとめ**
- 区分ごとのlogicはprogramを複雑にするやっかいな存在
- 早期returnやguard節を使うと区分ごとのlogicをわかりやすく整理できる
- 区分ごとに別のclassに分けると独立性を高めることができる
- 多態を使うと、区分ごとのlogicをif文 / switch文を使わずに記述できる
- Javaの列挙型(enum)は多態をsimpleに記述するしくみ
- 列挙型を活用すると、区分ごとの業務logicをわかりやすく整理して記述できる

# Ch. 3 業務logicをわかりやすく整理する

**まとめ**
- 変更が大変になるのはdata classと機能classを分けるから
- data classを使うと、業務logicの重複が増える
- application全体のcodeの見通しを良くするためには、dataとlogicを一体にする設計を徹底する
- 業務logicは業務dataの近くにまとめる(domain object)
- Domain modelに業務logicを集める
- Domain modelは画面やDBの都合から独立させる
- ほかの層は業務的な判断/加工/計算のlogicをdomain modelに任せることでsimpleででわかりやすい構造になる

# Ch. 4 Domain modelの考え方で設計する

**まとめ**
- Domain modelは業務logicをobject指向で整理する技法
- Dataの整理ではなく業務logicの整理
- 業務の関心事はヒト/モノ/コトで整理できる
- コトを整理の軸にする
- 起きて良いこと/起きてはいけないことの判断と対応が業務rule
- 業務ruleをobjectで表現する一般的なpatternを覚えておくとdomain modelの設計がやりやすくなる
- domain modelの設計のinputは業務の言葉の正しい理解
- 業務の言葉を正しく覚え、正しく使えるようになることが、良いdomain modelの設計に直結する
- 業務知識をprogramming言語で体系的に表現したdomain modelを中核にした業務applicationは、変更が楽で安全になる

# Ch. 5 Application機能を組み立てる

**まとめ**
- application層は業務処理の進行役であり調整役
- application層のservice classをsimpleに保つことで、system全体の見通しの良さと、変更のやりやすさにつながる
- service classは、さまざま関心事の交差点になり、ごちゃごちゃしやすい
- service classをsimpleに保つための設計の徹底が重要
- 全体を段階的に組み立てながら設計の改善を続ける
- 業務的な判断/加工/計算の詳細はdomain modelに集約する
- 画面の複合した関心事を持ち込まない
- そのためにservice classのmethodを基本処理単位に分解する
- 必要に応じて複合serviceを提供する
- DBのdata操作を意識しないように分解し隠ぺいする

# Ch. 6 DBの設計とdomain object

**まとめ**
- 制約のないDBがprogramを複雑にする
- 制約を徹底するとdata管理がうまくいき、programがわかりやすくなる
- table設計の基本は３つの制約:NOT NULL, 一意性, 外部key
- 良いtable設計のコツは、コトの記録の徹底
- 状態の更新はコトの記録とは独立させる
- Objectとtableは設計の動機ややり方が基本的に異なる
- Objectとtableの設計を独立させやすいしくみを活用する

# Ch. 7 画面とdomain objectの設計を連動させる

**まとめ**
- 画面はapplicationに複雑さを持ち込む
- なんでも画面はわかりにくい
- taskごとの画面に分けて考える
- 画面とdomain objectは、利用者の関心事として一致する
- 画面とdomain objectを一致させる改善が、domain objectの設計を洗練させる
- release note, 利用者guideなど、多くの関係者が理解し確認できる内容と、SWの設計を一致させることが、SWの変更を楽で安全にする

# Ch. 8 Application間の連携

**まとめ**
- application間の連携が、applicationの価値を高める
- 連携方式はfile転送/DB共有/Web API/非同期messagingがある
- Web APIの利用が広がっている
- 肥大化したWeb APIは使う側も提供する側も負担が多い
- APIの変更を楽で安全にするには、小さなAPIに分ける
- 小さなAPIを組み合わせたり一部を変更することで多様なneedsに対応できる
- APIも進化することで価値を生む
- application間を疎結合に連携する非同期messagingは今後の有力な選択肢

# Ch. 9 Object指向の開発process

**まとめ**
- Object指向の良さを活かすには分析と設計を一体にした開発のやり方が必要
- 分析工程と設計工程を分割しない
- 分析と設計を同じ人間が担当する
- 分析設計の成果はcodeで表現する（自己文書化）
- 更新すべきdocumentは利用者guideや業務manual
- source codeを中心に進捗と品質をmanagementする
- 対象業務の理解と整理に意欲がある技術者を選んで育成する

# Ch. 10 Object指向設計の学び方と教え方

**まとめ**
- Object指向は言葉による説明より、具体的なcodeで学ぶのが実践的
- refactoringを参考に、既存codeを改善してみる
- Object指向excerciseの9つruleで練習してみる
- Object指向らしい設計になれてきたら、より深く学ぶために実践パターン、オブジェクト指向入門、ドメイン駆動設計を読むと良い
- 特に、ドメイン駆動設計は、オブジェクト指向設計を現場で実践するためのすばらしい手引き

