---
title: Integration Services のテーブル (TRANSACT-SQL) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Integration Services system tables
- system tables [SQL Server], Integration Services
- system tables [Integration Services]
- SSIS, system tables
ms.assetid: 683b181b-0091-4a9c-86db-bc577af43cec
caps.latest.revision: 21
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fc5df46211b3de92b054fea4120d9b7c884a0ccb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259622"
---
# <a name="integration-services-tables-transact-sql"></a>Integration Services のテーブル (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用される情報を格納する、msdb データベースのシステム テーブルについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [sysssislog](../../relational-databases/system-tables/sysssislog-transact-sql.md)  
 ログ エントリごとに 1 行が含まれていますに[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]パッケージが実行時に生成されます。  
  
 このテーブルは、パッケージで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ プロバイダーが使用されている場合にのみ使用されます。  
  
 [sysssispackagefolders](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)  
 論理フォルダーごとに 1 つの行データを格納する、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]パッケージを整理するサービスで使用します。 列の値では、入れ子になったフォルダー間の親子リレーションシップが定義されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] サービスに接続した場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の階層ビューに、格納されているパッケージが表示されます。  
  
 [sysssispackages](../../relational-databases/system-tables/sysssispackages-transact-sql.md)  
 ごとに 1 つの行を含む[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]パッケージです。  
  
 パッケージを格納する場合にのみ、このテーブルが使用される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。  
  
  
