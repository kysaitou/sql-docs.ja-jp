---
title: SQL Server が可用性グループを強制的にフェールオーバーする
description: クラスターの種類が NONE の可用性グループの強制フェールオーバーを実行する
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: f5655e73481d830c848aea34c4a4f49613be0913
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
プライマリ レプリカは AG ごとに 1 つだけです。 プライマリ レプリカは読み書きができます。 プライマリになっているレプリカの変更は、フェールオーバーで行うことができます。 高可用性の AG では、クラスター マネージャーによってフェールオーバー プロセスが自動化されます。 クラスターの種類が NONE の AG では、フェールオーバー プロセスは手動です。 

クラスターの種類が NONE の AG でプライマリ レプリカをフェールオーバーするには、2 つの方法があります。

- データ損失のある強制的な手動フェールオーバー
- データ損失のない手動フェールオーバー

### <a name="forced-manual-failover-with-data-loss"></a>データ損失のある強制的な手動フェールオーバー

プライマリ レプリカを使うことができず、復旧できない場合は、この方法を使います。 

データ損失のあるフェールオーバーを強制的に行うには、ターゲット セカンダリ レプリカをホストしている SQL Server インスタンスに接続して、以下を実行します。

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>データ損失のない手動フェールオーバー

プライマリ レプリカを使うことができても、一時的または完全に構成を変更し、プライマリ レプリカをホストする SQL Server インスタンスを変更する必要がある場合は、この方法を使います。 手動フェールオーバーを実行する前に、データ損失の可能性がないように、ターゲット セカンダリ レプリカが最新の状態であることを確認します。 

データ損失のない手動フェールオーバーを行うには:

1. ターゲット セカンダリ レプリカを `SYNCHRONOUS_COMMIT` にします。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 次のクエリを実行して、アクティブなトランザクションが、プライマリ レプリカと少なくとも 1 つの同期セカンダリ レプリカにコミットされていることを確認します。 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   `synchronization_state_desc` が `SYNCHRONIZED` の場合、セカンダリ レプリカは同期されています。

3. `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` を 1 に更新します。

   次のスクリプトは、`ag1` という名前の AG で `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` を 1 に設定します。 次のスクリプトを実行する前に、`ag1` を実際の AG の名前に置き換えます。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   この設定により、すべてのアクティブなトランザクションが、プライマリ レプリカと少なくとも 1 つの同期セカンダリ レプリカにコミットされます。 

4. プライマリ レプリカをセカンダリ レプリカに降格させます。 降格された後のプライマリ レプリカは読み取り専用になります。 プライマリ レプリカをホストしている SQL Server インスタンスで次のコマンドを実行して、ロールを `SECONDARY` に更新します。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. ターゲット セカンダリ レプリカをプライマリに昇格させます。 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > AG を削除するには、[DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql) を使います。 クラスターの種類が NONE または EXTERNAL で作成された AG では、AG に含まれるすべてのレプリカでコマンドを実行する必要があります。