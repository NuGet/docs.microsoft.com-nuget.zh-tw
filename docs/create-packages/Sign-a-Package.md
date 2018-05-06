---
title: 簽署 NuGet 套件
description: 說明已簽署套件如何用於啟用內容完整性驗證。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a>簽署 NuGet 套件

簽署套件是可確保套件自建立後未曾受到修改的程序。

## <a name="prerequisites"></a>必要條件

1. 要簽署的套件 (`.nupkg` 檔案)。 請參閱[建立套件](creating-a-package.md)。

1. nuget.exe 4.6.0 或更新版本。 請參閱如何[安裝 NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)。

1. [程式碼簽署憑證](../reference/signed-packages-reference.md#get-a-code-signing-certificate)。

> [!Warning]
> nuget.org 目前不接受簽署的套件。 您可以簽署套件以發佈至自訂摘要。

## <a name="sign-a-package"></a>簽署套件

若要簽署套件，請使用 [nuget sign](../tools/cli-ref-sign.md)：

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

如命令參考所述，您可以使用憑證存放區中可用的憑證，或使用檔案中的憑證。

### <a name="common-problems-when-signing-a-package"></a>簽署套件時的常見問題

- 此憑證對於程式碼簽署無效。 您必須確認指定的憑證具有適當的增強金鑰使用方法 (EKU 1.3.6.1.5.5.7.3.3)。
- 憑證不符合基本需求，例如 RSA SHA-256 簽章演算法，或 2048 或更高位元的公開金鑰。
- 憑證已過期或已撤銷。
- 時間戳記伺服器不符合憑證需求。

> [!Note]
> 簽署的套件應包含時間戳記，以確定簽署憑證過期時，簽章仍保持有效。 簽署不含時間戳記時，簽署作業會產生 [NU3002 警告](../reference/Errors-and-Warnings.md#nu3002)。

## <a name="verify-a-signed-package"></a>驗證簽署的套件

使用 [nuget verify](../tools/cli-ref-verify.md)以查看特定套件的簽章詳細資料：

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>安裝簽署的套件

簽署的套件不需要安裝任何特定動作；不過，如果內容在簽署後已經過修改，就會封鎖安裝並產生 [NU3008 錯誤](../reference/Errors-and-Warnings.md#nu3008)。

> [!Warning]
> 以不受信任的憑證簽署的套件，會視為未簽署，安裝時會如同其他未簽署的套件一樣不含任何警告或錯誤。

## <a name="see-also"></a>另請參閱

[簽署的套件參考](../reference/Signed-Packages-Reference.md)
