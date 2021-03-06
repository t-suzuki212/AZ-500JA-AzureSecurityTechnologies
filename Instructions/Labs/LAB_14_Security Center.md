---
lab:
    title: '14 - Azure セキュリティ センター'
    module: 'モジュール 04 - セキュリティ操作の管理'
---

# ラボ 14: Azure セキュリティ センター
# 受講生用ラボ マニュアル

## ラボのシナリオ

ベースの環境の概念実証を作成するように求められました。具体的には、次のことを行います。

- 仮想マシンを監視するように セキュリティ センター を構成します。
- 仮想マシンの セキュリティ センター の推奨事項を確認します。
- ゲスト構成と Just In Time VM アクセスの推奨事項を実装します。 
- セキュア スコアを使用して、より安全なインフラストラクチャの作成に向けた進捗状況を判断する方法を確認します。

> このラボのすべてのリソースについて、**米国東部** リージョンを使用しています。クラスに使用する地域であることを講師に確認します。 

## ラボの目的

このラボでは、次の演習を行います。

- 演習 1: セキュリティ センター を実装する

### 演習 1: セキュリティ センター を実装する

この演習では、次のタスクを行います。

- タスク 1: セキュリティ センター を構成する
- タスク 2: ゲスト構成拡張機能をインストールするために セキュリティ センター の推奨事項を実装する
- タスク 3: Just In Time VM アクセスを有効にするために セキュリティ センター の推奨事項を実装する

#### タスク 1: セキュリティ センター を構成する

このタスクでは、セキュリティ センター をオンボードし、構成します。

1. Azure portal **`https://portal.azure.com/`** にサインインします。

    >**注**: このラボで使用している Azure サブスクリプションで所有者ロールまたは共同作成者ロールを持つアカウントを使用して Azure portal にサインインします。

1. Azure portal の Azure portal ページの上部にある「**リソース、サービス、ドキュメントの検索**」 テキスト ボックスで、「**セキュリティ センター**」と入力し、**Enter** キーを押します。     

1. 「**セキュリティ センター**」 の \| 「**はじめに**」 ブレードで 、「**アップグレード**」 をクリックし、「**エージェントのインストール**」 をクリックします。    
     
1. 「**セキュリティ センター**」 の \| 「**はじめに**」 ブレードで、「**価格と設定**」 をクリックします。  

1. 自分のサブスクリプションを表すエントリをクリックし、「**設定**」 をクリックします。**|**「**価格レベル**」 ブレードで、**Standard** 価格レベルが選択されていることを確認します。   

    >**注**: Standard 価格レベルの一部として使用できるすべての機能を確認し、各リソースの種類で Standard プランが有効になっていることを確認します。 

1. 変更を行った場合は、「**保存**」 をクリックします。 

1. 「**設定**」 の \| 「**価格レベル**」 ブレードで、「**データ収集**」 をクリックします。  

1. 「**設定**」 の \| 「**データ収集**」 タブで、「**自動プロビジョニング**」 を 「**オン**」  に設定します。 

1. 「**設定**」 の \| 「**データ収集**」 ブレードの 「**ワークスペースの構成**」 セクションで、「**別のワークスペースを使用する**」 オプションを選択し、ドロップダウン リストで、前のラボで作成した Log Analytics ワークスペースを選択します。     

1. 「**設定**」 の \| 「**データ収集**」 ブレードで、「**保存**」 をクリックします。  

1. 「**設定**」 の \| 「**データ収集**」 ブレードで、「**ワークフローの自動化**」 をクリックします。  

1. 「**設定**」 の \| 「**ワークフローの自動化**」 ブレードで 「**+ ワークフローの自動化の追加**」 をクリックします。  

1. 「**ワークフロー自動化の追加**」 ブレードで、使用可能な設定を確認します。  

    >**注**: 脅威検出アラートおよび セキュリティ センター の推奨事項に基づいてアクションをトリガーできます。Logic Apps に基づいてアクションを構成することもできます。 

1. 「**ワークフロー自動化の追加**」 ブレードで、「**キャンセル**」 をクリックします。   

    >**注**: セキュリティ センター は、システムの更新状況、OS セキュリティ構成、エンドポイント保護など、仮想マシンに関する多くの洞察を提供します。

#### タスク 2: ゲスト構成拡張機能をインストールするために セキュリティ センター の推奨事項を実装する

このタスクでは、仮想マシンにエンドポイント保護をインストールするための セキュリティ センター の推奨事項を実装します。 

