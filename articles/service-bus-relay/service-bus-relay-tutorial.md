---
title: Tutorial de Azure Service Bus WCF Relay | Microsoft Docs
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
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="9b3bc-103">Tutorial de Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="9b3bc-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="9b3bc-104">En este tutorial se describe cómo crear un servicio y una aplicación cliente de WCF Relay sencillos mediante Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="9b3bc-105">Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="9b3bc-106">Al trabajar con este tutorial adquirirá unos conocimientos sobre los pasos necesarios para crear una aplicación cliente y de servicio de WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="9b3bc-107">Como sus homólogos WCF originales, un servicio es una construcción que expone uno o varios puntos de conexión, cada uno de los cuales expone una o varias operaciones de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="9b3bc-108">El extremo de un servicio especifica una dirección donde se puede encontrar el servicio, un enlace que contiene la información que un cliente debe comunicar al servicio y un contrato que define la funcionalidad que ofrece el servicio a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="9b3bc-109">La diferencia principal entre WCF y WCF Relay es que el punto de conexión se expone en la nube en lugar de localmente en su equipo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="9b3bc-110">Cuando complete la secuencia de temas de este tutorial, tendrá un servicio en ejecución y un cliente que puede invocar las operaciones de este servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="9b3bc-111">En el primer tema se describe cómo configurar una cuenta.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="9b3bc-112">Los pasos siguientes explican cómo definir un servicio que usa un contrato, cómo implementar dicho servicio y cómo configurarlo en el código.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="9b3bc-113">También se describe cómo se hospeda y ejecuta el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="9b3bc-114">El servicio que se crea se hospeda a sí mismo y el cliente y el servicio se ejecutan en el mismo equipo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="9b3bc-115">Puede configurar el servicio mediante código o con un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="9b3bc-116">En los últimos tres pasos se describe cómo crear una aplicación cliente, cómo configurarla y cómo crear y usar un cliente que pueda tener acceso a la funcionalidad del host.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b3bc-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b3bc-117">Prerequisites</span></span>

