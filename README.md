test msg

    TEST

    TEST2

        TEST3

test call

    TEST

    TESTTEST

```git pull```

`git pull`

```sh
git pull
```

```test.sh
git pull
    git pull
        git pull
            git pull
            
    >git pull
        aaa
        aaa
    > git pull
    >   git pull
    >       git pull
```

>aaa
>aaa
    >aaa
    >aaa

aaa
aaa
###############
# タイムテーブル
|Time|Agenda|Content|
|:---:|:---|:---|
|13:00-13:30|受付||
|13:30-14:00|Red Hat OpenShift 4 概要|<講義>|
|14:30-15:30|Red Hat OpenShift 4 基礎ワークショップ|<ハンズオン> <br> OpenShift 4 環境デプロイメント|
|15:30-15:45|Break|
|15:45-16:45|Red Hat OpenShift 4 基礎ワークショップ|<講義+ハンズオン> <br> OpenShift 4 を活用したビルド/デプロイメントパイプライン|
|16:45-17:00|まとめ||

# ハンズオン概要
本ハンズオンは，OpenShift4(以降，OCPまたはOCP4)の基礎編です。

以下を学びます。
- Kubernetesクラスター(OCP4)の構築
- アプリケーションのデプロイ
- コンテナイメージのビルド&デプロイ
- CI/CDによる自動デプロイ

なお，インフラエンジニア向け，アプリ開発エンジニア向けを想定した発展的なコンテンツについては，今後のワークショップで実施予定です。

# ハンズオン環境および前提
本ハンズオンは，Kubernetesクラスターの動作環境としてAWSを使用します。K8s(OCP)クラスターは構築済です。
受講者は，K8s(OCP)クラスターに対するCUI操作をを行う際は，クライアントPCからSSHなどでEC2インスタンスに接続し，EC2からCLIを使用して，K8s(OCP)クラスターに対する操作を行います。GUIによる操作は，クライアントPCのブラウザを使用します。
このため以下の準備を事前に済ませておいてください。
- SSH用ツール
- ブラウザ(Google Chrome or Firefox)

# 0) Kubernetesクラスター(OCP4)の構築
IPIを使用してK8s(OCP)クラスターを構築します。
XXXX


# 1) OCPコンソールツアー


# 2) アプリケーションのデプロイ
OCPはカタログ機能を備えています。JavaやPythonなどの各種ランタイムやデータベースなどのミドルウェアを簡単にK8s上で使うことができます。実際にカタログ上からK8s上にデプロイしてみましょう。

## 2-1) プロジェクトの作成
1. ブラウザを立ち上げて **OCPコンソール** に接続します

    - Console URL: `https://oauth-openshift.apps.ocp41-ipi-0611.k8show.net`
    - Username: `capsmalt`
    - Password: `xxxxxxxx`
    
    > 自身のOCPクラスターのログイン情報を使用してください。
    > 
 
1. Home > Projects > Create Project を選択します

1. 任意のプロジェクト名を指定し，**Create** を選択します

    >Tips:
    >
    >OCPではプロジェクトを作成することで，新規Namespace(=プロジェクト名)が生成されます。NamespaceはK8sクラスターを論理的に分離させることが可能なK8sリソースの一種です。例えば，アプリA用のNamespaceを`ns_appa`，アプリB用のNamespaceを`ns_appb`のように作成することで，同一のK8sクラスター内に存在するns_appaとns_appbが干渉しないように構成することも可能です。


## 2-2) カタログ(ソース)からアプリケーションをデプロイ
1. Catalog > Developer Catalog > Python を選択します

    >Tips:
    >
    >Developer CatalogからPythonアプリケーションを作成することで以下のリソースが作成されます。
    >- Build config
    >    - Gitリポジトリからソースコードをビルド
    >- Image stream
    >    - ビルド済イメージのトラッキング
    >- Deployment config    
    >    - イメージ変更の際に新リビジョンにロールアウト
    >- Service
    >    - クラスター内にワークロードを公開
    >- Route
    >    - クラスター外にワークロードを公開

1. 任意の**アプリケーション名**，**Gitリポジトリ** を指定します

    - Name:`任意の名前(例: mypyapp)`
    - Git Repoaitory: `https://github.com/sclorg/django-ex.git` 
      - ("Try Sample↑" をクリックするとURLがセットされます)

1. 最後に **Create** を選択します

    >Tips:
    >
    >指定した名前のアプリケーション(コンテナ)が動作するPodがデプロイされました。
    >OCPコンソールで，Workloads > Pods > アプリ名-x-xxxx のように辿ることで確認できます。


## 2-3) 外部からアクセスするためのRoute(ルート)を作成
1. Networking > Routes > Create Route を選択します
1. 任意の**Route名**，対象アプリ用の**Service**，**Port** を指定します
    - Name: `任意の名前(例: mypyroute)`
    - Service: `mypyapp`
    - Target Port: `8080 → 8080(TCP)`
1. 最後に **Create** を選択します

    >Tips:
    >
    >Networking > Routes > ルート名 のように辿ることで確認できます。

## 2-4) アプリケーションの動作確認
1. Networking > Routes > ルート名 を選択します
1. Location欄にあるリンクを開きます
    例: `http://mypyroute-myprj.apps.ocp41-ipi-0611.k8show.net`
1. Pythonアプリのサンプルページが表示されることを確認します

## Option-1) 既存コンテナイメージを使ってOCPにアプリデプロイ
1. 任意のプロジェクトを選択
1. Home > Project > 作成済プロジェクト > Add > Deploy Image
1. Namespace(プロジェクト名)，とImage Nameを指定して，検索ボタンをクリック
    - Namespace: `作成済プロジェクト(例: myprj)`
    - Image Name: `quay.io/openshiftlabs/workshop-terminal:2.4.0`

quay.io/openshiftlabs/workshop-terminal:2.4.0


```
oc project myprj
oc project
oc adm policy add-scc-to-user anyuid -z default -n myprj
```


# 3) コンテナイメージのビルド&デプロイ
各自のコンテナイメージを作成し，OCP上にデプロイします。

# 4) CI/CDによる自動デプロイ