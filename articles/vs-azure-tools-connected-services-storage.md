---
title: aaaAdd almacenamiento de Azure mediante el uso de servicios conectados en Visual Studio | Documentos de Microsoft
description: "Agregar aplicación tooyour de almacenamiento de Azure mediante el cuadro de diálogo de Visual Studio agregar servicios conectados de Hola"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Adición de almacenamiento de Azure mediante Servicios conectados de Visual Studio
Con Visual Studio, puede conectarse a cualquiera de hello después tooAzure almacenamiento mediante el uso de hello **agregar servicios conectados** cuadro de diálogo:

- Servicio en la nube de C#
- Servició móvil de back-end de .NET
- Servicio o sitio web de ASP.NET
- Servicio de ASP.NET Core
- Servicio de trabajos web de Azure 

Hola funcionalidad del servicio conectado agrega todas las referencias de hello necesitado y el proyecto de tooyour de código de conexión y modifica los archivos de configuración correctamente. 

Una vez realizado, Hola **agregar servicios conectados** cuadro de diálogo muestra automáticamente la documentación que detalla Hola pasos toostart necesario trabajar con el almacenamiento de blobs, colas y tablas.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Conectar tooAzure almacenamiento mediante servicios conectados de hello diálogo
1. Abra el proyecto en Visual Studio.

1. En **el Explorador de soluciones**, contextual hello **servicios conectados** nodo y, en el menú contextual de Hola y seleccione **Agregar servicio conectado**.
   
    ![Incorporación de un servicio conectado de Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Hola **servicios conectados** página, seleccione **almacenamiento en la nube con el almacenamiento de Azure**.
   
    ![Incorporación de Azure Storage](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Hola **el almacenamiento de Azure** cuadro de diálogo, seleccione una cuenta de almacenamiento existente y seleccione **agregar**.
   
    Si necesita toocreate una cuenta de almacenamiento, vaya toohello siguiente paso. De lo contrario, vaya toostep 6.
    
    ![Agregar tooproject de cuenta de almacenamiento existente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate una cuenta de almacenamiento: 
   
   1. Seleccione **crear una nueva cuenta de almacenamiento** final Hola del cuadro de diálogo de Hola.

   1. Rellene hello **crear cuenta de almacenamiento** cuadro de diálogo y seleccione **crear**.
      
       ![Nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Cuando Hola **el almacenamiento de Azure** se muestra el cuadro de diálogo, Hola nueva cuenta de almacenamiento aparece en la lista de Hola. Seleccione la nueva cuenta de almacenamiento hello en lista de Hola y seleccione **agregar**.

1. Hola almacenamiento servicio conectado aparece bajo hello **referencias de servicio** nodo del proyecto.
   
## <a name="how-your-project-is-modified"></a>¿Cómo se modifica el proyecto?
Cuando termine de cuadro de diálogo de hello, Visual Studio agrega referencias y modifica determinados archivos de configuración. cambios concretos de Hello dependen del tipo de proyecto de hello: 

- Proyecto de ASP.NET - [¿Qué ha ocurrido? - Proyectos de ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Proyecto de ASP.NET Core - [¿Qué ha ocurrido? - Proyectos de ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Proyecto de servicio en la nube (roles web y roles de trabajo) - [¿Qué ha ocurrido? - Proyectos de servicios en la nube](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Proyecto de trabajo web - [¿Qué ha ocurrido? - Proyectos de trabajo web](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Pasos siguientes
- [Foro de MSDN: Almacenamiento de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog del equipo de Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentación de Almacenamiento de Azure](https://docs.microsoft.com/azure/storage/)
