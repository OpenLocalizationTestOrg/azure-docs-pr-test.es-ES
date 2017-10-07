---
title: nubes privadas de Azure aaaAccessing con Visual Studio | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooaccess privada recursos de la nube con Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Acceso a nubes privadas de Azure con Visual Studio
De forma predeterminada, Visual Studio admite extremos REST de nube pública de Azure. En este tema, aprenderá cómo toouse la nube privada del certificado tooaccess - e interactúan: hello en la nube privada desde Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess privada de Azure en la nube en Visual Studio
1. Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885) de nube privada de hello, descargue el archivo de configuración de publicación o póngase en contacto con el administrador para un archivo de configuración de la publicación. En la versión pública de Hola de Azure, Hola toodownload de vínculo es [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (archivo descargado Hola debe tener una extensión de `.publishsettings`)

1. Abra Visual Studio.

1. En **Explorador de servidores**, contextual hello **Azure** nodo y, en el menú contextual de hello, seleccione **administrar y filtrar suscripciones**.
   
    ![Comando Administrar suscripciones](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Hola **administrar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione hello **certificados** pestaña y, a continuación, seleccione **importación**.
   
    ![Importación de certificados de Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Hola **Importar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione **examinar**.

    ![Botón del cuadro de diálogo de importación suscripciones de Microsoft Azure Hola examinar](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Hola **abiertos** cuadro de diálogo, examinar toohello directorio donde se Hola guardado archivo publish-settings, seleccione Hola archivo y, a continuación, seleccione **abiertos**.

    ![Seleccione el archivo de configuración de publicación de hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Cuando se devuelve toohello **Importar suscripciones de Microsoft Azure** cuadro de diálogo, seleccione **importación**.

    ![Importar archivo de configuración de publicación de hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    certificados de Hola se importan desde el archivo de configuración de publicación de hello en Visual Studio y ahora puede interactuar con los recursos de nube privada.
   
## <a name="next-steps"></a>Pasos siguientes
- [Publicación tooan servicio de nube de Azure desde Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Descarga e importación de la configuración de publicación y la información de suscripción](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
