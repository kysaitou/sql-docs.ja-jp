---
title: Reporting Services のログ ファイルとソース | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
caps.latest.revision: 49
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8d2bbaf2046f8cf62264005e787938a8d61fee6a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025689"
---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services のログ ファイルとソース
  レポート サーバーおよびレポート サーバー環境では、サーバーの操作および状態に関する情報を記録するために、さまざまなログの保存先が使用されます。 ログ記録には、実行のログ記録とトレースのログ記録という 2 つの基本的なカテゴリがあります。 実行のログ記録には、レポート実行統計、監査、パフォーマンスの診断、および最適化に関する情報が含まれます。 トレースのログ記録は、エラー メッセージおよび一般的な診断に関する情報です。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード  
  
 次の表に、ログの場所やログの内容を表示する方法を含む、各ログに関する追加情報へのリンクを示します。  
  
|Log|Description|  
|---------|-----------------|  
|[レポート サーバー ExecutionLog と ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)|実行ログは、レポート サーバー データベースに格納されている SQL Server のビューです。<br /><br /> レポート サーバー実行ログには、レポートが実行された日時、実行したユーザー、レポートの配信先、使用された表示形式など、特定のレポートに関するデータが含まれます。|  
|SharePoint トレース ログ|SharePoint で実行されているレポート サーバーの SharePoint トレース ログには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の情報が含まれています。 SharePoint 統合ログ サービスに対して [!INCLUDE[ssRS](../../includes/ssrs-md.md)] 固有の情報を構成することもできます。 詳細については、「 [SharePoint トレース ログの Reporting Services イベントをオンにする (ULS)](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[レポート サーバー サービスのトレース ログ](../../reporting-services/report-server/report-server-service-trace-log.md)|サービスのトレース ログには、アプリケーションのデバッグまたは問題やイベントの調査を行う場合に役立つ詳細情報が含まれます。 トレース ログ ファイルは ReportServerService_\<timestamp>.log であり、次のフォルダーにあります。<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`|  
|[レポート サーバーの HTTP ログ](../../reporting-services/report-server/report-server-http-log.md)|HTTP ログ ファイルには、レポート サーバー Web サービスおよびレポート マネージャーによって処理された HTTP 要求および HTTP 応答がすべて記録されます。|  
|[Windows アプリケーション ログ](../../reporting-services/report-server/windows-application-log.md)|Microsoft Windows アプリケーション ログには、レポート サーバーのイベントに関する情報が含まれます。|  
|Windows パフォーマンス ログ|Windows パフォーマンス ログには、レポート サーバーのパフォーマンス データが含まれます。 パフォーマンス ログを作成してから、収集するデータを決定するカウンターを選択できます。 詳細については、「 [レポート サーバーのパフォーマンスの監視](../../reporting-services/report-server/monitoring-report-server-performance.md)」を参照してください。|  
|SQL Server セットアップ ログ ファイル|ログ ファイルはセットアップ中にも作成されます。 セットアップに失敗または成功した際に警告メッセージや他のメッセージが表示された場合、ログ ファイルを検証して問題のトラブルシューティングを行うことができます。 詳細については、「 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)」を参照してください。|  
|IIS ログ|Microsoft インターネット インフォメーション サービス (IIS) によって作成されたログ ファイル。 詳細については、「[インターネット インフォメーション サービス (IIS) のログ記録を有効にする方法](http://support.microsoft.com/kb/313437)」(http://support.microsoft.com/kb/313437) を参照してください。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services レポート サーバー &#40;ネイティブ モード&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [エラーとイベントのリファレンス (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