<span data-ttu-id="9b3bc-118">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="9b3bc-119">[Microsoft Visual Studio 2015 o una versión superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="9b3bc-120">En este tutorial se usa Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="9b3bc-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-121">An active Azure account.</span></span> <span data-ttu-id="9b3bc-122">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="9b3bc-123">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="9b3bc-124">Creación de un espacio de nombres de servicio</span><span class="sxs-lookup"><span data-stu-id="9b3bc-124">Create a service namespace</span></span>

<span data-ttu-id="9b3bc-125">El primer paso consiste en crear un espacio de nombres y obtener una clave de [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="9b3bc-126">Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se expone a través del servicio de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="9b3bc-127">El sistema genera una clave SAS automáticamente cuando se crea un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="9b3bc-128">La combinación del espacio de nombres de servicio y la clave SAS proporciona las credenciales para que Azure autentique el acceso a una aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="9b3bc-129">Siga las [instrucciones a continuación](relay-create-namespace-portal.md) para crear un espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="9b3bc-130">Definición de un contrato de servicio de WCF</span><span class="sxs-lookup"><span data-stu-id="9b3bc-130">Define a WCF service contract</span></span>

<span data-ttu-id="9b3bc-131">El contrato de servicio especifica las operaciones (la terminología del servicio web para funciones o métodos).que admite el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="9b3bc-132">Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="9b3bc-133">Cada método de la interfaz corresponde a una operación de servicio específica.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="9b3bc-134">Todas las interfaces deben tener el atributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) aplicado, y todas las operaciones deben tener el atributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) aplicado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="9b3bc-135">Si un método en una interfaz que tiene el atributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) no tiene el atributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), no se expone dicho método.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="9b3bc-136">El código para estas tareas se ofrece en el ejemplo a continuación del procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="9b3bc-137">Para leer una descripción completa de los contratos y servicios, vea [Diseño e implementación de servicios](https://msdn.microsoft.com/library/ms729746.aspx), en la documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="9b3bc-138">Creación de un contrato de retransmisión con una interfaz</span><span class="sxs-lookup"><span data-stu-id="9b3bc-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="9b3bc-139">Abra Visual Studio como administrador, para lo que debe hacer clic con el botón derecho en el programa del menú **Inicio** y, después, haga clic en **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="9b3bc-140">Cree un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-140">Create a new console application project.</span></span> <span data-ttu-id="9b3bc-141">Haga clic en el menú **Archivo** y seleccione **Nuevo**; a continuación, haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="9b3bc-142">En el cuadro de diálogo **Nuevo proyecto**, haga clic en **Visual C#** (si **Visual C#** no aparece, mire en **Otros lenguajes**).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="9b3bc-143">Haga clic en la plantilla **Aplicación de consola (.NET Framework)** y asígnele el nombre **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="9b3bc-144">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="9b3bc-145">Instale el paquete NuGet del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="9b3bc-146">Este paquete agrega automáticamente referencias a las bibliotecas de Service Bus, así como a **System.ServiceModel** de WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="9b3bc-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres que permite el acceso mediante programación a las características básicas de WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="9b3bc-148">Bus de servicio utiliza muchos de los objetos y atributos de WCF para definir contratos de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="9b3bc-149">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y, luego, en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="9b3bc-150">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="9b3bc-151">Asegúrese de que el nombre del proyecto está seleccionado en el cuadro **Versiones**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="9b3bc-152">Haga clic en **Instalar**y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="9b3bc-153">En el Explorador de soluciones, haga doble clic en el archivo Program.cs para abrirlo en el editor en caso de que no esté ya abierto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="9b3bc-154">Agregue las siguientes instrucciones using en la parte superior del archivo:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="9b3bc-155">Cambie el nombre de espacio de nombres de su nombre predeterminado **EchoService** a **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9b3bc-156">En este tutorial se usa el espacio de nombres de C# **Microsoft.ServiceBus.Samples**, que es el espacio de nombres del tipo administrado por contrato que se utiliza en el archivo de configuración del paso [Configurar el cliente de WCF](#configure-the-wcf-client).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="9b3bc-157">Puede especificar el espacio de nombres que quiera al compilar este ejemplo; no obstante, el tutorial no funcionará a menos que también modifique los espacios de nombres del contrato y el servicio de manera acorde, en el archivo de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="9b3bc-158">El espacio de nombres especificado en el archivo App.config debe ser el mismo que el que se especifique en los archivos de C#.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="9b3bc-159">Inmediatamente después de la declaración del espacio de nombres `Microsoft.ServiceBus.Samples`, pero dentro del espacio de nombres, defina una nueva interfaz denominada `IEchoContract` y aplique el atributo `ServiceContractAttribute` a la interfaz con un valor de espacio de nombres de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="9b3bc-160">El valor del espacio de nombres difiere del espacio de nombres que utiliza en todo el ámbito de su código.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="9b3bc-161">En su lugar, el valor del espacio de nombres se usa como identificador único para este contrato.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="9b3bc-162">La especificación del espacio de nombres impide explícitamente que el valor del espacio de nombres predeterminado se agregue al nombre del contrato.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="9b3bc-163">Pegue el siguiente fragmento de código después de la declaración de espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="9b3bc-164">Normalmente, el espacio de nombres del contrato de servicio contiene un esquema de nomenclatura que incluye información de versión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="9b3bc-165">Al incluirse la información de versión en el espacio de nombres del contrato de servicio, los servicios pueden aislar los cambios más importantes mediante la definición de un nuevo contrato de servicio con un nuevo espacio de nombres y su exposición en un nuevo extremo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="9b3bc-166">De esta manera, los clientes pueden seguir usando el contrato de servicio anterior sin tener que actualizarse.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="9b3bc-167">La información de versión puede constar de una fecha o un número de compilación.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="9b3bc-168">Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="9b3bc-169">Para los fines de este tutorial, el esquema de nomenclatura del espacio de nombres del contrato de servicio no contiene información de versión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="9b3bc-170">En la interfaz de `IEchoContract`, declare un método para la operación sencilla que el contrato `IEchoContract` expone en la interfaz y aplique el atributo `OperationContractAttribute` al método que quiere exponer como parte del contrato público de Relay WCF de la siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="9b3bc-171">Justo después de la definición de interfaz `IEchoContract`, declare un canal que herede de `IEchoContract` y también de la interfaz de `IClientChannel`, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="9b3bc-172">Un canal es el objeto de WCF a través del cual el host y el cliente se pasan información entre sí.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="9b3bc-173">Más tarde, escribirá código para el canal a fin de enviar información entre las dos aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="9b3bc-174">En el menú **Compilar**, haga clic en **Compilar solución** o presione **Ctrl+Mayús+B** para confirmar la precisión del trabajo realizado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="9b3bc-175">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-175">Example</span></span>

<span data-ttu-id="9b3bc-176">En el ejemplo de código siguiente se muestra una interfaz básica que define un contrato de WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="9b3bc-177">Ahora que la interfaz se ha creado, puede implementarla.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="9b3bc-178">Implementación del contrato de WCF</span><span class="sxs-lookup"><span data-stu-id="9b3bc-178">Implement the WCF contract</span></span>

<span data-ttu-id="9b3bc-179">La creación de una retransmisión de Azure requiere que primero cree el contrato, que se define con una interfaz.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="9b3bc-180">Para más información sobre cómo crear la interfaz, consulte el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="9b3bc-181">El siguiente paso es implementar la interfaz.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-181">The next step is to implement the interface.</span></span> <span data-ttu-id="9b3bc-182">Esto implica la creación de una clase denominada `EchoService` que implemente la interfaz `IEchoContract` definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="9b3bc-183">Después de implementar la interfaz, se debe configurar con un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="9b3bc-184">El archivo de configuración contiene la información necesaria para la aplicación, como el nombre del servicio, el nombre del contrato y el tipo de protocolo que se utiliza para comunicarse con el servicio de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="9b3bc-185">El código utilizado para estas tareas se proporciona en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="9b3bc-186">Para obtener información más general sobre cómo implementar un contrato de servicio, vea [Implementación de contratos de servicio](https://msdn.microsoft.com/library/ms733764.aspx) en la documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="9b3bc-187">Cree una nueva clase denominada `EchoService` directamente después de la definición de la interfaz `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="9b3bc-188">La clase `EchoService` implementa la interfaz `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="9b3bc-189">Al igual que otras implementaciones de interfaz, puede implementar la definición en un archivo diferente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="9b3bc-190">Sin embargo, para este tutorial, la implementación se ubica en el mismo archivo que la definición de la interfaz y el método `Main`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="9b3bc-191">Aplique el atributo [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) en la interfaz de `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="9b3bc-192">El atributo especifica el nombre del servicio y el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="9b3bc-193">Después de hacerlo, aparecerá la clase `EchoService` de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="9b3bc-194">Implemente el método `Echo` definido en la interfaz `IEchoContract` de la clase `EchoService`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="9b3bc-195">Haga clic en **Compilar** y luego en **Compilar solución** para confirmar la precisión del trabajo realizado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="9b3bc-196">Definición de la configuración del host de servicios</span><span class="sxs-lookup"><span data-stu-id="9b3bc-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="9b3bc-197">El archivo de configuración es muy similar a un archivo de configuración de WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="9b3bc-198">Incluye el nombre del servicio, el punto de conexión (es decir, la ubicación que Azure Relay expone para que clientes y hosts se comuniquen entre sí) y el enlace (el tipo de protocolo que se usa para la comunicación).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="9b3bc-199">La principal diferencia es que el punto de conexión de servicio configurado hace referencia a un enlace [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) que no forma parte de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="9b3bc-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) es uno de los enlaces que define el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="9b3bc-201">En el **Explorador de soluciones**, haga doble clic en el archivo App.config para abrirlo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="9b3bc-202">En el elemento `<appSettings>`, reemplace los marcadores de posición con el nombre de su espacio de nombres de servicio y la clave SAS que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="9b3bc-203">Dentro de las etiquetas `<system.serviceModel>`, agregue un elemento `<services>`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="9b3bc-204">Puede definir varias aplicaciones de retransmisión en un único archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="9b3bc-205">Sin embargo, este tutorial solo define una.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="9b3bc-206">Dentro del elemento `<services>`, agregue un elemento `<service>` para definir el nombre del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="9b3bc-207">Dentro del elemento `<service>`, defina la ubicación del contrato del punto de conexión y también el tipo de enlace del extremo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="9b3bc-208">El extremo define dónde buscará el cliente la aplicación host.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="9b3bc-209">Más adelante en el tutorial, se usa este paso para crear un identificador URI que expone completamente el host a través de Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="9b3bc-210">El enlace declara que se está usando TCP como el protocolo para comunicarse con el servicio de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="9b3bc-211">En el menú **Compilar**, haga clic en **Compilar solución** para confirmar la precisión del trabajo realizado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="9b3bc-212">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-212">Example</span></span>

<span data-ttu-id="9b3bc-213">En el código siguiente se muestra la implementación del contrato de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-213">The following code shows the implementation of the service contract.</span></span>

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

<span data-ttu-id="9b3bc-214">En el código siguiente se muestra el formato básico del archivo App.config asociado al servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="9b3bc-215">Hospedaje y ejecución de un servicio web básico para registrarse con el servicio de retransmisión</span><span class="sxs-lookup"><span data-stu-id="9b3bc-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="9b3bc-216">Este paso describe cómo ejecutar un servicio de Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="9b3bc-217">Creación de las credenciales de retransmisión</span><span class="sxs-lookup"><span data-stu-id="9b3bc-217">Create the relay credentials</span></span>

1. <span data-ttu-id="9b3bc-218">En `Main()`, cree dos variables para almacenar el espacio de nombres y la clave de SAS que se leen desde la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="9b3bc-219">La clave de SAS se usará más adelante para obtener acceso al proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="9b3bc-220">El espacio de nombres se pasa como parámetro a `CreateServiceUri` para crear un URI de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="9b3bc-221">Con un objeto [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior), declare que usará una clave de SAS como tipo de credencial.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="9b3bc-222">Agregue el código siguiente directamente después del código de que se agregó en el último paso.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="9b3bc-223">Creación de una dirección base para el servicio</span><span class="sxs-lookup"><span data-stu-id="9b3bc-223">Create a base address for the service</span></span>

<span data-ttu-id="9b3bc-224">Siguiendo el código que agregó en el último paso, cree una instancia de `Uri` para la dirección base del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="9b3bc-225">Este identificador URI especifica el esquema del Bus de servicio, el espacio de nombres y la ruta de acceso de la interfaz del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="9b3bc-226">"sb" es una abreviatura para el esquema de Bus de servicio e indica que se usa TCP como protocolo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="9b3bc-227">Esto también se indicó anteriormente en el archivo de configuración, cuando se especificó [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) como el enlace.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="9b3bc-228">Para este tutorial, el identificador URI es `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="9b3bc-229">Creación y configuración del host de servicios</span><span class="sxs-lookup"><span data-stu-id="9b3bc-229">Create and configure the service host</span></span>

1. <span data-ttu-id="9b3bc-230">Establezca el modo de conectividad a `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="9b3bc-231">El modo de conectividad describe el protocolo que usa el servicio para comunicarse con el servicio de retransmisión; HTTP o TCP.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="9b3bc-232">Con la configuración predeterminada `AutoDetect`, el servicio intenta conectarse a Azure Relay a través de TCP si está disponible, y HTTP si no lo está.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="9b3bc-233">Tenga en cuenta que esto difiere del protocolo que especifica el servicio para la comunicación del cliente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="9b3bc-234">Dicho protocolo viene determinado por el enlace utilizado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="9b3bc-235">Por ejemplo, un servicio puede usar el enlace [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx), que especifica que su punto de conexión se comunica con los clientes a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="9b3bc-236">Ese mismo servicio podría especificar **ConnectivityMode.AutoDetect** para que el servicio se comunique con Azure Relay mediante TCP.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="9b3bc-237">Cree el host del servicio, con el identificador URI creado anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="9b3bc-238">El host del servicio es el objeto de WCF que crea una instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="9b3bc-239">En este caso, se le pasa el tipo de servicio que quiere crear (un tipo `EchoService`) y también a la dirección en la que quiere exponer el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="9b3bc-240">En la parte superior del archivo Program.cs, agregue referencias a [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) y [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="9b3bc-241">De nuevo en `Main()`, configure el punto de conexión para permitir el acceso público.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="9b3bc-242">En este paso se informa al servicio de retransmisión de que la aplicación se puede encontrar públicamente al examinar la fuente ATOM del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="9b3bc-243">Si establece **DiscoveryType** en **privada**, un cliente podría seguir teniendo acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="9b3bc-244">Sin embargo, el servicio no aparecería cuando buscase el espacio de nombres de Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="9b3bc-245">En su lugar, el cliente tendría que conocer de antemano la ruta de acceso del extremo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="9b3bc-246">Aplique las credenciales de servicio a los extremos de servicio definidos en el archivo App.config:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="9b3bc-247">Como se indicó en el paso anterior, podría haber declarado varios servicios y extremos en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="9b3bc-248">Si lo hubiera hecho, este código recorrería el archivo de configuración y buscaría todos los extremos a los que se deban aplicar las credenciales.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="9b3bc-249">Sin embargo, para este tutorial, el archivo de configuración tiene un solo extremo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="9b3bc-250">Apertura del host de servicios</span><span class="sxs-lookup"><span data-stu-id="9b3bc-250">Open the service host</span></span>

1. <span data-ttu-id="9b3bc-251">Abra el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="9b3bc-252">Informe al usuario de que se está ejecutando el servicio y explíquele cómo cerrarlo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="9b3bc-253">Cuando termine, cierre el host del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="9b3bc-254">Presione **Ctrl+Mayús+B** para compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="9b3bc-255">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-255">Example</span></span>

<span data-ttu-id="9b3bc-256">El código de servicio completado debería tener el siguiente formato.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="9b3bc-257">En el código se incluye el contrato de servicio y la implementación de los pasos anteriores del tutorial. Además, hospeda el servicio en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

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

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="9b3bc-258">Crear un cliente WCF para el contrato de servicio</span><span class="sxs-lookup"><span data-stu-id="9b3bc-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="9b3bc-259">El siguiente paso consiste en crear una aplicación cliente y definir el contrato de servicio que se implementará en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="9b3bc-260">Tenga en cuenta que muchos de estos pasos son similares a los que se usaron para crear un servicio: definir un contrato, editar un archivo App.config, usar credenciales para conectarse al servicio de retransmisión, etc.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="9b3bc-261">El código utilizado para estas tareas se proporciona en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="9b3bc-262">Cree un nuevo proyecto en la solución actual de Visual Studio para el cliente mediante los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="9b3bc-263">En el Explorador de soluciones, en la misma solución que contenga el servicio, haga clic con el botón derecho en la solución actual (no el proyecto) y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="9b3bc-264">Después, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="9b3bc-265">En el cuadro de diálogo **Agregar nuevo proyecto**, haga clic en **Visual C#** (si **Visual C#** no aparece, mire en **Otros lenguajes**), seleccione la plantilla **Aplicación de consola (.NET Framework)** y asígnele el nombre **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="9b3bc-266">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="9b3bc-267">En el Explorador de soluciones, haga doble clic en el archivo Program.cs del proyecto **EchoClient** para abrirlo en el editor en caso de que no esté ya abierto.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="9b3bc-268">Cambie el nombre del espacio de nombres de su nombre predeterminado de `EchoClient` a `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="9b3bc-269">Instale el [paquete NuGet de Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus): en el Explorador de soluciones, haga clic con el botón derecho en el proyecto **EchoClient** y luego haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="9b3bc-270">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="9b3bc-271">Haga clic en **Instalar**y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="9b3bc-272">Agregue una instrucción `using` para el espacio de nombres [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) en el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="9b3bc-273">Agregue la definición del contrato de servicio al espacio de nombres, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="9b3bc-274">Tenga en cuenta que esta definición es idéntica a la definición que se usa en el proyecto **Service**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="9b3bc-275">Debe agregar este código en la parte superior del espacio de nombres `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="9b3bc-276">Presione **Ctrl+Shift+B** para compilar el cliente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="9b3bc-277">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-277">Example</span></span>

<span data-ttu-id="9b3bc-278">En el código siguiente se muestra el estado actual del archivo Program.cs en el proyecto **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

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

## <a name="configure-the-wcf-client"></a><span data-ttu-id="9b3bc-279">Configurar el cliente de WCF</span><span class="sxs-lookup"><span data-stu-id="9b3bc-279">Configure the WCF client</span></span>

<span data-ttu-id="9b3bc-280">En este paso, creará un archivo App.config para una aplicación cliente básica que accede al servicio creado anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="9b3bc-281">Este archivo App.config define el contrato, el enlace y el nombre del extremo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="9b3bc-282">El código utilizado para estas tareas se proporciona en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="9b3bc-283">En el Explorador de soluciones, en el proyecto **EchoClient**, haga doble clic en **App.config** para abrir el archivo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="9b3bc-284">En el elemento `<appSettings>`, reemplace los marcadores de posición con el nombre de su espacio de nombres de servicio y la clave SAS que copió en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="9b3bc-285">Dentro del elemento system.serviceModel, agregue un elemento `<client>`.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="9b3bc-286">En este paso se declara que está definiendo una aplicación cliente de estilo WCF.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="9b3bc-287">Dentro del elemento `client`, defina el nombre, el contrato y el tipo de enlace para el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="9b3bc-288">En este paso se define el nombre del punto de conexión, el contrato definido en el servicio y el hecho de que la aplicación cliente use TCP para comunicarse con Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="9b3bc-289">El nombre del extremo se usa en el paso siguiente para vincular la configuración de este extremo con el identificador URI del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="9b3bc-290">Haga clic en **Archivo** y luego en **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="9b3bc-291">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-291">Example</span></span>

<span data-ttu-id="9b3bc-292">En el código siguiente se muestra el archivo App.config del cliente de eco.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-292">The following code shows the App.config file for the Echo client.</span></span>

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

## <a name="implement-the-wcf-client"></a><span data-ttu-id="9b3bc-293">Implementación del cliente de WCF</span><span class="sxs-lookup"><span data-stu-id="9b3bc-293">Implement the WCF client</span></span>
<span data-ttu-id="9b3bc-294">En este paso, implementará una aplicación cliente básica que accede al servicio que creó anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="9b3bc-295">De forma similar al servicio, el cliente realiza muchas de las mismas operaciones para acceder a Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="9b3bc-296">Establece el modo de conectividad.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="9b3bc-297">Crea el identificador URI que localiza el servicio de host.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="9b3bc-298">Define las credenciales de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="9b3bc-299">Aplica a las credenciales para la conexión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="9b3bc-300">Abre la conexión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-300">Opens the connection.</span></span>
6. <span data-ttu-id="9b3bc-301">Realiza las tareas específicas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="9b3bc-302">Cierra la conexión.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-302">Closes the connection.</span></span>

<span data-ttu-id="9b3bc-303">Sin embargo, una de las principales diferencias es que la aplicación cliente usa un canal para conectarse al servicio de retransmisión, mientras que el servicio utiliza una llamada a **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="9b3bc-304">El código utilizado para estas tareas se proporciona en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="9b3bc-305">Implementación de una aplicación cliente</span><span class="sxs-lookup"><span data-stu-id="9b3bc-305">Implement a client application</span></span>
1. <span data-ttu-id="9b3bc-306">Establezca el modo de conectividad en **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="9b3bc-307">Agregue el código siguiente dentro del método `Main()` de la aplicación **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="9b3bc-308">Defina variables para contener los valores del espacio de nombres del servicio y la clave SAS que se leen desde la consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="9b3bc-309">Cree el identificador URI que define la ubicación del host en el proyecto de Relay.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="9b3bc-310">Cree el objeto de credenciales para el extremo del espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="9b3bc-311">Cree el generador de canales que carga la configuración que se describe en el archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="9b3bc-312">Un generador de canales es un objeto de WCF que crea un canal a través del cual se comunican las aplicaciones cliente y de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="9b3bc-313">Aplique las credenciales.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="9b3bc-314">Cree y abra el canal al servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="9b3bc-315">Escriba la interfaz de usuario básica y la funcionalidad del eco.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

    <span data-ttu-id="9b3bc-316">Tenga en cuenta que el código usa la instancia del objeto de canal como un proxy para el servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="9b3bc-317">Cierre el canal y el generador.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="9b3bc-318">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9b3bc-318">Example</span></span>

<span data-ttu-id="9b3bc-319">El código completado debería tener el siguiente formato y mostrar cómo crear una aplicación cliente, cómo llamar a las operaciones del servicio y cómo cerrar el cliente cuando finaliza la llamada a la operación.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

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

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

## <a name="run-the-applications"></a><span data-ttu-id="9b3bc-320">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9b3bc-320">Run the applications</span></span>

1. <span data-ttu-id="9b3bc-321">Presione **Ctrl+Mayús+B** para compilar la solución.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="9b3bc-322">Esto compila el proyecto de cliente y el proyecto de servicio que creó en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="9b3bc-323">Antes de ejecutar la aplicación cliente, debe asegurarse de que se está ejecutando la aplicación del servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="9b3bc-324">En el Explorador de soluciones en Visual Studio, haga clic con el botón derecho en la solución **EchoService** y después haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="9b3bc-325">En el cuadro de diálogo de propiedades de la solución haga clic en **Proyecto de inicio** y después haga clic en el botón **Proyectos de inicio múltiples**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="9b3bc-326">Asegúrese de que **EchoService** aparece en primer lugar en la lista.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="9b3bc-327">Defina el cuadro **Acción** para los proyectos **EchoService** y **EchoClient** en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="9b3bc-328">Haga clic en **Dependencias del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="9b3bc-329">En el cuadro **Proyectos**, seleccione **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="9b3bc-330">En el cuadro **Depende de:**, asegúrese de que **EchoService** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="9b3bc-331">Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="9b3bc-332">Presione **F5** para ejecutar ambos proyectos.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="9b3bc-333">Ambas ventanas de consola se abrirán y le solicitarán el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="9b3bc-334">Primero debe ejecutarse el servicio, por ello, en la ventana de la consola de **EchoService** escriba el espacio de nombres y después presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="9b3bc-335">A continuación, se le solicitará su clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="9b3bc-336">Escríbala y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="9b3bc-337">Este un ejemplo del resultado de la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-337">Here is example output from the console window.</span></span> <span data-ttu-id="9b3bc-338">Tenga en cuenta que los valores que se proporcionan aquí se ofrecen solamente como un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="9b3bc-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="9b3bc-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="9b3bc-340">La aplicación del servicio imprime en la ventana de la consola la dirección en la que está escuchando, tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="9b3bc-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="9b3bc-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="9b3bc-342">En la ventana de la consola de **EchoClient** escriba la misma información que especificó anteriormente para la aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="9b3bc-343">Siga los pasos anteriores para especificar los mismos valores de espacio de nombres de servicio y clave SAS para la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="9b3bc-344">Tras especificar estos valores, el cliente abrirá un canal al servicio y se le solicitará que escriba algo de texto, como se muestra en el siguiente ejemplo de salida de consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="9b3bc-345">Escriba algo de texto para enviarlo a la aplicación de servicio y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="9b3bc-346">Este texto se enviará al servicio a través de la operación de servicio de eco y aparecerá en la ventana de la consola del servicio, como se muestra en el siguiente ejemplo de salida.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="9b3bc-347">La aplicación cliente recibe el valor devuelto de la operación `Echo`, que es el texto original, y lo imprime en la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="9b3bc-348">A continuación se muestra un ejemplo del resultado de la ventana de consola del cliente.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="9b3bc-349">Puede continuar enviando mensajes de texto desde el cliente al servicio de esta manera.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="9b3bc-350">Cuando haya terminado, presione ENTRAR en las ventanas de las consolas del cliente y el servicio para finalizar ambas aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b3bc-351">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b3bc-351">Next steps</span></span>

<span data-ttu-id="9b3bc-352">En este tutorial se ha mostrado cómo crear un servicio y una aplicación cliente de Azure Relay mediante las funcionalidades de WCF Relay de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="9b3bc-353">Para ver un tutorial parecido donde se usa [mensajería de Service Bus](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), consulte [Introducción a las colas de Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="9b3bc-354">Para más información sobre Azure Relay, consulte los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="9b3bc-355">Información general sobre la arquitectura de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="9b3bc-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="9b3bc-356">Introducción a Azure Relay</span><span class="sxs-lookup"><span data-stu-id="9b3bc-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="9b3bc-357">Uso de WCF Relay de Service Bus con .NET</span><span class="sxs-lookup"><span data-stu-id="9b3bc-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
