---
title: "aaaSet seguridad PowerShell toocreate una máquina virtual para hello Marketplace | Documentos de Microsoft"
description: "Instrucciones para configurar Azure PowerShell y lo usa como un proceso opcional de flujo de toocreate toodeploy de imágenes de máquina virtual y venden en, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Configurar Azure PowerShell toocreate una oferta de hello Azure Marketplace
Para obtener información detallada acerca de cómo tooset PowerShell de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Un enfoque sencillo es toouse Hola certificado (método), que descarga e importa un certificado necesario para la autenticación. Hola tooobtain necesita certificados, usar hello **Get-AzurePublishSettingsFile** cmdlet. Guarde el archivo hello cuando se le pida. certificado de hello tooimport en una sesión de PowerShell, use hello **importación-AzurePublishSettingsFile** cmdlet.

tooconfigure y almacén Hola comunes Microsoft Azure suscripción de sesión de PowerShell de hello, utilice hello **Set-AzureSubscription** y **Select-AzureSubscription** cmdlets:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

primer comando de Hello asocia una cuenta de almacenamiento predeterminada con suscripción de hello (necesario para algunas operaciones de aprovisionamiento de VM).  en segundo lugar, Hola hace suscripción Hola Hola uno actual (reconocido por otros cmdlets).

## <a name="see-also"></a>Otras referencias
* [Introducción: cómo toopublish una toohello de oferta de Azure Marketplace](marketplace-publishing-getting-started.md)
* [Crear una imagen de máquina virtual para hello Marketplace](marketplace-publishing-vm-image-creation.md)

