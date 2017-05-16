---
title: "レプリケーション エージェント実行可能ファイルの概念 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 096156484b2378713485e1177eb9b0cfd6faa5d8
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-executables-concepts"></a>レプリケーション エージェント実行可能ファイルの概念
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケーション エージェントは、次のような方法でプログラムから制御できます。  
  
-   <xref:Microsoft.SqlServer.Replication> 名前空間で管理対象のエージェントのプログラミング インターフェイスを使用する。  
  
-   エージェントの実行可能ファイルを一連のパラメーターを指定してコマンド プロンプトから呼び出す。  
  
 レプリケーション エージェントはコマンド プロンプトから直接呼び出すことができるため、コマンド ライン スクリプトをバッチ ファイル化することで、プログラムからエージェントにアクセスできます。 エージェントをコマンド プロンプトから呼び出した場合、そのエージェントは、エージェントを呼び出したユーザーまたはバッチ ファイルを実行したユーザーの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows セキュリティ アカウント下で実行されます。  
  
 次のレプリケーション エージェントのインスタンスは、実行可能ファイルを使用して実行できます。  
  
-   [レプリケーション ディストリビューション エージェント](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [レプリケーション ログ リーダー エージェント](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [レプリケーション マージ エージェント](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [レプリケーション キュー リーダー エージェント](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
-   [レプリケーション スナップショット エージェント](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
 レプリケーション エージェントを呼び出す際、パフォーマンス プロファイルを使用することで、あらかじめ定義された一連のパラメーターを自動的にエージェント実行可能ファイルに渡すことができます。 詳しくは、「 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 次の例は、レプリケーション エージェントをコマンド プロンプトから呼び出す方法を示しています。 レプリケーション エージェントは、レプリケーション管理オブジェクト (RMO) を使用して呼び出すこともできます。 詳細については、「[サブスクリプションの同期 &#40;レプリケーション&#41;](../../../relational-databases/replication/synchronize-subscriptions-replication.md)」を参照してください。  
  
> [!NOTE]  
>  これらの例では、読みやすくするために、改行が追加されています。 バッチ ファイルの場合、コマンドは 1 行で入力する必要があります。  
  
### <a name="running-the-snapshot-agent"></a>スナップショット エージェントの実行  
 次の例では、バッチ ファイルを使って、スナップショット エージェントをコマンド プロンプトから呼び出し、**AdvWorksSalesOrdersMerge** パブリケーションのスナップショットを生成しています。 (以下のスクリプトでは、[!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] ファイル (バージョン 130) へのパスを使用しています)。 スクリプトを調整し、使用しているバージョンの [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] のファイルを指すようにする必要があります。)  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\130\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>ディストリビューション エージェントの実行  
 この例では、バッチ ファイルを使って、ディストリビューション エージェントをコマンド プロンプトから呼び出し、**AdvWorksProductTran** パブリケーションからの変更を、プッシュ サブスクライバーに連続してレプリケートしています。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>マージ エージェントの実行  
 この例では、バッチ ファイルを使って、マージ エージェントをコマンド プロンプトから呼び出し、**AdvWorksSalesOrdersMerge** パブリケーションにプル サブスクリプションを同期しています。  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\130\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  