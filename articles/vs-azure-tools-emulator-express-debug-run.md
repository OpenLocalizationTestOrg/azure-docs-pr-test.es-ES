---
title: servicio en un equipo local en la nube aaaUsing Emulator Express toorun y depurar un Azure | Documentos de Microsoft
description: Usar Emulator Express toorun y depurar un servicio de nube en un equipo local
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Con Emulator Express toorun y depurar un Azure servicio en la nube en un equipo local
Con Emulator Express, puede probar y depurar un servicio en la nube sin ejecutar Visual Studio como administrador. Puede establecer el toouse de configuración de proyecto cualquier Emulator Express u Hola emulador completo, según los requisitos de Hola de servicio en la nube. Para obtener más información acerca del emulador completo hello, consulte [ejecutar una aplicación de Azure en hello emulador de proceso](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Uso de Emulator Express en Visual Studio
Al crear un proyecto de Azure en Azure SDK 2.3 o posterior, Emulator Express se usa automáticamente. Para los proyectos existentes que se crearon con una versión anterior de hello Azure SDK, use Hola después tooselect pasos Emulator Express:

1. Cree o abra un proyecto de servicio en la nube de Azure en Visual Studio.

1. En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.

1. En las páginas de propiedades de proyectos de hello, seleccione hello **Web** ficha.

    ![Propiedades de proyecto de servicio en la nube de Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. En **Servidor de desarrollo local**, seleccione la opción **Usar IIS Express**.

1. En **Emulador**, seleccione **usar Emulator Express**.
   
1. toolaunch Hola Emulator Express, ejecute hello siguiente comando en un símbolo del sistema: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitaciones de Emulator Express
Hola problemas siguientes se conoce las limitaciones de Emulator Express: 

- Emulator Express no es compatible con el servidor web de IIS.
- El servicio de nube puede contener varios roles, pero cada rol es instancia tooone limitado.
- No puede tener acceso a los números de puerto inferiores a 1000. Si utiliza un proveedor de autenticación que normalmente utiliza un puerto inferior a 1000, tendrá que toochange este número de puerto de tooa valor por encima de 1000.
- Las limitaciones que se aplican toohello emulador de proceso de Azure también aplican tooEmulator Express. Por ejemplo, no puede tener más de 50 instancias de rol por implementación. Para obtener más información acerca de hello emulador de proceso de Azure, consulte [ejecutar una aplicación de Azure en hello emulador de proceso](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Pasos siguientes
[Depuración de servicios en la nube de Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
