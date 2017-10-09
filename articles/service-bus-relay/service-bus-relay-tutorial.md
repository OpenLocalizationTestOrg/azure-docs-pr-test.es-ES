---
title: "tutorial de retransmisión de WCF de Service Bus aaaAzure | Documentos de Microsoft"
description: "Cree un servicio y una aplicación cliente de Service Bus con Relay WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="8e5ea-103">Tutorial de Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="8e5ea-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="8e5ea-104">Este tutorial describe cómo toobuild WCF simple de retransmisión aplicación de cliente y el servicio utiliza la retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="8e5ea-105">Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="8e5ea-106">Trabajar a través de este tutorial le ofrece una descripción de pasos de hello toocreate requiere una aplicación de cliente y el servicio de retransmisión de WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="8e5ea-107">Como sus homólogos WCF originales, un servicio es una construcción que expone uno o varios puntos de conexión, cada uno de los cuales expone una o varias operaciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="8e5ea-108">extremo de Hola de un servicio especifica una dirección donde se puede encontrar el servicio de hello, un enlace que contiene información de Hola que un cliente debe comunicar con el servicio de Hola y un contrato que define la funcionalidad de hello proporcionada por los clientes de hello servicio tooits.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="8e5ea-109">Hola principal diferencia entre WCF y de retransmisión de WCF es que ese extremo Hola se expone en la nube de hello en lugar de localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="8e5ea-110">Después de trabajar a través de la secuencia de Hola de temas en este tutorial, tendrá un servicio en ejecución y un cliente que se puede invocar operaciones de hello del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="8e5ea-111">Hola primer tema describe cómo tooset una cuenta.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="8e5ea-112">se describen los pasos de Hello cómo toodefine un servicio que usa un contrato, cómo tooimplement Hola servicio y cómo tooconfigure Hola servicio en código.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="8e5ea-113">También se describe cómo servicio hello toohost y ejecución.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="8e5ea-114">Hello servicio que se crea se hospeda a sí mismo y cliente de Hola y el servicio se ejecutan en hello mismo equipo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="8e5ea-115">Puede configurar el servicio de hello mediante código o un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="8e5ea-116">pasos de tres final Hola describen cómo configurar la aplicación de cliente de hello, toocreate una aplicación cliente y crear y utilizar a un cliente que puede tener acceso a la funcionalidad de Hola de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e5ea-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8e5ea-117">Prerequisites</span></span>

