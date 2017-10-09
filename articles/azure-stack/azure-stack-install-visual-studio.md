---
title: "aaaInstall Visual Studio y conéctese tooAzure pila | Documentos de Microsoft"
description: "Obtenga información acerca de los pasos de hello necesarios tooinstall Visual Studio y conéctese tooAzure pila"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: aa63f9eaf5cd72a0b2f31256c2df99fb41ca11fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-connect-tooazure-stack"></a>Instalar Visual Studio y conéctese tooAzure pila

Usar Visual Studio tooauthor e implementar Azure Resource Manager [plantillas](azure-stack-arm-templates.md) en pila de Azure. Puede utilizar pasos de hello descritos en este tooinstall artículo Visual Studio o desde [Kit de desarrollo de Azure pila](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está conectado a través de [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn). Estos pasos crean una nueva instalación de Visual Studio 2015 Community Edition. Obtenga más información sobre la [coexistencia](https://msdn.microsoft.com/library/ms246609.aspx) de otras versiones de Visual Studio.

## <a name="install-visual-studio"></a>Instalación de Visual Studio
1. Descargue y ejecute hello [instalador de plataforma Web](https://www.microsoft.com/web/downloads/platform.aspx).             
2. Busque **Visual Studio Community 2015 with Microsoft Azure SDK - 2.9.6**, haga clic en **Agregar** e **Instalar**.

    ![Captura de pantalla de los pasos de la instalación de WebPI](./media/azure-stack-install-visual-studio/image1.png) 

3. Desinstalar hello **Microsoft Azure PowerShell** que se instala como parte del programa Hola a Azure SDK.

    ![Captura de pantalla de la interfaz de agregar o quitar programas para Azure PowerShell](./media/azure-stack-install-visual-studio/image2.png) 

4. [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Instalación de PowerShell para Azure Stack)

5. Reinicie el sistema de operativo de hello al finalizar la instalación de Hola.

## <a name="connect-tooazure-stack"></a>Conectar tooAzure pila

1. Inicie Visual Studio.

2. De hello **vista** menú, seleccione **nube explorador**.

3. En el nuevo panel de hello, seleccione **Agregar cuenta** e inicie sesión con sus credenciales de Azure Active Directory.  
    ![Captura de pantalla del explorador de la nube una vez iniciado la sesión y conectado tooAzure pila](./media/azure-stack-install-visual-studio/image6.png)

Una vez iniciada la sesión, puede [implementar plantillas](azure-stack-deploy-template-visual-studio.md) o examinar los tipos de recursos disponibles y grupos de recursos toocreate sus propias plantillas.  

## <a name="next-steps"></a>Pasos siguientes

 - [Desarrollo de plantillas para Azure Stack](azure-stack-develop-templates.md)
