---
title: las funciones de Azure mediante Visual Studio aaaDevelop | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodevelop y probar las funciones de Azure mediante el uso de funciones de Azure Tools para Visual Studio de 2017."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Herramientas de Azure Functions para Visual Studio  

Herramientas de funciones de Azure para Visual Studio de 2017 es una extensión de Visual Studio que le permite desarrollar, probar e implementar tooAzure de funciones de C#. Si se trata de la primera experiencia con las funciones de Azure, se puede obtener más información en [un tooAzure Introducción funciones](functions-overview.md).

Hola herramientas de funciones de Azure proporciona Hola siguientes ventajas: 

* Editar, compilar y ejecutar funciones en el equipo de desarrollo local. 
* Publicar las funciones de Azure directamente proyecto tooAzure. 
* Usar enlaces de función de trabajos Web atributos toodeclare directamente en código de C# en lugar de mantener un function.json independiente para las definiciones de enlace de Hola.
* Desarrollar e implementar funciones de C# compiladas previamente. Las funciones compiladas previamente proporcionan un mejor rendimiento de arranque en frío que las funciones basadas en scripts de C#. 
* Código de las funciones de C# al tiempo que tiene todas las ventajas de Hola de desarrollo de Visual Studio. 

Este tema muestra cómo toouse hello las funciones de Azure Tools para Visual Studio de 2017 toodevelop sus funciones en C#. También aprenderá cómo toopublish su tooAzure de proyecto como un ensamblado. NET.

## <a name="prerequisites"></a>Requisitos previos