<span data-ttu-id="8e5ea-118">toocomplete este tutorial, necesitará Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="8e5ea-119">[Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="8e5ea-120">En este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="8e5ea-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-121">An active Azure account.</span></span> <span data-ttu-id="8e5ea-122">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="8e5ea-123">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="8e5ea-124">Creación de un espacio de nombres de servicio</span><span class="sxs-lookup"><span data-stu-id="8e5ea-124">Create a service namespace</span></span>

<span data-ttu-id="8e5ea-125">Hola primer paso es un espacio de nombres toocreate y tooobtain una [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) clave.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="8e5ea-126">Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se exponen a través del servicio de retransmisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="8e5ea-127">Una clave SAS se genera automáticamente por el sistema de hello cuando se crea un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="8e5ea-128">combinación de Hola de espacio de nombres de servicio y la clave SAS proporciona credenciales de Hola para aplicación de Azure tooauthenticate access tooan.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="8e5ea-129">Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="8e5ea-130">Definición de un contrato de servicio de WCF</span><span class="sxs-lookup"><span data-stu-id="8e5ea-130">Define a WCF service contract</span></span>

<span data-ttu-id="8e5ea-131">contrato de servicio de Hello especifica qué operaciones (Hola terminología del servicio web de funciones o métodos) Hola servicio admite.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="8e5ea-132">Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="8e5ea-133">Cada método de interfaz de hello corresponde tooa operación del servicio concreta.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="8e5ea-134">Cada interfaz debe tener hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo aplicado tooit y cada operación debe tener hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit de atributo que se aplica.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="8e5ea-135">Si un método en una interfaz que tiene hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo no tiene hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo, que no se expone el método.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="8e5ea-136">código de Hello para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="8e5ea-137">Para obtener una descripción completa de contratos y servicios, vea [diseñar e implementar servicios](https://msdn.microsoft.com/library/ms729746.aspx) Hola documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="8e5ea-138">Creación de un contrato de retransmisión con una interfaz</span><span class="sxs-lookup"><span data-stu-id="8e5ea-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="8e5ea-139">Abra Visual Studio como administrador haciendo clic en el programa Hola Hola **iniciar** menú y seleccionando **ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="8e5ea-140">Cree un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-140">Create a new console application project.</span></span> <span data-ttu-id="8e5ea-141">Haga clic en hello **archivo** menú y seleccione **New**, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="8e5ea-142">Hola **nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#** (si **Visual C#** no aparece, mire debajo **otros lenguajes**).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="8e5ea-143">Haga clic en hello **aplicación de consola (.NET Framework)** plantilla y asígnele el nombre **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="8e5ea-144">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="8e5ea-145">Instalar paquete NuGet de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="8e5ea-146">Este paquete agrega automáticamente referencias toohello Service Bus bibliotecas, así como Hola WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="8e5ea-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres de Hola que habilita características básicas Hola de tooprogrammatically acceso de WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="8e5ea-148">Bus de servicio usa muchos de los objetos de Hola y atributos de contratos de servicio WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="8e5ea-149">En el Explorador de soluciones, haga clic en proyecto de hello y, a continuación, haga clic en **administrar paquetes de NuGet...** . Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="8e5ea-150">Ese nombre de proyecto Hola está seleccionado en hello **versiones** cuadro.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="8e5ea-151">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="8e5ea-152">En el Explorador de soluciones, haga doble clic en tooopen de archivo Program.cs hello en el editor de hello, si aún no está abrir.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="8e5ea-153">Agregue Hola siguientes instrucciones using al principio de hello del archivo de Hola:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="8e5ea-154">Cambiar el nombre del espacio de nombres de Hola de su nombre predeterminado de **EchoService** demasiado**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8e5ea-155">Este tutorial utiliza el espacio de nombres de hello C# **Microsoft.ServiceBus.Samples**, que es el espacio de nombres de Hola de hello basadas en contratos de tipo que se utiliza en el archivo de configuración de Hola Hola administrado [cliente de WCF configurar hello](#configure-the-wcf-client) paso.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="8e5ea-156">Puede especificar cualquier espacio de nombres que desee al compilar este ejemplo; Sin embargo, el tutorial de hello no funcionará a menos que, a continuación, modifique Hola espacios de nombres de servicio y contrato de hello en consecuencia, en el archivo de configuración de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="8e5ea-157">espacio de nombres de Hello especificado en hello App.config debe ser archivo mismo Hola como espacio de nombres de hello especificado en los archivos de C#.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="8e5ea-158">Directamente después de hello `Microsoft.ServiceBus.Samples` declaración de espacio de nombres, pero dentro del espacio de nombres de hello, defina una nueva interfaz denominada `IEchoContract` y aplicar hello `ServiceContractAttribute` interfaz toohello de atributo con un valor de espacio de nombres de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="8e5ea-159">valor de espacio de nombres de Hello difiere del espacio de nombres de Hola que utilizas en ámbito de hello del código.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="8e5ea-160">En su lugar, valor de espacio de nombres de Hola se utiliza como un identificador único para este contrato.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="8e5ea-161">Especificar explícitamente el espacio de nombres de hello, impide que valor de espacio de nombres predeterminado de Hola se agreguen toohello el nombre del contrato.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="8e5ea-162">Pegue Hola siguiente código después de la declaración de espacio de nombres de hello:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="8e5ea-163">Normalmente, el espacio de nombres del contrato de servicio de hello contiene un esquema de nomenclatura que incluya la información de versión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="8e5ea-164">Incluida la información de versión en el espacio de nombres del contrato de servicio de hello permite cambios importantes de servicios tooisolate definiendo un nuevo contrato de servicio con un nuevo espacio de nombres y exponerlo en un nuevo extremo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="8e5ea-165">De esta manera, los clientes pueden seguir contrato de servicio anterior toouse Hola sin necesidad de toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="8e5ea-166">La información de versión puede constar de una fecha o un número de compilación.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="8e5ea-167">Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="8e5ea-168">Para fines de Hola de este tutorial, Hola esquema del espacio de nombres del contrato de servicio de Hola de nombre no contiene información de versión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="8e5ea-169">Dentro de hello `IEchoContract` de la interfaz, declare un método para Hola Hola de operación único `IEchoContract` contrato expone Hola interfaz y aplique hello `OperationContractAttribute` método toohello de atributo que desea tooexpose como parte de Hola pública retransmisión de WCF contrato, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="8e5ea-170">Directamente después de hello `IEchoContract` definición de la interfaz, declare un canal que herede tanto `IEchoContract` y también toohello `IClientChannel` interfaz, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="8e5ea-171">Un canal es objeto WCF de Hola a través del cual cliente y el host de hello pasan información tooeach otras.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="8e5ea-172">Más tarde, escribirá el código de información de tooecho Hola canal entre dos aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="8e5ea-173">De hello **generar** menú, haga clic en **generar solución** o presione **Ctrl + Mayús + B** precisión de hello tooconfirm de su trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="8e5ea-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-174">Example</span></span>

<span data-ttu-id="8e5ea-175">Hola siguiente código muestra una interfaz básica que define un contrato de retransmisión de WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="8e5ea-176">Hello interfaz está creada, puede implementar interfaz Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="8e5ea-177">Contrato de WCF implemente Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-177">Implement hello WCF contract</span></span>

<span data-ttu-id="8e5ea-178">Crear una retransmisión de Azure requiere que cree primero el contrato de hello, que se define mediante una interfaz.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="8e5ea-179">Para obtener más información acerca de cómo crear la interfaz de hello, vea el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="8e5ea-180">Hola siguiente paso es interfaz de hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="8e5ea-181">Esto implica la creación de una clase denominada `EchoService` que implementa Hola definido por el usuario `IEchoContract` interfaz.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="8e5ea-182">Después de implementar la interfaz de hello, a continuación, configurar interfaz hello mediante un archivo de configuración App.config.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="8e5ea-183">archivo de configuración de Hello contiene información necesaria para la aplicación hello, como nombre de hello del servicio de hello, nombre de hello del contrato de Hola y tipo de Hola de protocolo que está toocommunicate usado con el servicio de retransmisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="8e5ea-184">código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="8e5ea-185">Para obtener información más general acerca de cómo tooimplement un servicio de contrato, consulte [implementar contratos de servicio](https://msdn.microsoft.com/library/ms733764.aspx) Hola documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="8e5ea-186">Crear una nueva clase denominada `EchoService` directamente después de la definición de Hola de hello `IEchoContract` interfaz.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="8e5ea-187">Hola `EchoService` clase implementa hello `IEchoContract` interfaz.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="8e5ea-188">Implementaciones de interfaz tooother similar, puede implementar definición hello en un archivo diferente.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="8e5ea-189">Sin embargo, para este tutorial, la implementación de hello está ubicada en hello mismo archivo como definición de interfaz de Hola y Hola `Main` método.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="8e5ea-190">Aplicar hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello `IEchoContract` interfaz.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="8e5ea-191">atributo de Hello especifica el espacio de nombres y nombre del servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="8e5ea-192">Una vez hecho esto, Hola `EchoService` clase aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="8e5ea-193">Hola implemente `Echo` método definido en hello `IEchoContract` interfaz Hola `EchoService` clase.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="8e5ea-194">Haga clic en **generar**, a continuación, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="8e5ea-195">Definir configuración de hello para el host del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="8e5ea-196">archivo de configuración de Hello es el archivo de configuración de WCF tooa muy similar.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="8e5ea-197">Se incluye el nombre del servicio Hola, endpoint (es decir, ubicación de Hola que Azure retransmisión expone para que los clientes y hosts toocommunicate entre sí) y Hola enlace (Hola el tipo de protocolo que se usa toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="8e5ea-198">Hello diferencia principal es que este punto de conexión de servicio configurado hace referencia tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) enlace, que no forma parte del programa Hola a .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="8e5ea-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) es uno de los enlaces de hello definidos por el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="8e5ea-200">En **el Explorador de soluciones**, haga doble clic en el archivo tooopen de hello App.config en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="8e5ea-201">Hola `<appSettings>` elemento, reemplace los marcadores de posición de Hola por nombre de Hola de su espacio de nombres de servicio y Hola clave SAS que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="8e5ea-202">Dentro de hello `<system.serviceModel>` etiquetas, agregue un `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="8e5ea-203">Puede definir varias aplicaciones de retransmisión en un único archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="8e5ea-204">Sin embargo, este tutorial solo define una.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="8e5ea-205">Dentro de hello `<services>` elemento, agregue un `<service>` nombre del servicio Hola Hola de toodefine de elemento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="8e5ea-206">Dentro de hello `<service>` elemento, definir Hola ubicación del contrato de extremo de Hola y Hola también tipo de enlace de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="8e5ea-207">punto de conexión de Hola define dónde debe buscar cliente hello para la aplicación de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="8e5ea-208">Más adelante, el tutorial de hello usa este toocreate paso un URI que exponga completamente el host de Hola a través de retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="8e5ea-209">enlace de Hello declara que estamos usando TCP como Hola toocommunicate de protocolo con el servicio de retransmisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="8e5ea-210">De hello **generar** menú, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="8e5ea-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-211">Example</span></span>

<span data-ttu-id="8e5ea-212">Hello código siguiente muestra implementación Hola Hola del contrato de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-212">hello following code shows hello implementation of hello service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="8e5ea-213">Hello código siguiente muestra hello formato básico del archivo App.config de hello asociado al host de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="8e5ea-214">Hospedar y ejecutar un tooregister de servicio web básico con el servicio de retransmisión de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="8e5ea-215">Este paso describe cómo toorun un Azure retransmisión servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="8e5ea-216">Crear credenciales de retransmisión de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="8e5ea-217">En `Main()`, cree dos variables en qué espacio de nombres de toostore Hola y Hola clave SAS que se leen desde la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="8e5ea-218">clave SAS de Hello será usado tooaccess más adelante el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="8e5ea-219">espacio de nombres de Hola se pasa como un parámetro demasiado`CreateServiceUri` toocreate un URI de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="8e5ea-220">Con un [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) objeto, declare que va a usar una clave SAS como tipo de credencial de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="8e5ea-221">Agregar Hola después el código directamente después de código de hello agregado en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="8e5ea-222">Crear una dirección base para el servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-222">Create a base address for hello service</span></span>

<span data-ttu-id="8e5ea-223">Después de código de hello agregado en el último paso de hello, cree un `Uri` instancia para la dirección base Hola del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="8e5ea-224">Este URI especifica el esquema de Bus de servicio de hello, espacio de nombres de Hola y ruta de acceso de Hola de interfaz de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="8e5ea-225">"sb" es una abreviatura para el esquema de Bus de servicio de Hola e indica que estamos usando TCP como protocolo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="8e5ea-226">Esto se ha indicado anteriormente en el archivo de configuración de hello, cuando [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) se especificó como enlace Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="8e5ea-227">Para este tutorial, hello URI es `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="8e5ea-228">Crear y configurar el host del servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="8e5ea-229">Establecer el modo de conectividad de hello demasiado`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="8e5ea-230">modo de conectividad de Hello describe Hola protocolo Hola servicio usa toocommunicate con servicio de retransmisión de hello; HTTP o TCP.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="8e5ea-231">Con configuración predeterminada de hello `AutoDetect`, servicio de hello intenta tooconnect tooAzure retransmisión a través de HTTP y TCP, si está disponible si TCP no está disponible.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="8e5ea-232">Tenga en cuenta que esto difiere del servicio de Hola Hola protocolo se especifica para la comunicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="8e5ea-233">Dicho protocolo viene determinado por enlace Hola utilizado.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="8e5ea-234">Por ejemplo, un servicio puede utilizar hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) enlace, que especifica que el extremo se comunica con los clientes a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="8e5ea-235">Que el mismo servicio podría especificar **ConnectivityMode.AutoDetect** para que el servicio de Hola se comunica con la retransmisión de Azure a través de TCP.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="8e5ea-236">Crear el host de servicio de hello, con hello que URI creado anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="8e5ea-237">host de servicio de Hello es objeto WCF de Hola que crea una instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="8e5ea-238">En este caso, se le pase tipo hello del servicio que desea toocreate (un `EchoService` tipo) y también la dirección del toohello a la que desea que el servicio de Hola de tooexpose.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="8e5ea-239">En hello parte superior del archivo de hello Program.cs, agregue referencias demasiado[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) y [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="8e5ea-240">En `Main()`, configurar el acceso público de hello extremo tooenable.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="8e5ea-241">Este paso informa a servicio de retransmisión de Hola que la aplicación se puede encontrar públicamente examinando la fuente ATOM de hello para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="8e5ea-242">Si establece **DiscoveryType** demasiado**privada**, un cliente todavía sería capaz de tooaccess servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="8e5ea-243">Sin embargo, el servicio de hello no aparecería cuando busca el espacio de nombres de hello retransmisión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="8e5ea-244">En su lugar, Hola cliente tendría ruta de acceso de punto de conexión de tooknow Hola con antelación.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="8e5ea-245">Aplicar credenciales del servicio de hello toohello puntos de conexión de servicio definidos en el archivo App.config de hello:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="8e5ea-246">Como se indicó en el paso anterior de hello, podría haberse declarado varios servicios y los puntos de conexión en el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="8e5ea-247">Si tuviera, este código recorrería el archivo de configuración de Hola y búsqueda para cada punto de conexión toowhich debería aplicar sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="8e5ea-248">Sin embargo, para este tutorial, el archivo de configuración de hello tiene solo un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="8e5ea-249">Host de servicio de hello abierto</span><span class="sxs-lookup"><span data-stu-id="8e5ea-249">Open hello service host</span></span>

1. <span data-ttu-id="8e5ea-250">Abra el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="8e5ea-251">Informar al usuario de Hola que Hola servicio está en ejecución y explique cómo tooshut servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="8e5ea-252">Cuando termine, cierre el host de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="8e5ea-253">Presione **Ctrl + Mayús + B** proyecto de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="8e5ea-254">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-254">Example</span></span>

<span data-ttu-id="8e5ea-255">El código de servicio completado debería tener el siguiente formato.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="8e5ea-256">código de Hello incluye contrato de servicio de Hola y la implementación de los pasos anteriores en el tutorial de Hola y Hola de hosts de servicio en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="8e5ea-257">Crear a un cliente WCF de contrato de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="8e5ea-258">paso siguiente Hello es toocreate una aplicación cliente y definir Hola contrato de servicio se implementarán en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="8e5ea-259">Tenga en cuenta que muchos de estos pasos son similares a los pasos de hello usa toocreate un servicio: definir un contrato, editar un archivo App.config de archivos, con el servicio de retransmisión de credenciales tooconnect toohello y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="8e5ea-260">código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="8e5ea-261">Crear un nuevo proyecto de la solución de Visual Studio actual de hello para el cliente de hello haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="8e5ea-262">En el Explorador de soluciones, en Hola la misma solución que contiene el servicio de hello, haga clic en la solución actual de hello (no en proyecto de hello) y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="8e5ea-263">Después, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="8e5ea-264">Hola **Agregar nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#** (si **Visual C#** no aparece, mire debajo **otros lenguajes**), seleccione Hola **Aplicación de consola (.NET Framework)** plantilla y asígnele el nombre **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="8e5ea-265">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="8e5ea-266">En el Explorador de soluciones, haga doble clic en el archivo Program.cs Hola Hola **EchoClient** proyecto tooopen abrir en el editor de hello, si aún no lo está.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="8e5ea-267">Cambiar el nombre del espacio de nombres de Hola de su nombre predeterminado de `EchoClient` demasiado`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="8e5ea-268">Instalar hello [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus): en el Explorador de soluciones, haga clic en hello **EchoClient** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="8e5ea-269">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="8e5ea-270">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="8e5ea-271">Agregar un `using` instrucción para hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) espacio de nombres en el archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="8e5ea-272">Agregar espacio de nombres de hello servicio contrato definición toohello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="8e5ea-273">Tenga en cuenta que esta definición es definición toohello idénticos que se usa en hello **servicio** proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="8e5ea-274">Debe agregar este código en parte superior de Hola de hello `Microsoft.ServiceBus.Samples` espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="8e5ea-275">Presione **Ctrl + Mayús + B** cliente de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="8e5ea-276">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-276">Example</span></span>

<span data-ttu-id="8e5ea-277">Hello código siguiente muestra hello estado actual del archivo Program.cs de Hola Hola **EchoClient** proyecto.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="8e5ea-278">Configurar el cliente WCF de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-278">Configure hello WCF client</span></span>

<span data-ttu-id="8e5ea-279">En este paso, creará un archivo App.config para una aplicación cliente básica que tiene acceso a servicios de hello creado anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="8e5ea-280">Este archivo App.config define el contrato de hello, enlace y el nombre de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="8e5ea-281">código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="8e5ea-282">En el Explorador de soluciones, en hello **EchoClient** proyecto de equipo y haga doble clic en **App.config** tooopen archivo de hello en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="8e5ea-283">Hola `<appSettings>` elemento, reemplace los marcadores de posición de Hola por nombre de Hola de su espacio de nombres de servicio y Hola clave SAS que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="8e5ea-284">De elemento de system.serviceModel hello, agregue un `<client>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="8e5ea-285">En este paso se declara que está definiendo una aplicación cliente de estilo WCF.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="8e5ea-286">Dentro de hello `client` elemento, Definir nombre hello, contrato y tipo de enlace de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="8e5ea-287">Este paso define nombre Hola de punto de conexión de hello, contrato de hello definido en el servicio de Hola y hechos de Hola que aplicación de cliente de hello usa TCP toocommunicate con retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="8e5ea-288">Hello nombre de punto de conexión se usa en hello siguiente paso toolink esta configuración de punto de conexión con el URI del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="8e5ea-289">Haga clic en **Archivo** y luego en **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="8e5ea-290">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-290">Example</span></span>

<span data-ttu-id="8e5ea-291">Hello código siguiente muestra archivo App.config de hello para el cliente de eco hello.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-291">hello following code shows hello App.config file for hello Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="8e5ea-292">Cliente de WCF implemente Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-292">Implement hello WCF client</span></span>
<span data-ttu-id="8e5ea-293">En este paso, se implementa una aplicación cliente básica que tiene acceso a servicios de Hola que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="8e5ea-294">Servicio toohello similar, el cliente de hello realiza muchas de hello mismo operaciones tooaccess retransmisión de Azure:</span><span class="sxs-lookup"><span data-stu-id="8e5ea-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="8e5ea-295">Establece el modo de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="8e5ea-296">Crea el URI que localiza el servicio de host de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="8e5ea-297">Define las credenciales de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="8e5ea-298">Se aplica Hola credenciales toohello conexión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="8e5ea-299">Abre la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-299">Opens hello connection.</span></span>
6. <span data-ttu-id="8e5ea-300">Realiza tareas de específicos de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="8e5ea-301">Cierra la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-301">Closes hello connection.</span></span>

<span data-ttu-id="8e5ea-302">Sin embargo, una de las principales diferencias de hello es que la aplicación de cliente de hello usa un servicio de retransmisión de canal tooconnect toohello, mientras que el servicio de hello utiliza una llamada demasiado**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="8e5ea-303">código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="8e5ea-304">Implementación de una aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="8e5ea-304">Implement a client application</span></span>
1. <span data-ttu-id="8e5ea-305">Establecer el modo de conectividad de hello demasiado**detección automática**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="8e5ea-306">Agregar Hola siguiente código dentro de hello `Main()` método de hello **EchoClient** aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="8e5ea-307">Definir variables toohold Hola valores para el espacio de nombres de servicio de Hola y la clave SAS que se leen desde la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="8e5ea-308">Crear Hola URI que define la ubicación de hello del host de hello en el proyecto de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="8e5ea-309">Crear objeto de credencial de hello para el punto de conexión del espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="8e5ea-310">Crear el generador de canales de Hola que carga la configuración de Hola que se describe en el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="8e5ea-311">Un generador de canales es un objeto WCF que crea un canal a través del cual se comunican las aplicaciones de cliente y servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="8e5ea-312">Aplicar las credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="8e5ea-313">Crear y abrir el servicio de toohello de canal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="8e5ea-314">Escribir la interfaz de usuario básica de Hola y funcionalidad de eco hello.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="8e5ea-315">Tenga en cuenta que código de hello usa instancia Hola del objeto de canal de Hola como un proxy para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="8e5ea-316">Cierre canal hello y generador de hello cerrar.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="8e5ea-317">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8e5ea-317">Example</span></span>

<span data-ttu-id="8e5ea-318">El código completado debe aparecer como sigue, que muestra cómo toocreate una aplicación cliente, cómo toocall Hola operaciones del servicio de Hola y cómo tooclose Hola a cliente después de la operación de hello llamar a finaliza.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a><span data-ttu-id="8e5ea-319">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="8e5ea-319">Run hello applications</span></span>

1. <span data-ttu-id="8e5ea-320">Presione **Ctrl + Mayús + B** solución de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="8e5ea-321">Esto compila el proyecto de cliente de Hola y el proyecto de servicio de Hola que creó en los pasos anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="8e5ea-322">Antes de la aplicación cliente en ejecución hello, debe asegurarse de que está ejecutando la aplicación de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="8e5ea-323">En el Explorador de soluciones en Visual Studio, haga clic en hello **EchoService** solución, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="8e5ea-324">En el cuadro de diálogo de propiedades de solución de hello, haga clic en **proyecto de inicio**, a continuación, haga clic en hello **proyectos de inicio múltiples** botón.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="8e5ea-325">Asegúrese de que **EchoService** aparece en primer lugar en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="8e5ea-326">Conjunto hello **acción** cuadro para ambos hello **EchoService** y **EchoClient** proyectos demasiado**iniciar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="8e5ea-327">Haga clic en **Dependencias del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="8e5ea-328">Hola **proyectos** cuadro, seleccione **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="8e5ea-329">Hola **depende de** cuadro, asegúrese de que **EchoService** está activada.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="8e5ea-330">Haga clic en **Aceptar** toodismiss hello **propiedades** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="8e5ea-331">Presione **F5** toorun ambos proyectos.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="8e5ea-332">Ambas ventanas de consola abrirse y solicitarle para nombre de espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="8e5ea-333">Hello servicio debe ejecutarse en primer lugar, por lo que en hello **EchoService** ventana de consola, escriba el espacio de nombres de hello y, a continuación, presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="8e5ea-334">A continuación, se le solicitará su clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="8e5ea-335">Escriba la clave SAS de hello y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="8e5ea-336">Este es el resultado de ejemplo de ventana de consola Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-336">Here is example output from hello console window.</span></span> <span data-ttu-id="8e5ea-337">Tenga en cuenta que los valores de hello figuran aquí se proporcionan por ejemplo solo con fines.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="8e5ea-338">`Your Service Namespace: myNamespace``Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="8e5ea-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="8e5ea-339">aplicación de servicio de Hello imprime la dirección de Hola la ventana toohello consola en el que está escuchando, tal como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="8e5ea-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/``Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="8e5ea-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="8e5ea-341">Hola **EchoClient** ventana de consola, escriba Hola la misma información que especificó anteriormente para la aplicación de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="8e5ea-342">Siga Hola de hello anteriores pasos tooenter mismo espacio de nombres de servicio y la SAS de valores para la aplicación de cliente de hello de clave.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="8e5ea-343">Después de escribir estos valores, cliente hello abre un servicio de toohello de canal y le pide tooenter algún texto tal como se muestra en el siguiente ejemplo de salida de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="8e5ea-344">Escriba alguna aplicación de servicio de texto toosend toohello y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="8e5ea-345">Este texto se envía el servicio de toohello a través de la operación de servicio eco hello y aparece en la ventana de consola de servicio de hello como en la siguiente salida de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="8e5ea-346">aplicación de cliente de Hello recibe el valor devuelto de Hola de hello `Echo` operación, que es el texto original de Hola y lo imprime tooits ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="8e5ea-347">Hola aquí te mostramos la salida de ejemplo de ventana de consola de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="8e5ea-348">Puede continuar enviando mensajes de texto hello toohello servicio del cliente de esta manera.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="8e5ea-349">Cuando haya terminado, presione ENTRAR en tooend de windows de consola de cliente y servicio Hola ambas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e5ea-350">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e5ea-350">Next steps</span></span>

<span data-ttu-id="8e5ea-351">Este tutorial se ha explicado cómo toobuild una aplicación de cliente de retransmisión de Azure y el servicio utilizando Hola capacidades de retransmisión de WCF de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="8e5ea-352">Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8e5ea-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="8e5ea-353">toolearn más información acerca de la retransmisión de Azure, vea Hola temas siguientes.</span><span class="sxs-lookup"><span data-stu-id="8e5ea-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="8e5ea-354">Información general sobre la arquitectura de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="8e5ea-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="8e5ea-355">Introducción a Azure Relay</span><span class="sxs-lookup"><span data-stu-id="8e5ea-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="8e5ea-356">Cómo el servicio con .NET de la retransmisión de hello toouse WCF</span><span class="sxs-lookup"><span data-stu-id="8e5ea-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
