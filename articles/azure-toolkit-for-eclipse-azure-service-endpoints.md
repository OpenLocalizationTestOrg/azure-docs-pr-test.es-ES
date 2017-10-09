---
title: aaaAzure los extremos de servicio
description: "Describe la configuración de extremo de servicio de Azure de hello en hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Puntos de conexión de servicio de Azure
Los puntos de conexión de servicio de Azure determinan que si la aplicación está implementada tooand administrado por la plataforma global de Azure hello, Azure operado por 21Vianet en China o una privada plataforma Windows Azure. Hola **los extremos de servicio** cuadro de diálogo permite toospecify que desea toouse de los extremos del servicio. Hola tooopen **los extremos de servicio** cuadro de diálogo, en Eclipse, haga clic en **ventana**, haga clic en **preferencias**, expanda **Azure**y, a continuación, haga clic en **Los extremos del servicio**. Hola configuración **conjunto Active** campo determina qué servicio de Azure extremos se utilizarán para hello Azure proyectos en el área de trabajo actual.

siguiente Hello muestra hello **los extremos de servicio** cuadro de diálogo.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>extremos de servicio de hello tooset
Hola **los extremos de servicio** cuadro de diálogo, realice una de hello siguientes acciones:

* Si desea toouse Hola plataforma global de Azure, de hello **conjunto Active** lista desplegable, seleccione **windowsazure.com** y haga clic en **Aceptar**.

* Si desea toouse Azure operado por 21Vianet en China, de hello **conjunto Active** lista desplegable, seleccione **windowsazure.cn (China)** y haga clic en **Aceptar**.

* Si desea que toouse una plataforma de Azure privada:

  1. Haga clic en **Editar**.

  2. Se abre un cuadro de diálogo, que le informa de que hello **los extremos de servicio** cuadro de diálogo se cerrará y se abrirá el archivo de conjuntos de preferencias de hello. Haga clic en **Aceptar**.

  3. En el archivo de hello preferencesets.xml, cree un nuevo `preferenceset` elemento. Para este nuevo elemento, crear `name`, `blob`, `management`, `portalURL` y `publishsettings` atributos y agrégueles valores correspondientes de la plataforma de Azure privada tooyour. Puede utilizar valores de hello proporcionados Hola existentes `preferenceset` elementos como plantillas. **Tenga en cuenta**: Hola valor utilizado para hello `blob` atributo debe contener texto hello "blob" en la dirección URL de Hola.

  4. Guarde y cierre preferencesets.xml.

  5. Vuelva a abrir hello **los extremos de servicio** cuadro de diálogo.

  6. De hello **conjunto Active** lista desplegable, seleccione Hola activo establecido que creó y haga clic en **Aceptar**.

  7. Una vez que ha creado su plataforma de Azure privada `preferenceset` elemento, puede cambiar Hola valores asignados tooit haciendo clic en hello **editar** botón en hello **punto de conexión de servicios** cuadro de diálogo. También puede crear varios elementos `preferenceset` de la plataforma de Azure privada, si así lo desea.

## <a name="see-also"></a>Otras referencias
[kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]

[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