1. Azure portal で、**セキュリティ センター** に移動する \| 「**概要**」 ブレード。 

1. 「**セキュリティ センター**」 の \| 「**概要**」 ブレードの 「**ポリシーとコンプライアンス**」 セクションで 、「**全体のセキュア スコア**」 をクリックします。     

    >**注**: 現在のスコアを確認します。

1. 「**セキュリティ センター**」 の \| 「**概要**」 ブレードの 「**リソース セキュリティの検疫**」 セクションで、「**コンピューティング リソースとアプリ リソース**」 をクリックします。    

1. 「**セキュリティ センター**」 の \| 「**計算**」 ブレードで、「**VM およびサーバー**」 タブをクリックしてから、「**myVM**」 エントリをクリックします。    

1. 「**myvm**」 ブレードの 「**推奨事項の一覧**」 セクションにある 「**推奨事項**」 タブで推奨事項を確認し、「**A vulnerability assessment solution should be enabled on your virtual machines（脆弱性評価ソリューションを仮想マシンで有効にする必要がある）**」 エントリをクリックします。 

1. 「**脆弱性評価ソリューションを仮想マシンで有効にする必要がある**」 ブレードで、「**修復**」 をクリックします。   

1. 「**リソースの修復**」 ブレードで、**myVM** が選択したリソースとして表示されていることを確認し、「**1 つのリソースを修復**」 をクリックします。     

    >**注**: ツール バーの 「**通知**」 アイコンをクリックして 「**通知**」 ブレードを表示して、インストールの進行状況を監視します。    

    >**注**:  また、**myVM** 仮想マシンの構成を表示してインストールを確認することもできます。  「**myVM** 仮想マシン」 ブレードの 「**設定**」 セクションで、「**拡張機能**」 をクリックすると、「**myVM」\| 拡張機能**」 ブレードに、**AzurePolicyforWindows** 拡張機能が「**プロビジョニングに成功**」の状態で一覧表示されます。  

    >**注**: セキュリティ センター は、仮想マシンを自動的に再スキャンします。これは、セキュア スコアの増加によって反映されます。

    >**注**: インストールが完了するのを待たず、代わりに次のタスクに進みます。 

#### タスク 3: Just In Time VM アクセスを有効にするために セキュリティ センター の推奨事項を実装する

このタスクでは、仮想マシンでの Just In Time VM アクセスを有効にする セキュリティ センター の推奨事項を実装します。 

1. Azure portal で、**セキュリティ センター** に移動する | 「**概要**」 ブレード。 

1. 「**セキュリティ センター**」 の \| 「**概要**」 ブレードの 「**リソース セキュリティの検疫**」 セクションで 、「**コンピューティングとアプリ**」 をクリックします。    

1. 「**セキュリティ センター**」 の \| 「**コンピューティングとアプリ**」 ブレードで、「**VM とサーバー**」 タブをクリックしてから、「**myVM**」 エントリをクリックします。    

1. 「**myvm**」 ブレードの 「**推奨事項リスト**」 セクションにある 「**推奨事項**」 タブで、「**Management ports of virtual machines should be protected with just-in-time network access control（仮想マシンの管理ポートを Just-In-Time ネットワーク アクセス制御で保護する必要があります）**」 エントリをクリックします。       

1. 「**仮想マシンの管理ポートを Just-In-Time ネットワーク アクセス制御で保護する必要があります**」 ブレードで 、「**修復手順**」 セクションを展開し、手順を確認します。    

1. 「**仮想マシンの管理ポートを Just-In-Time ネットワーク アクセス制御で保護する必要があります**」 ブレードで、「**修復**」 をクリックします。   

1. 「**JIT VM アクセス構成**」 ブレードの、ポート **22** を参照する行の右端で、省略記号ボタンをクリックしてから、「**削除**」 をクリックします。     

1. 「**JIT VM アクセス構成**」 ブレードで、「**保存**」 をクリックします。

    >**注**: ツールバーの 「**通知**」 アイコンをクリックして、「**通知**」 ブレードを表示して、構成の進行状況を監視します。    

    >**注**: このラボでの推奨事項の実装がセキュア スコアに反映されるまでに時間がかかる場合があります。セキュア スコアを定期的にチェックして、これらの機能の実装による影響を判断します。 

> 結果: セキュリティ センター にオンボードし、仮想マシンの推奨事項を実装しています。 

**リソースをクリーン アップします**

>**注**: Azure Sentinel ラボで必要ですので、リソースをこのラボから削除しないでください。
