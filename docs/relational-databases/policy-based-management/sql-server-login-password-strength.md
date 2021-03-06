---
title: SQL Server ログイン パスワードの強度 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3859064d9c724b0174af0f228608c4235b1bf124
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32952897"
---
# <a name="sql-server-login-password-strength"></a>SQL Server ログイン パスワードの強度
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このルールでは、各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの [パスワード ポリシーを適用する] が有効になっているかどうかを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が有効で、オペレーティング システムが [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]よりも前のバージョンである場合、攻撃者は既知の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン パスワードを繰り返し利用できます。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 オペレーティング システムを [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]にアップグレードすることをお勧めします。  
  
 使用している環境で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が必要ではない場合は、Windows 認証を使用します。  
  
 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対して、[パスワード ポリシーを適用する] を有効にします。 [ログインのパスワード ポリシーを構成するには、](../../t-sql/statements/alter-login-transact-sql.md) ALTER LOGIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用します。  
  
## <a name="for-more-information"></a>詳細情報  
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
