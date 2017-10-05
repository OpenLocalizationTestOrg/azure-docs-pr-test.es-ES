---
title: Tutorial de REST de Service Bus mediante Azure Relay | Microsoft Docs
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
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="61ac3-103">Tutorial de REST de Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="61ac3-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="61ac3-104">En este tutorial se describe cómo compilar una sencilla aplicación host de Azure Relay que expone una interfaz basada en REST.</span><span class="sxs-lookup"><span data-stu-id="61ac3-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="61ac3-105">REST permite a un cliente web, como un explorador web, tener acceso a la API de Bus de servicio a través de solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="61ac3-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="61ac3-106">En este tutorial se usa el modelo de programación REST de Windows Communication Foundation (WCF) para construir un servicio REST de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="61ac3-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="61ac3-107">Para obtener más información, vea [Modelo de programación REST de WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) y [Diseño e implementación de servicios](/dotnet/framework/wcf/designing-and-implementing-services) en la documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="61ac3-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="61ac3-108">Paso 1: Crear un espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="61ac3-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="61ac3-109">Para comenzar a usar las características de Relay en Azure, primero debe crear un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="61ac3-110">Un espacio de nombres proporciona un contenedor con un ámbito para el desvío de recursos de Azure en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61ac3-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="61ac3-111">Siga [estas instrucciones](relay-create-namespace-portal.md) para crear un espacio de nombres de Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="61ac3-112">Paso 2: Definir un contrato de servicio de WCF basado en REST para utilizar con Azure Relay</span><span class="sxs-lookup"><span data-stu-id="61ac3-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="61ac3-113">Cuando se crea un servicio WCF de tipo REST, debe definir el contrato.</span><span class="sxs-lookup"><span data-stu-id="61ac3-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="61ac3-114">El contrato especifica qué operaciones admite el host.</span><span class="sxs-lookup"><span data-stu-id="61ac3-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="61ac3-115">Una operación de servicio puede considerarse como un método de servicio web.</span><span class="sxs-lookup"><span data-stu-id="61ac3-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="61ac3-116">Los contratos se crean mediante la definición de una interfaz de C++, C# o Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="61ac3-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="61ac3-117">Cada método de la interfaz corresponde a una operación de servicio específica.</span><span class="sxs-lookup"><span data-stu-id="61ac3-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="61ac3-118">El atributo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) se debe aplicar a cada interfaz, y el atributo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) se debe aplicar a cada operación.</span><span class="sxs-lookup"><span data-stu-id="61ac3-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="61ac3-119">Si un método en una interfaz que tiene [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) no tiene [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), ese método no se expone.</span><span class="sxs-lookup"><span data-stu-id="61ac3-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="61ac3-120">El código utilizado para estas tareas se muestra en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="61ac3-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="61ac3-121">La diferencia principal entre un contrato de WCF y un contrato de estilo REST es la adición de una propiedad a [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="61ac3-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="61ac3-122">Esta propiedad permite asignar un método de la interfaz a un método en el otro lado de la interfaz.</span><span class="sxs-lookup"><span data-stu-id="61ac3-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="61ac3-123">En este caso, usaremos [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) para vincular un método a HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="61ac3-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="61ac3-124">Esto permite al Bus de servicio recuperar e interpretar con precisión los comandos enviados a la interfaz.</span><span class="sxs-lookup"><span data-stu-id="61ac3-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="61ac3-125">Para crear un contrato con una interfaz</span><span class="sxs-lookup"><span data-stu-id="61ac3-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="61ac3-126">Abra Visual Studio como administrador: haga clic con el botón derecho en el programa en el menú **Inicio** y después haga clic en **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="61ac3-127">Cree un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="61ac3-127">Create a new console application project.</span></span> <span data-ttu-id="61ac3-128">Haga clic en el menú **Archivo**, seleccione **Nuevo** y después **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="61ac3-129">En el cuadro de diálogo **Nuevo proyecto**, haga clic en **Visual C#**, seleccione la plantilla **Aplicación de consola** y asígnele el nombre **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="61ac3-130">Use la **Ubicación** predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61ac3-130">Use the default **Location**.</span></span> <span data-ttu-id="61ac3-131">Haga clic en **Aceptar** para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="61ac3-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="61ac3-132">Para un proyecto de C#, Visual Studio crea un archivo `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="61ac3-133">Esta clase contiene un método `Main()` vacío, necesario para que un proyecto de aplicación de consola se compile correctamente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="61ac3-134">Agregue referencias a Service Bus y **System.ServiceModel.dll** al proyecto instalando el paquete NuGet de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="61ac3-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="61ac3-135">Este paquete agrega automáticamente referencias a las bibliotecas de Service Bus, así como a **System.ServiceModel** de WCF.</span><span class="sxs-lookup"><span data-stu-id="61ac3-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="61ac3-136">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto **ImageListener** y haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="61ac3-137">Haga clic en la pestaña **Examinar** y luego busque `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="61ac3-138">Haga clic en **Instalar**y acepte las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="61ac3-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="61ac3-139">Debe agregar explícitamente una referencia a **System.ServiceModel.Web.dll** en el proyecto:</span><span class="sxs-lookup"><span data-stu-id="61ac3-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="61ac3-140">a.</span><span class="sxs-lookup"><span data-stu-id="61ac3-140">a.</span></span> <span data-ttu-id="61ac3-141">En el Explorador de soluciones, haga clic en la carpeta **Referencias** bajo la carpeta del proyecto y después haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="61ac3-142">b.</span><span class="sxs-lookup"><span data-stu-id="61ac3-142">b.</span></span> <span data-ttu-id="61ac3-143">En el cuadro de diálogo **Agregar referencia**, haga clic en la pestaña **Marco** a la izquierda y, en el cuadro **Buscar**, escriba **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="61ac3-144">Active la casilla **System.ServiceModel.Web** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="61ac3-145">Agregue las siguientes instrucciones `using` al principio del archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="61ac3-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="61ac3-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) es el espacio de nombres que permite el acceso mediante programación a las características básicas de WCF.</span><span class="sxs-lookup"><span data-stu-id="61ac3-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="61ac3-147">WCF Relay utiliza muchos de los objetos y atributos de WCF para definir contratos de servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="61ac3-148">Usará este espacio de nombres en la mayoría de las aplicaciones de Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="61ac3-149">De forma similar, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) ayuda a definir el canal, que es el objeto a través del cual se comunica con Azure Relay y el explorador web del cliente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="61ac3-150">Por último, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contiene los tipos que permiten crear aplicaciones basadas en web.</span><span class="sxs-lookup"><span data-stu-id="61ac3-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="61ac3-151">Cambie el nombre del espacio de nombres `ImageListener` a **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="61ac3-152">Inmediatamente después de la llave de apertura de la declaración del espacio de nombres, defina una nueva interfaz denominada **IImageContract** y aplique el atributo **ServiceContractAttribute** a la interfaz con un valor de `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="61ac3-153">El valor del espacio de nombres difiere del espacio de nombres que utiliza en todo el ámbito de su código.</span><span class="sxs-lookup"><span data-stu-id="61ac3-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="61ac3-154">El valor del espacio de nombres se utiliza como identificador único para este contrato, y debe tener información de la versión.</span><span class="sxs-lookup"><span data-stu-id="61ac3-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="61ac3-155">Para obtener más información, vea [Control de versiones del servicio](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="61ac3-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="61ac3-156">La especificación del espacio de nombres impide explícitamente que el valor del espacio de nombres predeterminado se agregue al nombre del contrato.</span><span class="sxs-lookup"><span data-stu-id="61ac3-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="61ac3-157">Dentro de la interfaz `IImageContract`, declare un método para la operación sencilla que el contrato `IImageContract` expone en la interfaz y aplique el atributo `OperationContractAttribute` al método que desea exponer como parte del contrato público del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="61ac3-158">En el atributo **OperationContract**, agregue el valor **WebGet**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="61ac3-159">Al hacerlo, permite que el servicio Relay enrute las solicitudes HTTP GET a `GetImage` y convierta los valores devueltos de `GetImage` en una respuesta HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="61ac3-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="61ac3-160">Más adelante en el tutorial, utilizará un explorador web para tener acceso a este método y mostrar la imagen en el explorador.</span><span class="sxs-lookup"><span data-stu-id="61ac3-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="61ac3-161">Inmediatamente después de la definición `IImageContract`, declare un canal que herede de las interfaces `IImageContract` y `IClientChannel`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="61ac3-162">Un canal es el objeto de WCF a través del cual el servicio y el cliente se pasan información entre sí.</span><span class="sxs-lookup"><span data-stu-id="61ac3-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="61ac3-163">Más adelante, creará el canal en su aplicación host.</span><span class="sxs-lookup"><span data-stu-id="61ac3-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="61ac3-164">Azure Relay usa después este canal para pasar las solicitudes HTTP GET del explorador a su implementación **GetImage**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="61ac3-165">El servicio Relay también usa el canal para tomar el valor devuelto de **GetImage** y convertirlo en HTTP GETRESPONSE para el explorador del cliente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="61ac3-166">En el menú **Compilar**, haga clic en **Compilar solución** para confirmar la precisión del trabajo realizado hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="61ac3-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="61ac3-167">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="61ac3-167">Example</span></span>
<span data-ttu-id="61ac3-168">En el ejemplo de código siguiente se muestra una interfaz básica que define un contrato de WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="61ac3-169">Paso 3: Implementar un contrato de servicio de WCF basado en REST para usar el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="61ac3-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="61ac3-170">La creación de un servicio WCF Relay de estilo REST requiere que se cree primero el contrato, que se define mediante una interfaz.</span><span class="sxs-lookup"><span data-stu-id="61ac3-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="61ac3-171">El siguiente paso es implementar la interfaz.</span><span class="sxs-lookup"><span data-stu-id="61ac3-171">The next step is to implement the interface.</span></span> <span data-ttu-id="61ac3-172">Esto implica la creación de una clase denominada **ImageService** que implementa la interfaz **IImageContract** definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="61ac3-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="61ac3-173">Después de implementar el contrato, a continuación se configura la interfaz usando un archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="61ac3-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="61ac3-174">El archivo de configuración contiene la información necesaria para la aplicación, como el nombre del servicio, el nombre del contrato y el tipo de protocolo que se utiliza para comunicarse con el servicio Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="61ac3-175">El código utilizado para estas tareas se proporciona en el ejemplo que sigue al procedimiento.</span><span class="sxs-lookup"><span data-stu-id="61ac3-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="61ac3-176">Al igual que con los pasos anteriores, hay muy pocas diferencias entre implementar un contrato de estilo REST y un contrato de WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="61ac3-177">Para implementar un contrato de Bus de servicio de estilo REST</span><span class="sxs-lookup"><span data-stu-id="61ac3-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="61ac3-178">Cree una nueva clase denominada **ImageService** directamente después de la definición de la interfaz **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="61ac3-179">La clase **ImageService** implementa la interfaz **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="61ac3-180">Al igual que otras implementaciones de interfaz, puede implementar la definición en un archivo diferente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="61ac3-181">Sin embargo, para este tutorial, la implementación aparece en el mismo archivo que la definición de interfaz y el método `Main()`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="61ac3-182">Aplique el atributo [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) a la clase **IImageService** para indicar que la clase es una implementación de un contrato de WCF.</span><span class="sxs-lookup"><span data-stu-id="61ac3-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="61ac3-183">Como se mencionó anteriormente, este espacio de nombres no es un espacio de nombres tradicional.</span><span class="sxs-lookup"><span data-stu-id="61ac3-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="61ac3-184">Más bien, forma parte de la arquitectura de WCF que identifica el contrato.</span><span class="sxs-lookup"><span data-stu-id="61ac3-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="61ac3-185">Para más información, vea el tema [Nombres de contratos de datos](https://msdn.microsoft.com/library/ms731045.aspx) en la documentación de WCF.</span><span class="sxs-lookup"><span data-stu-id="61ac3-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="61ac3-186">Agregue una imagen .jpg al proyecto.</span><span class="sxs-lookup"><span data-stu-id="61ac3-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="61ac3-187">Se trata de una imagen que el servicio muestra en el explorador de recepción.</span><span class="sxs-lookup"><span data-stu-id="61ac3-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="61ac3-188">Haga clic con el botón derecho en el proyecto y, después, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="61ac3-189">A continuación, haga clic en **Elemento existente**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-189">Then click **Existing Item**.</span></span> <span data-ttu-id="61ac3-190">Utilice el cuadro de diálogo **Agregar elemento existente** para buscar un .jpg adecuado y después haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="61ac3-191">Al agregar el archivo, asegúrese de que está seleccionada la opción **Todos los archivos** en la lista desplegable situada junto al campo **Nombre de archivo:**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="61ac3-192">En el resto de este tutorial se supone que el nombre de la imagen es "image.jpg".</span><span class="sxs-lookup"><span data-stu-id="61ac3-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="61ac3-193">Si tiene un archivo diferente, debe cambiar el nombre de la imagen o cambiar su código para compensar.</span><span class="sxs-lookup"><span data-stu-id="61ac3-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="61ac3-194">Para asegurarse de que el servicio en ejecución pueda encontrar el archivo de imagen, en el **Explorador de soluciones**, haga clic con el botón derecho en dicho archivo y luego en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="61ac3-195">En el panel **Propiedades**, establezca **Copiar en el directorio de salida** en **Copiar si es posterior**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="61ac3-196">Agregue una referencia al ensamblado **System.Drawing.dll** al proyecto, además de las siguientes instrucciones `using` asociadas.</span><span class="sxs-lookup"><span data-stu-id="61ac3-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="61ac3-197">En la clase **ImageService**, agregue el siguiente constructor que carga el mapa de bits y se prepara para enviarlo al explorador del cliente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="61ac3-198">Directamente después del código anterior, agregue el siguiente método **GetImage** en la clase **ImageService** para devolver un mensaje HTTP que contiene la imagen.</span><span class="sxs-lookup"><span data-stu-id="61ac3-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="61ac3-199">Esta implementación usa **MemoryStream** para recuperar la imagen y prepararla para el streaming al explorador.</span><span class="sxs-lookup"><span data-stu-id="61ac3-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="61ac3-200">Este inicia la posición de la secuencia en cero, declara el contenido de la secuencia como jpeg y transmite la información.</span><span class="sxs-lookup"><span data-stu-id="61ac3-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="61ac3-201">En el menú **Compilar**, haga clic en **Compilar solución**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="61ac3-202">Para definir la configuración para ejecutar el servicio web en el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="61ac3-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="61ac3-203">En el **Explorador de soluciones**, haga doble clic en **App.config** para abrirlo en el editor de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="61ac3-204">El archivo **App.config** incluye el nombre del servicio, el punto de conexión (es decir, la ubicación que Azure Relay expone para que clientes y hosts se comuniquen entre sí) y el enlace (el tipo de protocolo que se usa para la comunicación).</span><span class="sxs-lookup"><span data-stu-id="61ac3-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="61ac3-205">La principal diferencia aquí es que el punto de conexión de servicio configurado hace referencia a un enlace [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding).</span><span class="sxs-lookup"><span data-stu-id="61ac3-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="61ac3-206">El elemento XML `<system.serviceModel>` es un elemento de WCF que define uno o varios servicios.</span><span class="sxs-lookup"><span data-stu-id="61ac3-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="61ac3-207">En este caso, se utiliza para definir el nombre del servicio y el extremo.</span><span class="sxs-lookup"><span data-stu-id="61ac3-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="61ac3-208">En la parte inferior del elemento `<system.serviceModel>` (pero aún dentro de `<system.serviceModel>`), agregue un elemento `<bindings>` con el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="61ac3-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="61ac3-209">Esto define los enlaces utilizados en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61ac3-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="61ac3-210">Puede definir varios enlaces, pero para este tutorial está definiendo solo uno.</span><span class="sxs-lookup"><span data-stu-id="61ac3-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="61ac3-211">Este código anterior define un enlace [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) de WCF Relay con **relayClientAuthenticationType** establecido en **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="61ac3-212">Este valor indica que un extremo que usa este enlace no requiere una credencial de cliente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="61ac3-213">Después del elemento `<bindings>`, agregue un elemento `<services>`.</span><span class="sxs-lookup"><span data-stu-id="61ac3-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="61ac3-214">Al igual que los enlaces, puede definir varios servicios en un solo archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="61ac3-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="61ac3-215">Sin embargo, para este tutorial, solo se define uno.</span><span class="sxs-lookup"><span data-stu-id="61ac3-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="61ac3-216">Este paso configura un servicio que utiliza el valor predeterminado definido anteriormente **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="61ac3-217">También usa el valor predeterminado **sbTokenProvider**, que se define en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="61ac3-218">Después del elemento `<services>`, cree un elemento `<behaviors>` con el contenido siguiente, pero reemplace "SAS_KEY" por la clave de *firma de acceso compartido* (SAS) que obtuvo antes en [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="61ac3-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="61ac3-219">Aún en App.config, en el elemento `<appSettings>`, reemplace todo el valor de la cadena de conexión por la cadena de conexión que obtuvo antes en el portal.</span><span class="sxs-lookup"><span data-stu-id="61ac3-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="61ac3-220">Desde el menú **Compilar**, haga clic en **Compilar solución** para compilar la solución completa.</span><span class="sxs-lookup"><span data-stu-id="61ac3-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="61ac3-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="61ac3-221">Example</span></span>
<span data-ttu-id="61ac3-222">El código siguiente muestra la implementación de contrato y servicio para un servicio basado en REST que se ejecuta en Service Bus con el enlace **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="61ac3-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="61ac3-223">En el ejemplo siguiente se muestra el archivo App.config asociado con el servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="61ac3-224">Paso 4: Hospedar el servicio de WCF basado en REST para usar Azure Relay</span><span class="sxs-lookup"><span data-stu-id="61ac3-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="61ac3-225">Este paso describe cómo ejecutar un servicio web mediante una aplicación de consola con WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="61ac3-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="61ac3-226">En el ejemplo que sigue al procedimiento se proporciona una lista completa del código escrito en este paso.</span><span class="sxs-lookup"><span data-stu-id="61ac3-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="61ac3-227">Para crear una dirección base para el servicio</span><span class="sxs-lookup"><span data-stu-id="61ac3-227">To create a base address for the service</span></span>
1. <span data-ttu-id="61ac3-228">En la declaración de la función `Main()`, cree una variable para almacenar el espacio de nombres de su proyecto.</span><span class="sxs-lookup"><span data-stu-id="61ac3-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="61ac3-229">Asegúrese de reemplazar `yourNamespace` por el nombre del espacio de nombres de Relay que creó antes.</span><span class="sxs-lookup"><span data-stu-id="61ac3-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="61ac3-230">El Bus de servicio utiliza el nombre del espacio de nombres para crear un URI único.</span><span class="sxs-lookup"><span data-stu-id="61ac3-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="61ac3-231">Cree una instancia `Uri` para la dirección base del servicio que se basa en el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="61ac3-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="61ac3-232">Para crear y configurar el host del servicio web</span><span class="sxs-lookup"><span data-stu-id="61ac3-232">To create and configure the web service host</span></span>
* <span data-ttu-id="61ac3-233">Cree el host del servicio web, utilizando la dirección URI creada anteriormente en esta sección.</span><span class="sxs-lookup"><span data-stu-id="61ac3-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="61ac3-234">El host de servicio es el objeto de WCF que crea una instancia de la aplicación host.</span><span class="sxs-lookup"><span data-stu-id="61ac3-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="61ac3-235">En este ejemplo se pasa el tipo de host que desea crear (un **ImageService**) y también la dirección en la que desea exponer la aplicación host.</span><span class="sxs-lookup"><span data-stu-id="61ac3-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="61ac3-236">Para ejecutar el host del servicio web</span><span class="sxs-lookup"><span data-stu-id="61ac3-236">To run the web service host</span></span>
1. <span data-ttu-id="61ac3-237">Abra el servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="61ac3-238">El servicio está ahora en ejecución.</span><span class="sxs-lookup"><span data-stu-id="61ac3-238">The service is now running.</span></span>
2. <span data-ttu-id="61ac3-239">Muestre un mensaje que indica que el servicio se está ejecutando y cómo detenerlo.</span><span class="sxs-lookup"><span data-stu-id="61ac3-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="61ac3-240">Cuando termine, cierre el host del servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="61ac3-241">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="61ac3-241">Example</span></span>
<span data-ttu-id="61ac3-242">En el ejemplo siguiente se incluye el contrato de servicio y la implementación de los pasos anteriores en el tutorial y se hospeda el servicio en una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="61ac3-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="61ac3-243">Compile el código siguiente en un archivo ejecutable denominado ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="61ac3-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="61ac3-244">Compilación del código</span><span class="sxs-lookup"><span data-stu-id="61ac3-244">Compiling the code</span></span>
<span data-ttu-id="61ac3-245">Después de compilar la solución, haga lo siguiente para ejecutar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="61ac3-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="61ac3-246">Presione **F5** o busque la ubicación del archivo ejecutable (ImageListener\bin\Debug\ImageListener.exe) para ejecutar el servicio.</span><span class="sxs-lookup"><span data-stu-id="61ac3-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="61ac3-247">Mantenga la aplicación en ejecución, ya que se necesita para realizar el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="61ac3-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="61ac3-248">Copie y pegue la dirección desde el símbolo del sistema en un explorador para ver la imagen.</span><span class="sxs-lookup"><span data-stu-id="61ac3-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="61ac3-249">Cuando haya terminado, presione **ENTRAR** en la ventana del símbolo del sistema para cerrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61ac3-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61ac3-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61ac3-250">Next steps</span></span>
<span data-ttu-id="61ac3-251">Ahora que ha creado una aplicación que utiliza el servicio Service Bus Relay, consulte los artículos siguientes para obtener más información sobre Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="61ac3-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="61ac3-252">Información general sobre la arquitectura de Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="61ac3-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="61ac3-253">Introducción a Azure Relay</span><span class="sxs-lookup"><span data-stu-id="61ac3-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="61ac3-254">Uso de WCF Relay de Service Bus con .NET</span><span class="sxs-lookup"><span data-stu-id="61ac3-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
