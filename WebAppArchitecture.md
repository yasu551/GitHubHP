1. Introduciton
2. Before the Web: TCP/IP
3. Birth of the World Wide Web: HTTP
4. Web Servers
5. Web Browsers
6. HTML and its Roots
7. XML Languages and Applications
8. Dynamic Web Applications
9. Approaches to Web Application Development
10. Application Primer: Virtual Realty Listing Services
11. Emerging Technologies

## 1. Introduciton

#### The Web in Perspective

- Berners-Leeがinformation management systemを提案した
- knowledgeとresourceを共有できる。computer network上で。
- そのsystemは、World Wide Webという名前で広がっている

#### The Origins of the Web

#### From Web Pages to Web Sites

#### From Web Sites to Web Applications

#### How to Build Web Applications in One Easy Lesson

#### What is Covered in this Book

## 2. Before the Web: TCP/IP

#### TCP/IP
- TCP/IP Protocol Suiteは、ARPANETが進化したものである
- The Suiteは、layerd taxonomy of data communications protocolsである。
- TCP/IPで重要なprotocolは、以下である
    - TCP: Transmission Control Protocol
    - IP: Internet Protocol
- The suiteは他にも多くのprotocols and servicesからなる

#### Layers

TCP/IPと関連のあるprotocol layersは以下である。
- the Network Interface layer
    - TCP/IP内のdata transmissionのlowest levelの責任をもつ
    - the underlying physical networkとcommunicationを促す
- the Internet layer
    - 以下のことをするためのmechanismsを提供する
        - intersystem communications
        - controlling message routing
        - validity checking
        - message header composition/decomposition
    - IP(Internet Protocol)がこのlayerをoperateする
    - そのときICMP(the Internet Control Message Protocol)も動く
    - ICMPは、control transmissionとerror messagesを操縦する。systems間の
    - Ping: internet service. ICMPを通してoperateする
- the Transport layer
    - message transport servicesを提供する。remote systemsで駆動しているapplication間の
    - this layerではTCP(the Transmission Control Protocol)がoperateする
    - TCPは、reliable, connection-oriented message transportを提供する
    - Internet servicesとしてよく知られるもののほとんどは、それらの基礎としてTCPを使用している。
    - reliabilityを要求しないsome servicesはUDP(Use Datagram Protocol)を使用する
- the Application layer
    - TCP/IP protocol stackでhighest levelのlayerである
    - the Internetと関連するservicesのほとんどがoperateする


This protocol taxonomyはlayersを含むため、それらprotocolsの実装はよくprotocol stackと呼ばれる。

These Intenet servicesは、いくつかのdegreeを提供する。information exchangeのdegree。それはthe webの誕生を得た。初めの夢を結実するために。その結実は、初期のdevelopersは決して想像してなかったであろう

#### The client/server paradigm

TCP/IP applicationsは、client/server paradigmによってoperateする。
それらapplications上では、serversは次を実行する。
1. client pragramsからrequestsが到着するのを待つ
2. そのとき、あれらrequestsを処理する

serversは、services and daemonsと呼ばれる。underlying OSの言語に依存する

Client pragramsは、人が使用するapplicationsである。
serversは自信のrequestsを作る必要がある。
そのrequestsは他のserversによってのみ満たされる。
clientとserverは、別々のmachinesで走る。networkを横切るconnectionを介してcommunicateする。

client/server architecturesの初期の実装は、open protocolsを使用しなかった。
client programsは、server programsと同じくらいheavyにする必要がある。
lightweight(thin) clientはframeworkにだけ存在する。そのframeworkはcommon protocols and application controlsはclient machines's OSに関連する。
そのようなframeworkなしで、connectivity featuresのほとんどは、直接client programに含まれる必要があった。その重さに加えて。

client/server applicationsのためのTCP/IPを使用する利点は、以下である。
- protocol stackは、client machineにinstallされる。OSの一部として
- clinet program自身は、thin clientよりもよい

