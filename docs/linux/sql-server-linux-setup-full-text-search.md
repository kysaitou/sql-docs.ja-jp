---
title: Linux 上の SQL Server フルテキスト検索のインストール |Microsoft ドキュメント
description: この記事では、Linux に SQL Server フルテキスト検索をインストールする方法について説明します。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 401eb2569a1da86964543f9122d213398f39eff4
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2018
---
# <a name="install-sql-server-full-text-search-on-linux"></a>Linux 上の SQL Server フルテキスト検索をインストールします。

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

次の手順インストール[SQL Server フルテキスト検索](https://msdn.microsoft.com/library/ms142571.aspx)(**mssql サーバー-fts**) on Linux です。 フルテキスト検索では、SQL Server テーブル内の文字ベースのデータに対してフルテキスト クエリを実行することができます。 このリリースの既知の問題については、次を参照してください。、 [Release Notes](sql-server-linux-release-notes.md)です。

> [!NOTE]
> SQL Server フルテキスト検索を最初にインストールする前に[SQL Server のインストール](sql-server-linux-setup.md#platforms)です。 これにより、キーとリポジトリをインストールするときに使用する構成、 **mssql サーバー-fts**パッケージです。

プラットフォーム用の SQL Server フルテキスト検索をインストールします。

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL をインストールします。</a>

インストールする次のコマンドを使用して、 **mssql サーバー-fts** Red Hat Enterprise Linux にします。 

```bash
sudo yum install -y mssql-server-fts
```

既に存在する場合**mssql サーバー-fts**インストールされている、次のように、次のコマンドで最新バージョンに更新できます。

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

オフラインでインストールする場合は、検索で、フルテキスト検索のパッケージのダウンロード、[リリース ノート](sql-server-linux-release-notes.md)です。 記事で説明されている同じ、オフライン インストール手順に従って[SQL Server のインストール](sql-server-linux-setup.md#offline)です。

## <a name="ubuntu">Ubuntu にインストールします</a>

インストールする次のコマンドを使用して、 **mssql サーバー-fts** Ubuntu でします。 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

既に存在する場合**mssql サーバー-fts**インストールされている、次のように、次のコマンドで最新バージョンに更新できます。

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

オフラインでインストールする場合は、検索で、フルテキスト検索のパッケージのダウンロード、[リリース ノート](sql-server-linux-release-notes.md)です。 記事で説明されている同じ、オフライン インストール手順に従って[SQL Server のインストール](sql-server-linux-setup.md#offline)です。

## <a name="SLES">SLES をインストールします。</a>

インストールする次のコマンドを使用して、 **mssql サーバー-fts** SUSE Linux Enterprise Server にします。 

```bash
sudo zypper install mssql-server-fts
```

既に存在する場合**mssql サーバー-fts**インストールされている、次のように、次のコマンドで最新バージョンに更新できます。

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

オフラインでインストールする場合は、検索で、フルテキスト検索のパッケージのダウンロード、[リリース ノート](sql-server-linux-release-notes.md)です。 記事で説明されている同じ、オフライン インストール手順に従って[SQL Server のインストール](sql-server-linux-setup.md#offline)です。

## <a name="supported-languages"></a>サポートされている言語

フルテキスト検索を使用して[ワード ブレーカー](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)言語に基づいて個々 の単語を識別する方法を決定します。 クエリを実行して登録されているワード ブレーカーの一覧を取得することができます、 **sys.fulltext_languages**カタログ ビューです。 次の言語のワード ブレーカーは、SQL Server 2017 とともにインストールされます。

| 言語 | 言語 ID |
|---|---|
| ニュートラル | 0 |
| アラビア語 | 1025 |
| ベンガル語 (インド) | 1093 |
| ブークモール | 1044 |
| ブラジル | 1046 |
| 英語 (U.K.) | 2057 |
| ブルガリア語 | 1026 |
| カタロニア語 | 1027 |
| 中国語 (中華人民共和国香港特別行政区) | 3076 |
| 中国語 (中華人民共和国マカオ特別行政区) | 5124 |
| 中国語 (シンガポール) | 4100 |
| クロアチア語 | 1050 |
| チェコ語 | 1029 |
| デンマーク語 | 1030 |
| オランダ語 | 1043 |
| 英語 | 1033 |
| フランス語 | 1036 |
| ドイツ語 | 1031 |
| ギリシャ語 | 1032 |
| グジャラート語 | 1095 |
| ヘブライ語 | 1037 |
| ヒンディー語 | 1081 |
| アイスランド語 | 1039 |
| インドネシア語 | 1057 |
| イタリア語 | 1040 |
| 日本語 | 1041 |
| カンナダ語 | 1099 |
| 韓国語 | 1042 |
| ラトビア語 | 1062 |
| リトアニア語 | 1063 |
| マレー語 - マレーシア | 1086 |
| マラヤーラム語 | 1100 |
| マラーティー語 | 1102 |
| ポーランド語 | 1045 |
| ポルトガル語 | 2070 |
| パンジャーブ語 | 1094 |
| ルーマニア語 | 1048 |
| ロシア語 | 1049 |
| セルビア語 (キリル) | 3098 |
| セルビア語 (ラテン) | 2074 |
| 簡体字中国語 | 2052 |
| スロバキア語 | 1051 |
| スロベニア語 | 1060 |
| スペイン語 | 3082 |
| スウェーデン語 | 1053 |
| タミール語 | 1097 |
| テルグ語 | 1098 |
| タイ語 | 1054 |
| 繁体字中国語 | 1028 |
| トルコ語 | 1055 |
| ウクライナ語 | 1058 |
| ウルドゥ語 | 1056 |
| ベトナム語 | 1066 |

## <a id="filters"></a> フィルター

フルテキスト検索は、バイナリ ファイルに格納されているテキストのでも動作します。 必須でここでは、インストールされているフィルターは、ファイルを処理します。 フィルターの詳細については、次を参照してください。[検索用フィルターの管理と構成](../relational-databases/search/configure-and-manage-filters-for-search.md)です。

呼び出すことによってインストールされているフィルターの一覧を表示できる**sp_help_fulltext_system_components 'filter'** です。 SQL Server 2017 年 1、次のフィルターがインストールされます。

| [コンポーネント名] | クラス ID | バージョン |
|---|---|---|
|.a | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ans | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.asc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asm | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.asp | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bas | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.bat | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cls | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cmd | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.csa | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.css | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.csv | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dbs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.def | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dic | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.dos | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.faq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hhc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.hta | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.html | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.i | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ics | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.idq | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.ini | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.inx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.jav | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.kci | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgn | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.mak | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odc | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.odl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgdef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.prc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rc2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.reg | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rgs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rtf | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.rul | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.scc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.shtml | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sol | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.stm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.tab | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tdl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tlh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.tli | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.trg | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.txt | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.udf | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.udt | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.url | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vbs | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>セマンティック検索
[セマンティック検索](../relational-databases/search/semantic-search-sql-server.md)を抽出し、統計的に関連するインデックス、フルテキスト検索機能を上に構築*キー フレーズ*です。 これにより、データベース内のドキュメント内で意味を照会することができます。 ようなドキュメントを識別することもできます。

セマンティック検索を使用するのには、最初のコンピューターに、セマンティック言語統計データベースを復元する必要があります。

1. などのツールを使用[sqlcmd](sql-server-linux-setup-tools.md)Linux の SQL Server インスタンスで、次の TRANSACT-SQL コマンドを実行します。 このコマンドは、言語統計データベースを復元します。

   ```sql
   RESTORE DATABASE [semanticsdb] FROM
   DISK = N'/opt/mssql/misc/semanticsdb.bak' WITH FILE = 1,
   MOVE N'semanticsdb' TO N'/var/opt/mssql/data/semanticsDB.mdf',
   MOVE N'semanticsdb_log' TO N'/var/opt/mssql/data/semanticsdb_log.ldf', NOUNLOAD, STATS = 5
   GO
   ```

   > [!NOTE]
   > 必要に応じて、前の RESTORE コマンドには、構成を調整するパスを更新します。

1. セマンティック言語統計データベースを登録する次の TRANSACT-SQL コマンドを実行します。

    ```sql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO
    ```

## <a name="next-steps"></a>次の手順

について、フルテキスト検索は、次を参照してください。 [SQL Server フルテキスト検索](../relational-databases/search/full-text-search.md)です。 
