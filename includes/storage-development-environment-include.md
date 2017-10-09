## <a name="set-up-your-development-environment"></a>Configuración de su entorno de desarrollo
A continuación, configurar el entorno de desarrollo en Visual Studio para que sean más ejemplos de código de hello tootry listo en esta guía.

### <a name="create-a-windows-console-application-project"></a>Creación de un proyecto de aplicación de consola de Windows
En Visual Studio, cree una nueva aplicación de consola de Windows. Hola siguientes pasos muestra cómo toocreate una aplicación de consola en Visual Studio 2017, sin embargo, los pasos de hello son similares en otras versiones de Visual Studio.

1. Seleccione **Archivo** > **Nuevo** > **Proyecto**
2. Seleccione **Instalado** > **Plantillas** > **Visual C#** > **Escritorio clásico de Windows**
3. Seleccione **Aplicación de consola (.NET Framework)**
4. Escriba un nombre para la aplicación Hola **nombre:** campo
5. Seleccione **Aceptar**.

![Cuadro de diálogo de creación de proyecto en Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Todos los ejemplos de código de este tutorial pueden agregarse toohello `Main()` método de la aplicación de consola `Program.cs` archivo.

Puede usar hello biblioteca de cliente de almacenamiento de Azure en cualquier tipo de aplicación. NET, incluida una aplicación web o servicio de nube de Azure y las aplicaciones de escritorio y móviles. En esta guía, usamos una aplicación de consola para hacerlo más sencillo.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Usar paquetes de NuGet tooinstall Hola necesario
Hay dos paquetes necesita tooreference en su proyecto toocomplete este tutorial:

* [Biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): este paquete proporciona acceso mediante programación toodata recursos en su cuenta de almacenamiento.
* [Biblioteca de Administrador de configuración de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): este paquete proporciona una clase para analizar una cadena de conexión en un archivo de configuración, independientemente del lugar en que se ejecute la aplicación.

Puede usar NuGet tooobtain ambos paquetes. Siga estos pasos:

1. Haga clic con el botón derecho en el proyecto, en el **Explorador de soluciones**, y elija **Administrar paquetes NuGet**.
2. Busque en línea "WindowsAzure.Storage" y haga clic en **instalar** tooinstall Hola biblioteca cliente de almacenamiento y sus dependencias.
3. Busque en línea "WindowsAzure.ConfigurationManager" y haga clic en **instalar** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> paquete de la biblioteca cliente de almacenamiento de Hello también se incluye en hello [Azure SDK para .NET](https://azure.microsoft.com/downloads/). Sin embargo, se recomienda que instale también Hola biblioteca cliente de almacenamiento de tooensure de NuGet que siempre tiene la versión más reciente de Hola Hola de biblioteca de cliente.
> 
> dependencias de ODataLib Hola Hola biblioteca de cliente de almacenamiento para .NET se resuelven mediante paquetes de ODataLib de hello disponibles en NuGet, no de WCF Data Services. bibliotecas de ODataLib Hola se pueden descargar directamente o al que hace referencia el proyecto de código con NuGet. los paquetes de ODataLib específicos Hello usa Hola biblioteca cliente de almacenamiento son [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), y [espacial](http://nuget.org/packages/System.Spatial/). Aunque estas bibliotecas se utilizan las clases de almacenamiento de tabla de Azure de hello, son dependencias necesarias para la programación con hello biblioteca cliente de almacenamiento.
> 
> 

### <a name="determine-your-target-environment"></a>Determine su entorno de destino
Tiene dos opciones de entorno para ejecutar los ejemplos de hello en esta guía:

* Puede ejecutar el código en una cuenta de almacenamiento de Azure en la nube de Hola. 
* Puede ejecutar el código en el emulador de almacenamiento de Azure de Hola. emulador de almacenamiento de Hello es un entorno local que emula una cuenta de almacenamiento de Azure en la nube de Hola. el emulador de Hello es una opción disponible para probar y depurar el código mientras la aplicación está en desarrollo. emulador de Hello usa una cuenta conocida y una clave. Para obtener más información, vea [Hola uso emulador de almacenamiento de Azure para desarrollo y pruebas](../articles/storage/common/storage-use-emulator.md)

Si desea usar una cuenta de almacenamiento en nube de hello, copie la clave de acceso principal de hello para la cuenta de almacenamiento de hello portal de Azure. Para obtener más información, consulte [Visualización y copia de las claves de acceso de almacenamiento](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Puede tener como destino tooavoid de emulador de almacenamiento Hola incurrir en los gastos asociados con el almacenamiento de Azure. Sin embargo, si elige tootarget una cuenta de almacenamiento de Azure en la nube de hello, los costos para llevar a cabo este tutorial será insignificantes.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Configuración de la cadena de conexión de almacenamiento.
Hola biblioteca de cliente de almacenamiento de Azure para .NET admite el uso de un extremos de tooconfigure de cadena de conexión de almacenamiento y las credenciales para tener acceso a servicios de almacenamiento. Hola mejor manera toomaintain la cadena de conexión de almacenamiento está en un archivo de configuración. 

Para obtener más información acerca de las cadenas de conexión, vea [configurar una tooAzure de cadena de conexión almacenamiento](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Clave de la cuenta de almacenamiento es la contraseña de root toohello similar para la cuenta de almacenamiento. Siempre puede tooprotect cuidado su clave de cuenta de almacenamiento. Evitar la distribución a los usuarios de tooother, codificar de forma rígida, o guardarlo en un archivo de texto sin formato es accesible tooothers. Volver a generar la clave mediante Hola portal de Azure si cree que se han comprometido.
> 
> 

tooconfigure su cadena de conexión, abra hello `app.config` archivo desde el Explorador de soluciones en Visual Studio. Agregar contenido de Hola de hello `<appSettings>` elemento se muestra a continuación. Reemplace `account-name` con el nombre de saludo de la cuenta de almacenamiento y `account-key` con su clave de acceso de cuenta:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Por ejemplo, el valor de configuración es similar a:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

emulador de almacenamiento de hello tootarget, puede utilizar un acceso directo que se asigna el nombre de cuenta conocida de toohello y la clave. En ese caso, la configuración de la cadena de conexión es:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