Web applicationsは主要例である。applicationsのthin clientsのemploymentの例。
所望のapplication taskを実行するためにcustom programをbuildingするよりも、
web applicationsはweb browserを使う。programはほとんどのuser's systemsにすでにinstallされている。
あなたは、あるprogramよりもthinなclientを作れない。そのprogramはusersのdesktopsにinstallされている。

##### How Do TCP/IP Clients and Servers Communicate with Each Other?

serversと話すために、TCP/IP client programsはsocketを開く。そして、それは簡単なTCP connectionである。client と serverの間のconnection。
Serversはconnection requestsを聞く。特定のportsを通してくるrequests。
portはactual physical interfaceではない。computerとnetworkの間のinterface。request内の多くの参照(server programが指し示すrequest)はそれの意図したrecipientである。
それらは達成された合意である。port numbersと適合するために。特定のTCP/IP serverのport number.Serversはrequestsをきく。よく知られたport numbers.
Telnet serverは, port 23のconnection requestsをきく
SMTPは, port 25. web serverは port 80.

### TCP/IP APPLICATION SERVICES

common TCP/IP application servicesについて議論する。
Telnet, electronic mail, message forums, live massaging, and file servers

#### Telnet

Telnet protocolはapplication layer内でoperateする。
それはNetwork Virtual Teminal functionalityを支援するために開発された。そして、それは log inの能力である。Internetを通るremote machineへのlog inである。
Telnet protocolの詳細はInternet RFC 854.

Internet servicesの到来で、あなたはTelnet protocolを使える。他のsystemsへremoteでlog inするために。そのsystemsはInternetを通してaccess可能である。
初期は、Telnet clientsはdefautでport 23により接続していた。server machineに。しかし、そのtarget port numberはほとんどのclient programsですでに使われているに違いない。
あなたはTelnet client programを使える。任意のTCP serverへ接続し会話するために。そのaddressとport numberを知ることで。


#### Electronic mail

Electronic mail(e-mail)は、first killer appである。cyberspaceにおいて。
TCP/IPの到来で、それらservicesを提供するためのmechanismsはより一貫性をもった。そして、e-mailは統一化され、ubiquitousになった。
electronic mailのtransmissionはSMTP protocolを通して行われる。
electronic mailのreadingはたいてい、POP or IMAPを通して行われる。

##### SMTP(Simple Mail Transfer Protocol)

application layer protocol SMTPが普通TCPのtop上で走るとき、それは理論的には任意のunderlying transport protocolで使える。
このapplicationはsendmailと呼ばれる。それはSMTP protocolの実装である。UNIX systemsのための。
SMTP protocolの詳細はInternet RFC 821, SMTP messagesの構造はInternet RFC 822。

SMTPはserver, service, or daemonとして走る。
TCP/IP 環境では、SMTP serversはport 25で走る。
それらはrequestsを待つ。electronic mail messagesを送信するために。そして、それはlocal system users or across the networkから来る。
それらは次の責任を持つ。recipient addressを評価する。e-mail messagesの中から探す。それらはvalidであるかどうか　and/or final destinationはもう一つのrecipientかどうかをを定める。e.g. forwarding address, or the set of individual recipients subscribed to a mailing list.

もしrequest内に埋め込まれたmessageがlocal systemにaccountをもつuserを意図しているなら、SMTP serverはそのmessageをそのuserに運ぶ。それをmailboxに入れることによって。
実装に依存して、mailboxはsimple text fileからe-mail messageのcomplex DBへ送るなにかである。
もしthe messageがもう一つのsystemのuserのためのものなら、serverはthe messageを適切なsystemへ送信する方法をはっきりさせる必要がある。


##### POP()

##### IMAP()



## 3. Birth of the World Wide Web: HTTP


## 4. Web Servers


## 5. Web Browsers


## 6. HTML and its Roots


## 7. XML Languages and Applications


## 8. Dynamic Web Applications


## 9. Approaches to Web Application Development


## 10. Application Primer: Virtual Realty Listing Services


## 11. Emerging Technologies