---
title: "Realización de una llamada telefónica desde Twilio (.NET) | Microsoft Docs"
description: "Aprenda a realizar llamadas telefónicas y a enviar mensajes SMS con el servicio de la API de Twilio en Azure. Los ejemplos de código están escritos en .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="d5cce-104">Realización de una llamada telefónica con Twilio en un rol web en Azure</span><span class="sxs-lookup"><span data-stu-id="d5cce-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="d5cce-105">En esta guía se describe cómo usar Twilio para realizar una llamada desde una página web hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="d5cce-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="d5cce-106">La aplicación resultante pide al usuario que llame a un determinado número y deje un mensaje, como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="d5cce-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Formulario de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="d5cce-108"><a name="twilio-prereqs"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d5cce-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="d5cce-109">Tendrá que hacer lo siguiente para usar el código de este tema:</span><span class="sxs-lookup"><span data-stu-id="d5cce-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="d5cce-110">Adquiera una cuenta de Twilio y un token de autenticación desde la [Consola de Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="d5cce-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="d5cce-111">Para empezar con Twilio, regístrese en [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d5cce-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="d5cce-112">Puede estudiar los precios en [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d5cce-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="d5cce-113">Para más información sobre la API proporcionada por Twilio, vea [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d5cce-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="d5cce-114">Agregue la *biblioteca .NET de Twilio*  al rol web.</span><span class="sxs-lookup"><span data-stu-id="d5cce-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="d5cce-115">Vea **Para agregar las bibliotecas de Twilio al proyecto de rol web**, más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="d5cce-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="d5cce-116">Debe saber cómo crear un [rol web básico en Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="d5cce-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="d5cce-117"><a name="howtocreateform"></a>Creación de un formulario web para hacer una llamada</span><span class="sxs-lookup"><span data-stu-id="d5cce-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="d5cce-118"><a id="use_nuget"></a>Para agregar las bibliotecas de Twilio al proyecto de rol web:</span><span class="sxs-lookup"><span data-stu-id="d5cce-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="d5cce-119">Abra su solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5cce-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="d5cce-120">Haga clic con el botón secundario en **Referencias**.</span><span class="sxs-lookup"><span data-stu-id="d5cce-120">Right-click **References**.</span></span>
3. <span data-ttu-id="d5cce-121">Haga clic en **Administración de paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d5cce-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="d5cce-122">Haga clic en **En línea**.</span><span class="sxs-lookup"><span data-stu-id="d5cce-122">Click **Online**.</span></span>
5. <span data-ttu-id="d5cce-123">En el cuadro de búsqueda en línea, escriba *twilio*.</span><span class="sxs-lookup"><span data-stu-id="d5cce-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="d5cce-124">Haga clic en **Instalar** en el paquete de Twilio.</span><span class="sxs-lookup"><span data-stu-id="d5cce-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="d5cce-125">El siguiente código muestra cómo crear un formulario web para recuperar datos de usuario para hacer una llamada.</span><span class="sxs-lookup"><span data-stu-id="d5cce-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="d5cce-126">En este ejemplo, se crea un rol web de ASP.NET denominado **TwilioCloud**.</span><span class="sxs-lookup"><span data-stu-id="d5cce-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="d5cce-127"><a id="howtocreatecode"></a>Creación del código para realizar la llamada</span><span class="sxs-lookup"><span data-stu-id="d5cce-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="d5cce-128">El siguiente código, al que se llama cuando el usuario completa el formulario, crea el mensaje de llamada y genera la llamada.</span><span class="sxs-lookup"><span data-stu-id="d5cce-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="d5cce-129">En este ejemplo, el código se ejecuta en el controlador de eventos onclick del botón en el formulario.</span><span class="sxs-lookup"><span data-stu-id="d5cce-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="d5cce-130">(Use su cuenta Twilio y su token de autenticación en lugar de los valores de marcador de posición asignados a `accountSID` y `authToken` en el siguiente código).</span><span class="sxs-lookup"><span data-stu-id="d5cce-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="d5cce-131">Se realiza la llamada y se muestran el extremo de Twilio, la versión de la API y el estado de la llamada.</span><span class="sxs-lookup"><span data-stu-id="d5cce-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="d5cce-132">En la captura de pantalla siguiente se muestra el resultado de una ejecución de muestra.</span><span class="sxs-lookup"><span data-stu-id="d5cce-132">The following screenshot shows output from a sample run.</span></span>

![Respuesta de llamada de Azure con Twilio y ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="d5cce-134">Encontrará más información sobre TwiML en [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="d5cce-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="d5cce-135">Encontrará más información sobre &lt;Say&gt; y otros verbos de Twilio en [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="d5cce-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="d5cce-136"><a id="nextsteps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5cce-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="d5cce-137">Este código se proporciona para mostrar la funcionalidad básica del uso de Twilio en un rol web de ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="d5cce-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="d5cce-138">Antes de implementarlo en Azure en producción, es posible que desee agregar más controles de errores u otras características.</span><span class="sxs-lookup"><span data-stu-id="d5cce-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="d5cce-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d5cce-139">For example:</span></span>

* <span data-ttu-id="d5cce-140">En lugar de usar un formulario web, puede usar el almacenamiento de blobs de Azure o una instancia de Base de datos SQL de Azure para almacenar los números de teléfono y el texto de llamada.</span><span class="sxs-lookup"><span data-stu-id="d5cce-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="d5cce-141">Para más información sobre cómo usar blobs en Azure, vea [Introducción al servicio Azure Blob Storage en .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="d5cce-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="d5cce-142">Para más información sobre cómo usar SQL Database, vea [Azure SQL Database: uso de .NET (C#) para conectar y consultar datos][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="d5cce-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="d5cce-143">Puede usar `RoleEnvironment.getConfigurationSettings` para recuperar el identificador de la cuenta de Twilio y el token de autenticación desde los ajustes de configuración de su implementación, en vez de codificar de forma rígida los valores en el formulario.</span><span class="sxs-lookup"><span data-stu-id="d5cce-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="d5cce-144">Para más información sobre la clase `RoleEnvironment`, vea el tema sobre el [espacio de nombres Microsoft.WindowsAzure.ServiceRuntime][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="d5cce-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="d5cce-145">Lea las directrices de seguridad de Twilio en [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="d5cce-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="d5cce-146">Obtenga más información sobre Twilio en [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="d5cce-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="d5cce-147"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="d5cce-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d5cce-148">Uso de Twilio para funciones de voz y SMS desde Azure</span><span class="sxs-lookup"><span data-stu-id="d5cce-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
