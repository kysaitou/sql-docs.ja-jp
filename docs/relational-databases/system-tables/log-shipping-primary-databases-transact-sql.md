---
title: log_shipping_primary_databases (TRANSACT-SQL) |Microsoft ドキュメント
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_primary_databases
- log_shipping_primary_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_primary_databases system table
ms.assetid: 56888756-a798-42be-9b5e-0f9aa05a2cc6
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 233f883e4c714fb7c8eead62e885dabfb5f0167c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262456"
---
# <a name="logshippingprimarydatabases-transact-sql"></a>log_shipping_primary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ配布構成内のプライマリ データベースに対して 1 つのレコードを格納します。 次の表は、 **msdb**データベース。  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|ログ配布構成におけるプライマリ データベースの ID。|  
|**primary_database**|**sysname**|ログ配布構成におけるプライマリ データベースの名前。|  
|**backup_directory**|**nvarchar(500)**|プライマリ サーバーのトランザクション ログ バックアップ ファイルが格納されているディレクトリ。|  
|**backup_share**|**nvarchar(500)**|バックアップ ディレクトリへのネットワーク パスまたは UNC パス。|  
|**backup_retention_period**|**int**|バックアップ ディレクトリでログ バックアップ ファイルが保持される時間 (分単位)。この時間を過ぎるとファイルは削除されます。|  
|**backup_job_id**|**uniqueidentifier**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]プライマリ サーバー上のバックアップ ジョブに関連付けられているエージェントのジョブ ID。|  
|**monitor_server**|**sysname**|インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成で監視サーバーとして使用されています。|  
|**monitor_server_security_mode**|**bit**|監視サーバーへの接続に使用されるセキュリティ モード。<br /><br /> 1 = Windows 認証です。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**last_backup_file**|**nvarchar(500)**|最新のトランザクション ログ バックアップの絶対パス。|  
|**last_backup_date**|**datetime**|最後のログ バックアップ操作の日時。|  
|**user_specified_monitor**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **sp_help_log_shipping_primary_database**と**sp_help_log_shipping_secondary_primary**でモニターの設定の表示を制御するこの列を使用して[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]です。<br /><br /> 0 = ユーザーが明示的な値を指定しなかったこれら 2 つのストアド プロシージャのいずれかを呼び出すときに、 **@monitor_server**パラメーター。<br /><br /> 1 = ユーザーが明示的な値を指定しました。|  
|**backup_compression**|**tinyint**|ログ配布構成でサーバー レベルのバックアップの圧縮動作を上書きするかどうかを指定します。<br /><br /> 0 = 無効。 サーバーで構成されたバックアップ圧縮設定に関係なく、ログ バックアップは圧縮されません。<br /><br /> 1 = 有効にします。 サーバーで構成されたバックアップ圧縮設定に関係なく、ログ バックアップは常に圧縮されます。<br /><br /> 2 = のサーバーの構成を使用して、[表示または backup compression default サーバー構成オプションを構成する](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)サーバー構成オプション。 これが既定値です。<br /><br /> バックアップの圧縮は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Enterprise エディションでのみサポートされています。|  
  
## <a name="see-also"></a>参照  
 [ログ配布 & #40; についてSQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
