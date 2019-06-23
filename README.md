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

# ハンズオン環境および前提
本ハンズオンは，Kubernetesクラスターの動作環境としてAWSを使用します。K8s(OCP)クラスターは構築済です。
受講者は，K8s(OCP)クラスターに対するCUI操作をを行う際は，クライアントPCからSSHなどでEC2インスタンスに接続し，EC2からCLIを使用して，K8s(OCP)クラスターに対する操作を行います。GUIによる操作は，クライアントPCのブラウザを使用します。
このため以下の準備を事前に済ませておいてください。
- SSH用ツール
- ブラウザ(Google Chrome or Firefox)

# 1) Kubernetesクラスター(OCP4)の構築
IPIを使用してK8s(OCP)クラスターを構築します。

# 2) アプリケーションのデプロイ
OCPはカタログ機能を備えています。JavaやPythonなどの各種ランタイムやデータベースなどのミドルウェアを簡単にK8s上で使うことができます。実際にカタログ上からK8s上にデプロイしてみましょう。

                                                                                                                                          左側メニューからCatalog > Developer Catalog > Python を選択します。

# 3) コンテナイメージのビルド&デプロイ
各自のコンテナイメージを作成し，OCP上にデプロイします。

# 4) CI/CDによる自動デプロイ