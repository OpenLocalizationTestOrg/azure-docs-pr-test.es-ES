---
title: aaaConfiguring y usar Hola emulador de almacenamiento con Visual Studio | Documentos de Microsoft
description: Configurar y utilizar Hola emulador de almacenamiento con Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Configurar y utilizar Hola emulador de almacenamiento con Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Información general
entorno de desarrollo de Hello Azure SDK incluye emulador de almacenamiento de hello, que simula Hola Blob, cola y tabla de servicios de almacenamiento disponibles en Azure en su equipo de desarrollo local. Si está creando un servicio de nube que emplea servicios de almacenamiento de Azure de hello o escribe una aplicación externa que llama Hola servicios de almacenamiento, puede probar el código localmente en el emulador de almacenamiento de Hola. Hello Azure Tools para Microsoft Visual Studio integrar la administración de emulador de almacenamiento de hello en Visual Studio. Hello Azure Tools inicializar base de datos del emulador de almacenamiento de Hola por primera vez, inicia Hola servicio del emulador de almacenamiento al ejecutar o depurar el código de Visual Studio y proporciona los datos del emulador de almacenamiento de acceso de solo lectura toohello a través de hello Azure Storage Explorer.

Para obtener información detallada sobre el emulador de almacenamiento de hello, incluidos los requisitos del sistema e instrucciones de configuración personalizada, vea [Hola uso emulador de almacenamiento de Azure para desarrollo y pruebas](storage/common/storage-use-emulator.md).

> [!NOTE]
> Hay algunas diferencias de funcionalidad entre la simulación del emulador de almacenamiento hello y servicios de almacenamiento de Azure de Hola. Vea [hello las diferencias entre el emulador de almacenamiento y los servicios de almacenamiento de Azure](storage/common/storage-use-emulator.md) en la documentación del SDK de Azure para obtener información sobre las diferencias específicas de Hola Hola.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Configurar una cadena de conexión para el emulador de almacenamiento de Hola
emulador de almacenamiento tooaccess Hola desde el código dentro de un rol, le interesará tooconfigure una conexión de cadena que emulador de almacenamiento de toohello puntos y que más adelante puede ser modificada toopoint tooan cuenta de almacenamiento de Azure. Una cadena de conexión es una opción de configuración que el rol puede leer en la cuenta de almacenamiento de tooa de tooconnect en tiempo de ejecución. Para obtener más información acerca de cómo toocreate las cadenas de conexión, consulte [Hola Configurar aplicación de Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Puede devolver una cuenta de emulador de almacenamiento de toohello de referencia desde el código mediante el uso de hello **DevelopmentStorageAccount** propiedad. Este enfoque funciona correctamente si desea tooaccess Hola emulador de almacenamiento desde el código, pero si tiene previsto toopublish tooAzure de su aplicación, necesitará toocreate una tooaccess de cadena de conexión de su cuenta de almacenamiento de Azure y modificar su código toouse que cadena de conexión antes de publicarla. Si se cambia entre la cuenta del emulador de almacenamiento de hello y una cuenta de almacenamiento de Azure con frecuencia, una cadena de conexión simplificará el proceso.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Inicializar y ejecutar el emulador de almacenamiento de Hola
Puede especificar que, al ejecutar o depurar su servicio en Visual Studio, Visual Studio inicia automáticamente el emulador de almacenamiento de Hola. En el Explorador de soluciones, abra el menú contextual de hello para el **Azure** del proyecto y elija **propiedades**. En hello **desarrollo** ficha Hola **iniciar emulador de almacenamiento de Azure** elija **True** (si no se ha establecido el valor de toothat).

Hola primera vez ejecutar o depurar su servicio desde Visual Studio, el emulador de almacenamiento de hello inicia un proceso de inicialización. Este proceso reserva los puertos locales para el emulador de almacenamiento de Hola y crea la base de datos del emulador de almacenamiento de Hola. Una vez completado, este proceso no es necesario toorun nuevo a menos que se elimina la base de datos del emulador de almacenamiento de Hola.

> [!NOTE]
> A partir de versión de junio de 2012 de Hola de hello Azure Tools, emulador de almacenamiento de Hola se ejecuta de forma predeterminada, en SQL Express LocalDB. En versiones anteriores de hello Azure Tools, el emulador de almacenamiento de Hola se ejecuta en una instancia predeterminada de SQL Express 2005 o 2008, que se debe instalar antes de poder instalar hello Azure SDK. También puede ejecutar el emulador de almacenamiento de hello en una instancia con nombre de SQL Express o un conjunto con nombre o la instancia predeterminada de Microsoft SQL Server. Si necesita tooconfigure Hola almacenamiento emulador toorun con una instancia distinta de la instancia predeterminada de hello, consulte [Hola uso emulador de almacenamiento de Azure para desarrollo y pruebas](storage/common/storage-use-emulator.md).
> 
> 

emulador de almacenamiento de Hello proporciona un estado de Hola de tooview de interfaz de usuario de servicios de almacenamiento local de Hola y toostart, detenga y restablecerlos. Una vez que se ha iniciado el servicio del emulador de almacenamiento hello, puede mostrar la interfaz de usuario de Hola o iniciar o detener el servicio haciendo clic en el icono del área de notificación de Hola de Hola Hola emulador de Microsoft Azure en la barra de tareas de Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Visualización de los datos del emulador de almacenamiento en el Explorador de servidores
nodo de almacenamiento de Azure de Hello en el Explorador de servidores permite a tooview datos y cambiar la configuración para el blob y datos de la tabla en sus cuentas de almacenamiento, incluido Hola emulador de almacenamiento. Consulte [Administración de recursos de Azure Blob Storage con el Explorador de Storage (versión preliminar)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) para más información.

