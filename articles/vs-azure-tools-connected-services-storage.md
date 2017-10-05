---
title: "Adición de Azure Storage con Servicios conectados en Visual Studio | Microsoft Docs"
description: "Adición de almacenamiento de Azure a la aplicación mediante el cuadro de diálogo Agregar servicios conectados de Visual Studio"
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
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Adición de almacenamiento de Azure mediante Servicios conectados de Visual Studio
Con Visual Studio, puede conectar cualquiera de lo siguiente a Azure Storage mediante el uso del cuadro de diálogo **Add Connected Services** (Agregar servicios conectados):

- Servicio en la nube de C#
- Servició móvil de back-end de .NET
- Servicio o sitio web de ASP.NET
- Servicio de ASP.NET Core
- Servicio de trabajos web de Azure 

La funcionalidad del servicio conectado agrega todo el código de conexión y las referencias necesarios al proyecto y modifica los archivos de configuración de forma adecuada. 

Cuando se completa, el cuadro de diálogo **Add Connected Services** (Agregar servicios conectados) muestra automáticamente documentación que detalla los pasos necesarios para empezar a trabajar con el almacenamiento de blobs, colas y tablas.

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a>Conexión con Almacenamiento de Azure mediante el cuadro de diálogo Servicios conectados
1. Abra el proyecto en Visual Studio.

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo **Servicios conectados** y, en el menú contextual, seleccione **Agregar servicio conectado**.
   
    ![Incorporación de un servicio conectado de Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. En la página **Servicios conectados**, seleccione **Almacenamiento en la nube con Azure Storage**.
   
    ![Incorporación de Azure Storage](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. En el cuadro de diálogo **Azure Storage**, elija una cuenta de almacenamiento existente y seleccione **Agregar**.
   
    Si necesita crear una cuenta de almacenamiento, vaya al siguiente paso. De lo contrario, vaya al paso 6.
    
    ![Incorporación de una cuenta de almacenamiento existente al proyecto](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. Para crear una cuenta de almacenamiento: 
   
   1. Seleccione **Crear una nueva cuenta de almacenamiento** en la parte inferior del cuadro de diálogo.

   1. Rellene el cuadro de diálogo **Crear cuenta de almacenamiento** y seleccione **Crear**.
      
       ![Nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Cuando se muestre el cuadro de diálogo **Azure Storage**, la nueva cuenta de almacenamiento aparecerá en la lista. Seleccione la nueva cuenta de almacenamiento en la lista y seleccione **Agregar**.

1. El servicio de almacenamiento conectado aparece bajo el nodo **Referencias de servicio** del proyecto.
   
## <a name="how-your-project-is-modified"></a>¿Cómo se modifica el proyecto?
Cuando haya terminado con el cuadro de diálogo, Visual Studio agrega referencias y modifica determinados archivos de configuración. Los cambios específicos dependen del tipo de proyecto: 

- Proyecto de ASP.NET - [¿Qué ha ocurrido? - Proyectos de ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Proyecto de ASP.NET Core - [¿Qué ha ocurrido? - Proyectos de ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Proyecto de servicio en la nube (roles web y roles de trabajo) - [¿Qué ha ocurrido? - Proyectos de servicios en la nube](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Proyecto de trabajo web - [¿Qué ha ocurrido? - Proyectos de trabajo web](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Pasos siguientes
- [Foro de MSDN: Almacenamiento de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog del equipo de Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentación de Almacenamiento de Azure](https://docs.microsoft.com/azure/storage/)
