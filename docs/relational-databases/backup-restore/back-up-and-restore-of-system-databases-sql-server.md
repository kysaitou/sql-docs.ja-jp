---
title: システム データベースのバックアップと復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
caps.latest.revision: 57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cdf3056f71609a33910a6c4812127fc78861be5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921937"
---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>システム データベースのバックアップと復元 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、システムレベルのデータベースのセットである*システム データベース*が管理されています。これらのデータベースは、サーバー インスタンスの運用に不可欠です。 いくつかのシステム データベースは、重大な更新が行われるたびにバックアップする必要があります。 常にバックアップする必要があるシステム データベースには、 **msdb**、 **master**、および **model**があります。 サーバー インスタンス上のいずれかのデータベースでレプリケーションが使用されている場合は、 **distribution** システム データベースもバックアップする必要があります。 これらのシステム データベースをバックアップすることで、ハード ディスク障害などのシステム障害時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムの復元と復旧を行うことができます。  
  
 次の表に、すべてのシステム データベースの概要を示します。  
  
|システム データベース|Description|バックアップの必要性|復旧モデル|コメント|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[master](../../relational-databases/databases/master-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムに関するシステム レベルのすべての情報を記録するデータベース。|はい|Simple|**master** は、ビジネス ニーズを満たすのに十分なデータ保護を行うために必要な頻度でバックアップします。 定期的なバックアップ スケジュールの設定をお勧めします。大量の更新の後で追加のバックアップを行ってこれを補完することもできます。|  
|[model](../../relational-databases/databases/model-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上に作成されるすべてのデータベースのテンプレート。|はい|ユーザーが構成可能*|**model** は、データベース オプションをカスタマイズした直後など、ビジネス ニーズに応じて必要な場合のみバックアップします。<br /><br /> **ベスト プラクティス:** **model**については、必要なときにデータベースの完全バックアップのみを作成することをお勧めします。 **model** はサイズが小さく、変更頻度が低いため、ログのバックアップは必要ありません。|  
|[msdb](../../relational-databases/databases/msdb-database.md)|警告やジョブのスケジュール設定とオペレーターの記録のために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって使用されるデータベース。 **msdb** には、バックアップと復元の履歴テーブルなどの履歴テーブルも含まれます。|はい|単純 (既定)|**msdb** は更新するたびにバックアップします。|  
|[Resource](../../relational-databases/databases/resource-database.md) (RDB)|に付属するすべてのシステム オブジェクトのコピーを含んだ読み取り専用のデータベース。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|いいえ|—|**Resource** データベースにはコードのみが含まれ、mssqlsystemresource.mdf ファイル内に存在します。 そのため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **Resource** データベースをバックアップできません。<br /><br /> 注: mssqlsystemresource.mdf ファイルに対してファイル ベースまたはディスク ベースのバックアップを実行するには、このファイルをデータベース ファイルではなくバイナリ (.exe) ファイルとして扱います。 ただし、これらのバックアップでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の復元を使用できません。 mssqlsystemresource.mdf のバックアップ コピーの復元は手動でのみ実行できます。また、現在の **Resource** データベースを古いバージョンや安全でない可能性のあるバージョンで上書きしないように注意する必要があります。|  
|[tempdb](../../relational-databases/databases/tempdb-database.md)|一時的な結果セットや生成途中の結果セットを保存するためのワークスペース。 このデータベースは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを起動するたびに作成し直されます。 サーバー インスタンスをシャットダウンするとき、 **tempdb** 内のすべてのデータは完全に削除されます。|いいえ|Simple|**tempdb** システム データベースはバックアップできません。|  
|[[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)|サーバーをレプリケーション ディストリビューターとして構成している場合に限り存在するデータベース。 あらゆる種類のレプリケーションのメタデータや履歴、およびトランザクション レプリケーションのトランザクションが保存されます。|はい|Simple|**distribution** データベースをバックアップするタイミングの詳細については、「[レプリケートされたデータベースのバックアップと復元](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)」を参照してください。|  
  
 *model の現在の復旧モデルを確認する方法については、「[データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)」または「[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」を参照してください。  
  
## <a name="limitations-on-restoring-system-databases"></a>システム データベースの復元に関する制限  
  
-   システム データベースは、サーバー インスタンスが現在実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンで作成されたバックアップからのみ復元できます。 たとえば、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 で実行されているサーバー インスタンス上でシステム データベースを復元するには、サーバー インスタンスが [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 にアップグレードされた後に作成されたデータベース バックアップを使用する必要があります。  
  
-   データベースを復元するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行している必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを起動するには、 **master** データベースにアクセスでき、かつ少なくとも一部は使用できる必要があります。 **master** が使用できない状態になった場合、このデータベースを次のいずれかの方法で使用できる状態に戻すことができます。  
  
    -   現在のデータベース バックアップから **master** を復元します。  
  
         サーバー インスタンスを起動できる場合は、データベースの完全バックアップから **master** を復元できます。  
  
    -   **master** を完全に再構築します。  
  
         **master** に深刻な破損があり、それが原因で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を起動できない場合、 **master**を再構築する必要があります。 詳細については、「 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)」を参照してください。  
  
        > [!IMPORTANT]  
        >  **master** を再構築すると、すべてのシステム データベースが再構築されます。  
  
-   状況によっては、モデル データベースを復旧する問題は、システム データベースの再構築、あるいはモデル データベースの mdf ファイルや ldf ファイルの置き換えが必要な場合があります。 詳細については、「 [システム データベースの再構築](../../relational-databases/databases/rebuild-system-databases.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [master データベースの復元 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  
  
-   [データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [システム データベースの移動](../../relational-databases/databases/move-system-databases.md)  
  
## <a name="see-also"></a>参照  
 [ディストリビューション データベース](../../relational-databases/replication/distribution-database.md)   
 [master データベース](../../relational-databases/databases/master-database.md)   
 [msdb データベース](../../relational-databases/databases/msdb-database.md)   
 [model データベース](../../relational-databases/databases/model-database.md)   
 [Resource データベース](../../relational-databases/databases/resource-database.md)   
 [tempdb データベース](../../relational-databases/databases/tempdb-database.md)  
  
  
