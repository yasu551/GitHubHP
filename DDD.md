# 序文: 問題domainの複雑さをcontrolする

# まえがき

成功したprojectに共通する特徴
- 豊かなdomain modelがある。
- domain modelは、projectの基礎となった。
- domain modelは設計のiterationを通じて進化した。

本書が提供するもの
- framework: 設計上の意思決定を行うためのもの
- 技術的な語彙: domain設計について議論するためのもの

設計を成功させるためには、domainの複雑さを扱う必要がある。
また、それは体系的に扱う必要がある。

本書の前提
- 一番の焦点は、domain and domain logicに合わせる必要がある
- 複雑なdomain設計は、modelに基づいている必要がある

Agile 開発 processの2 practicesが定着している必要がある
- 開発がiterativeである
    - Surviving Object-Oriented Projects
    - Extreme Programming Explained
- 開発者とdomain expertが密接に関わっている
    - DDDは、domainに対するdeep insight と主要な概念を反映させたmodelを構築する
    - domain expertと開発者が膨大な知識を噛み砕くことで、そのmodelが構築される
    - このmodel構築は、project期間中に継続的に行われる

DDDとAgile開発が互いにどう補強し合うのかを説明する。設計と開発のpracticeを絡み合わせることで
- Domain modelingに対するapproachは、agile開発processでは開発の加速につながる
- processとdomain開発の相互作用され、他のどのapproachよりも実用的である

## 本書構成

- Part 1: domain modelを機能させる
    - DDDの基本的な目標; practicesを実践する動機となる
    - communication and designのために、domain modelを使用する意味を概観する
    - core chapters: 2, 3, 9, and 14
- Part 2: model駆動設計の構成要素
    - best practice's coreを要約し、基本的な構成要素の集合を作り上げる；Object-Oriented Domainn modelingにおけるbest practice
    - modelと実装されたSWとの間の溝を埋める方法を知る
    - 標準patternの共有により、設計に秩序がもたらされる
    - team memberは互いの仕事を容易に理解できる
    - 共通言語に用語法が適用されることで、all team memberがmodelと設計上の意思決定について議論できる
- Part 3: deeper insightへ向かうrefactoring
    - 次の課題に進む；利益をもたらす実用的なmodelを組み立てる
    - 発見processを重視する
    - modelの探求とcodeへの反映の繰り返すことで、豊かなmodelを組み立てる
    - 探求おいて有用なmodeling原則とtechniqueをしる
        - modeling原則: 選択の指針
        - technique: 探求の方向づけ
- Part 4: 戦略的設計
    - 複雑なsystemとの相互作用において発生する問題に対処する
    - systemに対して適用される3原則
        - context
        - 蒸留
        - 大規模な構造: 巨大system; 無秩序に広がるnetworkに組み込まれるsystem

## Domain駆動team

最大の収穫が得られる；TeamがDDD approachを適用し、domain modelが会話の中心になったとき。
CommunicationがSWとつながった状態を保てる；Team memberは言語を共有し、communicationを豊かにすることで。
Teamはmodelと一致した実装を作り出し、app開発に力を与える。
組織にとって最も価値のある機能を体系的にみれる；各teamの設計作業が関係性が明らかになるため。

# 目次

- Part 1: Domain modelを機能させる
    domain駆動設計におけるmodelの有用性、SWの核心
    - Ch. 1: 知識を噛み砕く
    効果的なmodelingの要素、知識の噛み砕き、継続的学習、知識豊富な設計、深いmodel
    - Ch. 2: communicationと言語の使い方
    Ubiquitous language, 声に出してmodelingする, 1 teamに1 language, documentと図, 説明のためのmodel
    - Ch. 3: modelと実装を結びつける
    Model-deriven design, modeling paradigmとtoolによるsupport, 骨格をみせる：なぜmodelがuserにとって重要なのか?, Hands on modelers
- Part 2: model駆動設計の構成要素
    - Ch. 4: domainを隔離する
    Layered architecture, domain層はmodelが息づく場所, smart UI "anti-pattern", その他の隔離
    - Ch. 5: SWで表現されたmodel
    関連, entities(reference objects), value objects, services, modules(packages) moding paradigm
    - Ch. 6: domain objectのlifecycle
    aggregates, factories, repositories, 関係DBに合わせてobjectを設計する
    - Ch. 7: 言語を使用する：応用例
    貨物輸送systemを導入する、domainを隔離する:appの導入、entities and value objectsを区別する、輸送domainの関連を設計する、集約の境界、repositoryを選択する、scenarioをwalk throughする, objectの生成, refactoringのために立ち止まる、輸送modelにおけるmodule, 新機能を導入する
- Part 3: deeper insightへ向かうrefactoring
    refactoringのlevel, deeper model, deeper model or しなやかな設計、発見のprocess
    - Ch. 8: breakthrough
    breakthroughの話、好機、基本への集中、新しい洞察の連鎖
    - Ch. 9: 暗黙的な概念を明示的にする
    概念を掘り出す、それほど明白でない概念をmodel化する方法、specification
    - Ch. 10: しなやかな設計
    intention-revealing interfaces, side-effect-free-functions, assertions, conceptual contours
    - Ch. 11: analysis patternを適用する
    - Ch. 12: design patternをmodelに関係付ける
    - Ch. 13: deeper insightへ向かうrefactoring
- Part 4: 戦略的設計
    - Ch. 14: modelの整合性を維持する
    - Ch. 15: 蒸留
    - Ch. 16: 大規模な構造
    - Ch. 17: 戦略をまとめ上げる