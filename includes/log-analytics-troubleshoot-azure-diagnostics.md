### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="ada67-101">Solución de problemas de Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="ada67-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="ada67-102">Si recibe Hola siguiente mensaje de error, no está registrado el proveedor de recursos de Hola Microsoft.insights:</span><span class="sxs-lookup"><span data-stu-id="ada67-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="ada67-103">proveedor de recursos de tooregister hello, realizar Hola pasos de hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="ada67-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="ada67-104">En el panel de navegación de Hola Hola izquierda, haga clic en *suscripciones*</span><span class="sxs-lookup"><span data-stu-id="ada67-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="ada67-105">Seleccionar suscripción Hola identificado en el mensaje de error de Hola</span><span class="sxs-lookup"><span data-stu-id="ada67-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="ada67-106">Haga clic en *Proveedores de recursos*</span><span class="sxs-lookup"><span data-stu-id="ada67-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="ada67-107">Buscar hello *Microsoft.insights* proveedor</span><span class="sxs-lookup"><span data-stu-id="ada67-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="ada67-108">Haga clic en hello *registrar* vínculo</span><span class="sxs-lookup"><span data-stu-id="ada67-108">Click hello *Register* link</span></span>

![Registro del proveedor de recursos de microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="ada67-110">Una vez Hola *Microsoft.insights* está registrado el proveedor de recursos, vuelva a intentar la configuración de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ada67-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="ada67-111">En PowerShell, si recibe Hola siguiente mensaje de error, debe tooupdate su versión de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ada67-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="ada67-112">Actualice su versión de PowerShell toohello noviembre de 2016 (v2.3.0) o una versión posterior, la versión siguiendo las instrucciones de hello en hello [empezar a trabajar con cmdlets de PowerShell de Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artículo.</span><span class="sxs-lookup"><span data-stu-id="ada67-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
