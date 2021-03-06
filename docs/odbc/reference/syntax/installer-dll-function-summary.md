---
title: インストーラー DLL 関数の概要 |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 685a0533aae91d790b48b788498aebbcb171fa93
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917389"
---
# <a name="installer-dll-function-summary"></a>インストーラー DLL 関数の概要
次の表では、インストーラー DLL 内の関数について説明します。 各関数のセマンティクスと構文に関する詳細については、次を参照してください。[インストーラー DLL の API リファレンス](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)です。  
  
|タスク|関数名|用途|  
|----------|-------------------|-------------|  
|ODBC のインストール|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|ドライバー固有のセットアップ DLL を読み込みます。|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|インストールされているドライバーの一覧を返します。|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|システム情報に、ドライバーを追加します。|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|ドライバー マネージャーのターゲット ディレクトリを返します。|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|関数のインストーラーのエラー状態や状態の情報を返します。|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|システム情報を変換プログラムを追加します。|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|エラーを報告するドライバーまたは変換プログラムのセットアップ ライブラリを使用できます。|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|システム情報からドライバーを削除します。|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|システム情報から ODBC コア コンポーネントを削除します。|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|システム情報の変換プログラムを削除します。|  
|データ ソースの構成|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|ドライバー固有のセットアップ DLL を呼び出します。|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|データ ソースに追加 ダイアログ ボックスが表示されます。|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|DSN の値を一覧表示する Odbc.ini エントリがシステム情報の場所を示す構成モードを取得します。|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|値は、システム情報を書き込みます。|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|翻訳者を選択するダイアログ ボックスが表示されます。|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|データ ソースとドライバーを構成するダイアログ ボックスが表示されます。|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|ファイル Dsn から情報を読み取ります。|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|既定のデータ ソースを削除します。|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|データ ソースを削除します。|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|DSN の値を一覧表示する Odbc.ini エントリがシステム情報の場所を示す構成モードを設定します。|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|長さとデータ ソース名の有効性を確認します。|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|データ ソースを追加します。|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|ファイル Dsn に情報を書き込みます。|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|システム情報の値を取得します。|
