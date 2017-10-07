---
title: "tutorial de REST de Bus de aaaService mediante retransmisión de Azure | Documentos de Microsoft"
description: "Cree una sencilla aplicación host de Azure Service Bus Relay que expone una interfaz basada en REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="45494-103">Tutorial de REST de Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="45494-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="45494-104">Este tutorial describe cómo toobuild una retransmisión de Azure simple hospedar la aplicación que expone una interfaz basada en REST.</span><span class="sxs-lookup"><span data-stu-id="45494-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="45494-105">REST permite que un cliente web, como un explorador web, hello tooaccess solicitudes de API de Bus de servicio a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="45494-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="45494-106">tutorial de Hello usa tooconstruct modelo programación Hola REST de Windows Communication Foundation (WCF) un servicio REST en el Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="45494-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="45494-107">Para obtener más información, consulte [el modelo de programación de REST de WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) y [diseñar e implementar servicios](/dotnet/framework/wcf/designing-and-implementing-services) Hola documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="45494-108">Paso 1: Crear un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="45494-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="45494-109">usar toobegin Hola características de retransmisión en Azure, primero debe crear un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="45494-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="45494-110">Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45494-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="45494-111">Siga hello [instrucciones a continuación](relay-create-namespace-portal.md) toocreate un espacio de nombres de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="45494-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="45494-112">Paso 2: Definir una toouse de contrato de servicio WCF basado en REST con retransmisión de Azure</span><span class="sxs-lookup"><span data-stu-id="45494-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="45494-113">Cuando se crea un servicio basado en REST WCF, debe definir el contrato de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="45494-114">contrato de Hello especifica qué operaciones Hola admite el host.</span><span class="sxs-lookup"><span data-stu-id="45494-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="45494-115">Una operación de servicio puede considerarse como un método de servicio web.</span><span class="sxs-lookup"><span data-stu-id="45494-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="45494-116">Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="45494-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="45494-117">Cada método de interfaz de hello corresponde tooa operación del servicio concreta.</span><span class="sxs-lookup"><span data-stu-id="45494-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="45494-118">Hola [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) atributo debe ser interfaz tooeach aplicados y Hola [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) atributo debe ser una operación tooeach aplicada.</span><span class="sxs-lookup"><span data-stu-id="45494-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="45494-119">Si un método en una interfaz que tiene hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) no tiene hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), que no se expone el método.</span><span class="sxs-lookup"><span data-stu-id="45494-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="45494-120">código de Hello utilizado para estas tareas se muestra en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="45494-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="45494-121">Hello diferencia principal entre un contrato de WCF y un contrato basado en REST es adición de Hola de una propiedad toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="45494-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="45494-122">Esta propiedad permite toomap un método en el método de interfaz tooa en hello otro lado de la interfaz de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="45494-123">En este caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink un tooHTTP método GET.</span><span class="sxs-lookup"><span data-stu-id="45494-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="45494-124">Esto permite que el Bus de servicio tooaccurately recuperar e interpretar comandos enviados toohello interfaz.</span><span class="sxs-lookup"><span data-stu-id="45494-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="45494-125">toocreate un contrato con una interfaz</span><span class="sxs-lookup"><span data-stu-id="45494-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="45494-126">Abra Visual Studio como administrador: programa Hola de menú contextual en hello **iniciar** menú y, a continuación, haga clic en **ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="45494-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="45494-127">Cree un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="45494-127">Create a new console application project.</span></span> <span data-ttu-id="45494-128">Haga clic en hello **archivo** menú y seleccione **New**, a continuación, seleccione **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="45494-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="45494-129">Hola **nuevo proyecto** cuadro de diálogo, haga clic en **Visual C#**, seleccione hello **aplicación de consola** plantilla y asígnele el nombre **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="45494-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="45494-130">Usar valor predeterminado de hello **ubicación**.</span><span class="sxs-lookup"><span data-stu-id="45494-130">Use hello default **Location**.</span></span> <span data-ttu-id="45494-131">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="45494-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="45494-132">Para un proyecto de C#, Visual Studio crea un archivo `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="45494-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="45494-133">Esta clase contiene vacío `Main()` método, necesario para un toobuild de proyecto de aplicación de consola correctamente.</span><span class="sxs-lookup"><span data-stu-id="45494-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="45494-134">Agregar referencias tooService Bus y **System.ServiceModel.dll** toohello proyecto mediante la instalación de paquetes de NuGet de Bus de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="45494-135">Este paquete agrega automáticamente referencias toohello Service Bus bibliotecas, así como Hola WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="45494-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="45494-136">En el Explorador de soluciones, haga clic en hello **ImageListener** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="45494-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="45494-137">Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="45494-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="45494-138">Haga clic en **instalar**y acepte los términos de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="45494-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="45494-139">Debe agregar explícitamente una referencia**System.ServiceModel.Web.dll** toohello proyecto:</span><span class="sxs-lookup"><span data-stu-id="45494-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="45494-140">a.</span><span class="sxs-lookup"><span data-stu-id="45494-140">a.</span></span> <span data-ttu-id="45494-141">En el Explorador de soluciones, haga clic en hello **referencias** carpeta bajo la carpeta del proyecto de hello y, a continuación, haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="45494-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="45494-142">b.</span><span class="sxs-lookup"><span data-stu-id="45494-142">b.</span></span> <span data-ttu-id="45494-143">Hola **Agregar referencia** diálogo cuadro, haga clic en hello **Framework** pestaña en el lado izquierdo de Hola y Hola **búsqueda** , escriba **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="45494-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="45494-144">Seleccione hello **System.ServiceModel.Web** casilla de verificación, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="45494-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="45494-145">Agregue los siguiente hello `using` las instrucciones en la parte superior de hello del archivo Program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="45494-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres de Hola que habilita el acceso mediante programación toobasic características de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="45494-147">Retransmisión de WCF usa muchos de los objetos de Hola y atributos de contratos de servicio WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="45494-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="45494-148">Usará este espacio de nombres en la mayoría de las aplicaciones de Relay.</span><span class="sxs-lookup"><span data-stu-id="45494-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="45494-149">De forma similar, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ayuda a define canal hello, que es objeto de Hola a través del cual se comunica con el explorador web del cliente hello y retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="45494-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="45494-150">Por último, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene tipos de Hola que le permiten aplicaciones basadas en web de toocreate.</span><span class="sxs-lookup"><span data-stu-id="45494-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="45494-151">Cambiar el nombre de hello `ImageListener` espacio de nombres demasiado**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="45494-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="45494-152">Directamente después de hello Abrir llave de apertura de la declaración de espacio de nombres de hello, defina una nueva interfaz denominada **IImageContract** y aplicar hello **ServiceContractAttribute** interfaz toohello de atributo con un valor de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="45494-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="45494-153">valor de espacio de nombres de Hello difiere del espacio de nombres de Hola que utilizas en ámbito de hello del código.</span><span class="sxs-lookup"><span data-stu-id="45494-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="45494-154">valor de espacio de nombres de Hola se utiliza como un identificador único para este contrato y debe tener información de versión.</span><span class="sxs-lookup"><span data-stu-id="45494-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="45494-155">Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="45494-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="45494-156">Especificar explícitamente el espacio de nombres de hello, impide que valor de espacio de nombres predeterminado de Hola se agreguen toohello el nombre del contrato.</span><span class="sxs-lookup"><span data-stu-id="45494-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="45494-157">Dentro de hello `IImageContract` de la interfaz, declare un método para Hola Hola de operación único `IImageContract` contrato expone Hola interfaz y aplique hello `OperationContractAttribute` atributo método toohello que desea tooexpose como parte de hello público Service Bus contrato.</span><span class="sxs-lookup"><span data-stu-id="45494-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="45494-158">Hola **OperationContract** atributo, agregue hello **WebGet** valor.</span><span class="sxs-lookup"><span data-stu-id="45494-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="45494-159">Si lo hace, habilita Hola tooroute de servicio de retransmisión HTTP GET solicita demasiado`GetImage`, hello tootranslate devolver valores de y `GetImage` en una respuesta GETRESPONSE de HTTP.</span><span class="sxs-lookup"><span data-stu-id="45494-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="45494-160">Más adelante en el tutorial de hello, utilizará un tooaccess de explorador web este método y la imagen de toodisplay hello en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="45494-161">Directamente después de hello `IImageContract` definición, declare un canal que herede de ambos hello `IImageContract` y `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="45494-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="45494-162">Un canal es objeto WCF de Hola a través del cual cliente y servicio de hello pasan información tooeach otras.</span><span class="sxs-lookup"><span data-stu-id="45494-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="45494-163">Más adelante, creará el canal de hello en la aplicación host.</span><span class="sxs-lookup"><span data-stu-id="45494-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="45494-164">Retransmisión de Azure, a continuación, utiliza este canal toopass hello las solicitudes HTTP GET desde Hola explorador tooyour **GetImage** implementación.</span><span class="sxs-lookup"><span data-stu-id="45494-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="45494-165">retransmisión de Hello también utiliza Hola Hola de tootake canal **GetImage** valor devuelto y lo traduce a un GETRESPONSE de HTTP para el explorador del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="45494-166">De hello **generar** menú, haga clic en **generar solución** precisión de hello tooconfirm de su trabajo hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="45494-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="45494-167">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="45494-167">Example</span></span>
<span data-ttu-id="45494-168">Hola siguiente código muestra una interfaz básica que define un contrato de retransmisión de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="45494-169">Paso 3: Implementar un contrato de servicio WCF basado en REST toouse Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="45494-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="45494-170">Crear un servicio de retransmisión de WCF basado en REST requiere crear primero el contrato de hello, que se define mediante una interfaz.</span><span class="sxs-lookup"><span data-stu-id="45494-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="45494-171">Hola siguiente paso es interfaz de hello tooimplement.</span><span class="sxs-lookup"><span data-stu-id="45494-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="45494-172">Esto implica la creación de una clase denominada **ImageService** que implementa Hola definido por el usuario **IImageContract** interfaz.</span><span class="sxs-lookup"><span data-stu-id="45494-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="45494-173">Después de implementar el contrato de hello, a continuación, configurar interfaz hello mediante un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="45494-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="45494-174">archivo de configuración de Hello contiene información necesaria para la aplicación hello, como nombre de hello del servicio de hello, nombre de hello del contrato de Hola y tipo de Hola de protocolo que está toocommunicate usado con el servicio de retransmisión de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="45494-175">código de Hello utilizado para estas tareas se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="45494-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="45494-176">Como con los pasos anteriores de hello, hay muy pocas diferencias entre implementar un contrato basado en REST y un contrato de retransmisión de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="45494-177">contrato de Bus de servicio de tooimplement un estilo de REST</span><span class="sxs-lookup"><span data-stu-id="45494-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="45494-178">Crear una nueva clase denominada **ImageService** directamente después de la definición de Hola de hello **IImageContract** interfaz.</span><span class="sxs-lookup"><span data-stu-id="45494-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="45494-179">Hola **ImageService** clase implementa hello **IImageContract** interfaz.</span><span class="sxs-lookup"><span data-stu-id="45494-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="45494-180">Implementaciones de interfaz tooother similar, puede implementar definición hello en un archivo diferente.</span><span class="sxs-lookup"><span data-stu-id="45494-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="45494-181">Sin embargo, para este tutorial, la implementación de hello aparece en hello mismo archivo como definición de interfaz de Hola y `Main()` método.</span><span class="sxs-lookup"><span data-stu-id="45494-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="45494-182">Aplicar hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) atributo toohello **IImageService** tooindicate de clase que Hola clase es una implementación de un contrato de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="45494-183">Como se mencionó anteriormente, este espacio de nombres no es un espacio de nombres tradicional.</span><span class="sxs-lookup"><span data-stu-id="45494-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="45494-184">En su lugar, es parte de la arquitectura WCF que identifica el contrato de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="45494-185">Para obtener más información, vea hello [nombres de contrato de datos](https://msdn.microsoft.com/library/ms731045.aspx) tema Hola documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="45494-186">Agregue un proyecto de tooyour de imagen JPG.</span><span class="sxs-lookup"><span data-stu-id="45494-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="45494-187">Se trata de una imagen que muestra los servicios de hello en Hola recibir explorador.</span><span class="sxs-lookup"><span data-stu-id="45494-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="45494-188">Haga clic con el botón derecho en el proyecto y, después, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="45494-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="45494-189">A continuación, haga clic en **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="45494-189">Then click **Existing Item**.</span></span> <span data-ttu-id="45494-190">Hola de uso **Agregar elemento existente** tooan de toobrowse del cuadro de diálogo procede .jpg y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="45494-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="45494-191">Al agregar el archivo hello, asegúrese de que **todos los archivos** está seleccionado en hello lista desplegable siguiente toohello **nombre de archivo:** campo.</span><span class="sxs-lookup"><span data-stu-id="45494-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="45494-192">resto de Hola de este tutorial se da por supuesto que Hola nombre de imagen de hello es "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="45494-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="45494-193">Si tiene un archivo diferente, se dispone de toorename Hola imagen o cambiar su toocompensate de código.</span><span class="sxs-lookup"><span data-stu-id="45494-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="45494-194">seguro que Hola ejecutando el servicio puede encontrar el archivo de imagen de hello, en toomake **el Explorador de soluciones** haga clic en archivo de imagen de hello, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="45494-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="45494-195">Hola **propiedades** panel, establezca **copiar tooOutput directorio** demasiado**copiar si es posterior**.</span><span class="sxs-lookup"><span data-stu-id="45494-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="45494-196">Agregar una referencia toohello **System.Drawing.dll** toohello ensamblado del proyecto y agregue siguiente Hola asociados `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="45494-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="45494-197">Hola **ImageService** clase, agregue Hola después de constructor que carga Hola mapa de bits y prepara toosend se toohello explorador del cliente.</span><span class="sxs-lookup"><span data-stu-id="45494-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="45494-198">Directamente después de código anterior, hello, agregue Hola siguiente **GetImage** método Hola **ImageService** mensaje tooreturn HTTP de clase que contiene la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="45494-199">Esta implementación usa **MemoryStream** tooretrieve Hola imagen y prepararlo para la transmisión por secuencias toohello explorador.</span><span class="sxs-lookup"><span data-stu-id="45494-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="45494-200">Inicia la posición de la secuencia de hello en la posición cero, declara el contenido de la transmisión de hello como jpeg y transmite la información de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="45494-201">De hello **generar** menú, haga clic en **generar solución**.</span><span class="sxs-lookup"><span data-stu-id="45494-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="45494-202">configuración de hello toodefine para ejecutar el servicio web de hello en el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="45494-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="45494-203">En **el Explorador de soluciones**, haga doble clic en **App.config** tooopen en el editor de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="45494-204">Hola **App.config** archivo incluye el nombre del servicio hello, extremo (es decir, la ubicación de hello Azure retransmisión expone para que los clientes y hosts toocommunicate entre sí) y (Hola el tipo de protocolo que se usa toocommunicate) de enlace.</span><span class="sxs-lookup"><span data-stu-id="45494-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="45494-205">Hello principal diferencia reside en ese punto de conexión de servicio de hello configurado hace referencia tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) enlace.</span><span class="sxs-lookup"><span data-stu-id="45494-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="45494-206">Hola `<system.serviceModel>` XML es un elemento WCF que define uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="45494-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="45494-207">En este caso, es punto de conexión y el nombre de servicio de hello toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="45494-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="45494-208">Final Hola de hello `<system.serviceModel>` elemento (pero aún dentro `<system.serviceModel>`), agregue un `<bindings>` elemento que tiene Hola siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="45494-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="45494-209">Esto define los enlaces de hello utilizados en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="45494-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="45494-210">Puede definir varios enlaces, pero para este tutorial está definiendo solo uno.</span><span class="sxs-lookup"><span data-stu-id="45494-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="45494-211">código de Hello anterior define una retransmisión de WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) enlace con **relayClientAuthenticationType** establecido demasiado**ninguno**.</span><span class="sxs-lookup"><span data-stu-id="45494-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="45494-212">Este valor indica que un extremo que usa este enlace no requiere una credencial de cliente.</span><span class="sxs-lookup"><span data-stu-id="45494-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="45494-213">Después de hello `<bindings>` elemento, agregue un `<services>` elemento.</span><span class="sxs-lookup"><span data-stu-id="45494-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="45494-214">Enlaces toohello similares, puede definir varios servicios en un único archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="45494-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="45494-215">Sin embargo, para este tutorial, solo se define uno.</span><span class="sxs-lookup"><span data-stu-id="45494-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="45494-216">Este paso configura un servicio que utiliza predeterminado Hola definido anteriormente **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="45494-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="45494-217">También se utiliza de forma predeterminada hello **sbTokenProvider**, que se define en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="45494-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="45494-218">Después de hello `<services>` elemento, crear una `<behaviors>` elemento con hello siguen contenido, reemplazando "SAS_KEY" con hello *firma de acceso compartido* clave (SAS) que ha obtenido anteriormente de hello [portal de Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="45494-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="45494-219">Aún en un archivo App.config, Hola `<appSettings>` elemento, reemplace el valor de cadena de conexión completa de hello con cadena de conexión de hello obtenido previamente desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="45494-220">De hello **generar** menú, haga clic en **generar solución** toobuild Hola toda la solución.</span><span class="sxs-lookup"><span data-stu-id="45494-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="45494-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="45494-221">Example</span></span>
<span data-ttu-id="45494-222">Hello código siguiente muestra hello contrato e implementación del servicio para un servicio basado en REST que se ejecuta en el Bus de servicio con hello **WebHttpRelayBinding** enlace.</span><span class="sxs-lookup"><span data-stu-id="45494-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="45494-223">Hello en el ejemplo siguiente se muestra archivo App.config de hello asociado con el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="45494-224">Paso 4: Host Hola WCF basado en REST servicio toouse retransmisión de Azure</span><span class="sxs-lookup"><span data-stu-id="45494-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="45494-225">Este paso describe cómo toorun una web service con una aplicación de consola con la retransmisión de WCF.</span><span class="sxs-lookup"><span data-stu-id="45494-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="45494-226">Obtener una lista completa del código de hello escrito en este paso se proporciona en el ejemplo de Hola Hola procedimiento.</span><span class="sxs-lookup"><span data-stu-id="45494-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="45494-227">una dirección base para el servicio de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="45494-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="45494-228">Hola `Main()` declaración de función, cree un espacio de nombres de variable toostore Hola del proyecto.</span><span class="sxs-lookup"><span data-stu-id="45494-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="45494-229">Asegúrese de que tooreplace `yourNamespace` con nombre hello del espacio de nombres de retransmisión de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45494-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="45494-230">Bus de servicio usa nombre Hola de su toocreate de espacio de nombres un URI único.</span><span class="sxs-lookup"><span data-stu-id="45494-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="45494-231">Crear un `Uri` instancia para la dirección base Hola del servicio de Hola que se basa en el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="45494-232">toocreate y configurar el host del servicio web Hola</span><span class="sxs-lookup"><span data-stu-id="45494-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="45494-233">Crear el host del servicio web hello, con la dirección URI de hello creada anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="45494-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="45494-234">host de servicio de Hello es objeto WCF de Hola que crea una instancia de la aplicación de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="45494-235">En este ejemplo se pasa el tipo de saludo del host que desea toocreate (un **ImageService**), y también Hola dirección a la que desea que aplicación de host de tooexpose Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="45494-236">host de servicio web de toorun Hola</span><span class="sxs-lookup"><span data-stu-id="45494-236">toorun hello web service host</span></span>
1. <span data-ttu-id="45494-237">Abra el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="45494-238">Ahora se está ejecutando el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-238">hello service is now running.</span></span>
2. <span data-ttu-id="45494-239">Muestra un mensaje que indica que está ejecutando el servicio de Hola y cómo toostop Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="45494-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="45494-240">Cuando termine, cierre el host de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="45494-241">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="45494-241">Example</span></span>
<span data-ttu-id="45494-242">Hola siguiente ejemplo incluye contrato de servicio de Hola y la implementación de los pasos anteriores en el servicio de Hola de hello tutorial y hospeda en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="45494-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="45494-243">Compile Hola siguiente código en un archivo ejecutable denominado ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="45494-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="45494-244">Compilar código de hello</span><span class="sxs-lookup"><span data-stu-id="45494-244">Compiling hello code</span></span>
<span data-ttu-id="45494-245">Después de compilar la solución de hello, Hola después de la aplicación de hello toorun:</span><span class="sxs-lookup"><span data-stu-id="45494-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="45494-246">Presione **F5**, o busque la ubicación del archivo ejecutable toohello (ImageListener\bin\Debug\ImageListener.exe), servicio de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="45494-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="45494-247">Mantener Hola ejecutando la aplicación, tal y como se requería paso siguiente de tooperform Hola.</span><span class="sxs-lookup"><span data-stu-id="45494-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="45494-248">Copie y pegue la dirección de Hola Hola desde línea de comandos en una imagen de hello toosee de explorador.</span><span class="sxs-lookup"><span data-stu-id="45494-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="45494-249">Cuando haya terminado, presione **ENTRAR** en aplicación Hola de hello símbolo ventana tooclose.</span><span class="sxs-lookup"><span data-stu-id="45494-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45494-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45494-250">Next steps</span></span>
<span data-ttu-id="45494-251">Ahora que ha creado una aplicación que utiliza el servicio de retransmisión de Bus de servicio de hello, vea Hola siguiendo artículos toolearn más acerca de la retransmisión de Azure:</span><span class="sxs-lookup"><span data-stu-id="45494-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="45494-252">Información general sobre la arquitectura de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="45494-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="45494-253">Introducción a Azure Relay</span><span class="sxs-lookup"><span data-stu-id="45494-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="45494-254">Cómo el servicio con .NET de la retransmisión de hello toouse WCF</span><span class="sxs-lookup"><span data-stu-id="45494-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
