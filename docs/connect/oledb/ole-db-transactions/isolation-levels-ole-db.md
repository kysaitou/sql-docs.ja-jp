---
title: 分離レベル (OLE DB) |Microsoft ドキュメント
description: 分離レベル (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 55cc5c0db959ce21a5a4b3ae60d83c2f42a56a09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="isolation-levels-ole-db"></a>分離レベル (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアントは、接続のトランザクション分離レベルを制御できます。 トランザクション分離レベルを制御するには、OLE DB Driver for SQL Server コンシューマーが使用します。  
  
-   DBPROPSET_SESSION プロパティの DBPROP_SESS_AUTOCOMMITISOLEVELS、OLE DB driver for SQL Server の既定の自動コミット モードです。  
  
     SQL Server の既定のレベルの OLE DB Driver は、DBPROPVAL_TI_READCOMMITTED です。  
  
-   *IsoLevel*のパラメーター、 **itransactionlocal::starttransaction**手動コミット トランザクションのローカルのメソッドです。  
  
-   *IsoLevel*のパラメーター、 **itransactiondispenser::begintransaction**メソッドの MS DTC によってコーディネートされる分散トランザクションです。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、ダーティ リード分離レベルでの読み取り専用アクセスを許可します。 他のすべてのレベルでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクトにロックをかけることによって同時実行を制限します。 クライアントがより高度な同時実行レベルを要求すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はデータへの同時アクセスに対してより厳密な制限を適用します。 最高レベルのデータへの同時アクセスを維持するために、OLE DB Driver for SQL Server コンシューマーは、特定の同時実行レベルの要求を適切に制御する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ではスナップショット分離レベルが導入されました。 詳細については、次を参照してください。[スナップショット分離を使用した作業](../../oledb/features/working-with-snapshot-isolation.md)です。  
  
## <a name="see-also"></a>参照  
 [トランザクション](../../oledb/ole-db-transactions/transactions.md)  
  
  