Herramientas de funciones de Azure se incluye en la carga de trabajo de desarrollo de Azure de Hola de [Visual Studio 2017 versión 15.3](https://www.visualstudio.com/vs/), o una versión posterior. Asegúrese de incluir hello **desarrollo Azure** carga de trabajo en la instalación de la versión 15.3 2017 de Visual Studio:

![Instalar Visual Studio de 2017 con cargas de trabajo de desarrollo de Azure Hola](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate e implementar funciones, también deberá:

* Una suscripción de Azure activa. Si no tiene una suscripción de Azure, hay disponibles [cuentas gratis](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

* Una cuenta de almacenamiento de Azure. toocreate una cuenta de almacenamiento, consulte [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Creación de un proyecto de Azure Functions 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Configurar proyecto hello para el desarrollo local

Cuando crea un nuevo proyecto mediante la plantilla de funciones de Azure de hello, obtendrá un proyecto vacío en C# que contiene Hola siguientes archivos:

* **host.JSON**: le permite configurar Hola host de funciones. Esta configuración se aplica tanto cuando se ejecuta localmente como en Azure. Para más información, consulte el artículo de referencia sobre [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
    
* **local.settings.json**: mantiene la configuración que se usa cuando se ejecutan localmente las funciones. Esta configuración no se usa Azure, que se usan en hello [herramientas básicas de las funciones de Azure](functions-run-local.md). Use esta configuración de toospecify de archivo, como las cadenas de conexión tooother Azure servicios. Agregar un nuevo toohello clave **valores** matriz para cada conexión requerido por las funciones en el proyecto. Para obtener más información, consulte [archivo de configuración Local](functions-run-local.md#local-settings-file) de tema de hello herramientas básicas de las funciones de Azure.

en tiempo de ejecución de funciones de Hello usa una cuenta de almacenamiento de Azure internamente. Todo desencadenador tipos distintos de HTTP y webhooks, deben configurarse hello **Values.AzureWebJobsStorage** clave de cadena de conexión en la cuenta de almacenamiento de Azure de tooa válido.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 cadena de conexión de cuenta de almacenamiento de tooset hello:

1. En Visual Studio, abra **Explorer nube**, expanda **cuenta de almacenamiento** > **la cuenta de almacenamiento**, a continuación, seleccione **propiedades**copia hello y **cadena de conexión principal** valor.   

2. En el proyecto, abrir el archivo de proyecto de hello local.settings.json y establecer valor de Hola de hello **AzureWebJobsStorage** clave de cadena de conexión de toohello que ha copiado.

3. Repita Hola anterior paso tooadd claves únicas toohello **valores** matriz para cualquier otra conexión requeridos por las funciones.  

## <a name="create-a-function"></a>Creación de una función

En las funciones compiladas previamente, se definen los enlaces de hello utilizados por la función hello aplicando los atributos en el código de hello. Cuando usas hello las funciones de Azure Tools toocreate las funciones de plantillas de hello proporcionado, estos atributos se aplican automáticamente. 

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Agregar** > **Nuevo elemento**. Seleccione **función Azure**, escriba un **nombre** clase hello y haga clic en **agregar**.

2. Elija el desencadenador, definir propiedades de enlace de Hola y haga clic en **crear**. Hello en el ejemplo siguiente se muestra hello configuración cuando crea un almacenamiento de cola activa la función. 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Una clave de cadena de conexión denominada **QueueStorage** se proporciona, que se define en el archivo de hello local.settings.json. 
 
3. Examinar Hola recién agregado la clase. Vea una variable static **ejecutar** método, que tiene el atributo hello **FunctionName** atributo. Este atributo indica que el método de hello es punto de entrada de hello para la función hello. 

    Por ejemplo, hello después de la clase de C# representa una función básica de almacenamiento que se desencadena de cola:

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Un atributo específico de enlace es el método de punto de entrada de toohello tooeach aplicado enlace parámetro especificado. atributo de Hello toma la información de enlace de hello como parámetros. En el ejemplo anterior de hello, Hola primer parámetro tiene un **QueueTrigger** atributo aplicado, que indica la función de la cola activada. nombre de la cola de Hola y el nombre de configuración de cadena de conexión se pasan como parámetros.  

## <a name="testing-functions"></a>Funciones de prueba

Azure Functions Core Tools le permite ejecutar un proyecto de Azure Functions en el equipo de desarrollo local. Son solicitada tooinstall estas herramientas Hola la primera vez que inicie una función de Visual Studio.  

tootest su función, presione F5. Si se le solicita, Aceptar solicitud Hola de toodownload de Visual Studio e instalar herramientas de núcleo de las funciones de Azure (CLI).  También deberá tooenable una excepción de firewall para que las herramientas de hello pueden administrar las solicitudes HTTP.

Con proyecto Hola que se ejecuta, puede probar el código de modo que probaría función implementada. Para más información, consulte [Estrategias para probar el código en Azure Functions](functions-test-a-function.md). Cuando se ejecuta en modo de depuración, los puntos de interrupción se alcanzan en Visual Studio tal como se esperaba. 

Para obtener un ejemplo de cómo tootest una cola desencadenó la función, vea hello [tutorial de inicio rápido de función de cola activada](functions-create-storage-queue-triggered-function.md#test-the-function).  

toolearn más sobre el uso de herramientas de hello Azure funciones principales, vea [código y probar las funciones de Azure localmente](functions-run-local.md).

## <a name="publish-tooazure"></a>Publicar tooAzure

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Cualquier configuración que agregó en hello local.settings.json debe también agregará toohello función aplicación en Azure. Esta configuración no se agrega automáticamente. Puede agregar la configuración necesaria tooyour función aplicación de una de estas maneras:
>
>* [Uso de Hola portal de Azure](functions-how-to-use-azure-function-app-settings.md#settings).
>* [Con hello `--publish-local-settings` opción de publicación en hello Azure funciones principales herramientas](functions-run-local.md#publish).
>* [Uso de Hola CLI de Azure](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las herramientas de funciones de Azure, vea Hola comunes sección de preguntas frecuentes de hello [Visual Studio Tools de 2017 para las funciones de Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) entrada de blog.

toolearn más información sobre herramientas de hello Azure funciones principales, vea [código y probar las funciones de Azure localmente](functions-run-local.md).  
toolearn más sobre el desarrollo de las funciones como bibliotecas de clases. NET, vea [bibliotecas de clases de .NET usando con funciones de Azure](functions-dotnet-class-library.md). En este tema también proporciona ejemplos de cómo toouse atributos toodeclare Hola diversos tipos de enlaces admitidos por las funciones de Azure.    
