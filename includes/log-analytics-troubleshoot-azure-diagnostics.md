### <a name="troubleshoot-azure-diagnostics"></a>Solución de problemas de Diagnósticos de Azure

Si recibe Hola siguiente mensaje de error, no está registrado el proveedor de recursos de Hola Microsoft.insights:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

proveedor de recursos de tooregister hello, realizar Hola pasos de hello portal de Azure:

1.  En el panel de navegación de Hola Hola izquierda, haga clic en *suscripciones*
2.  Seleccionar suscripción Hola identificado en el mensaje de error de Hola
3.  Haga clic en *Proveedores de recursos*
4.  Buscar hello *Microsoft.insights* proveedor
5.  Haga clic en hello *registrar* vínculo

![Registro del proveedor de recursos de microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Una vez Hola *Microsoft.insights* está registrado el proveedor de recursos, vuelva a intentar la configuración de diagnóstico.


En PowerShell, si recibe Hola siguiente mensaje de error, debe tooupdate su versión de PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Actualice su versión de PowerShell toohello noviembre de 2016 (v2.3.0) o una versión posterior, la versión siguiendo las instrucciones de hello en hello [empezar a trabajar con cmdlets de PowerShell de Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) artículo.
