---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6db18eb8805eef626a72332bf6190c39fda97981
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|10001|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|HR_E_UNEXPECTED|  
|メッセージ テキスト|プロバイダーが予期しない重大なエラーをレポートしました。|  
  
## <a name="explanation"></a>説明  
分散クエリ処理で、OLE DB プロバイダーを呼び出すときに一般的なエラーが発生しました。  
  
## <a name="user-action"></a>ユーザーの操作  
[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して OLE DB トレース イベントを収集し、このデータを OLE DB プロバイダーの製品サポートに提供します。  
  
## <a name="see-also"></a>参照  
[SQL Server プロファイラーのテンプレートと権限](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
