emulador de almacenamiento de Hello es compatible con una cuenta única fija y una clave de autenticación conocido para la autenticación de clave compartida. Esta cuenta y clave son Hola solo Shared Key las credenciales de admiten para su uso con el emulador de almacenamiento de Hola. Son las siguientes:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> clave de autenticación de Hello compatible con el emulador de almacenamiento de hello está pensado únicamente para la funcionalidad de Hola la prueba de su código de autenticación de cliente. No responde a ningún propósito de seguridad. No puede usar su cuenta de almacenamiento de producción y la clave con el emulador de almacenamiento de Hola. No se debe usar cuenta de hello de desarrollo con datos de producción.
> 
> emulador de almacenamiento de Hello admite solo la conexión a través de HTTP. Sin embargo, HTTPS es hello recomendada protocolo para tener acceso a recursos en una cuenta de almacenamiento de Azure de producción.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Conectar toohello cuenta del emulador mediante un acceso directo
Hola más fácil manera tooconnect toohello emulador de almacenamiento de la aplicación es tooconfigure una cadena de conexión en el archivo de configuración de la aplicación que hace referencia el acceso directo de hello `UseDevelopmentStorage=true`. Este es un ejemplo de un emulador de almacenamiento de toohello de cadena de conexión en un *app.config* archivo: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Conectar toohello cuenta del emulador mediante la clave y el nombre de cuenta conocida de Hola
toocreate una cadena de conexión que referencias Hola nombre de la cuenta de emulador y clave, debe especificar los puntos de conexión de Hola para cada uno de hello de servicios le interese toouse desde el emulador de hello en la cadena de conexión de Hola. Esto es necesario para que la cadena de conexión de hello hará referencia a los extremos de emulador de hello, que son diferentes de las de una cuenta de almacenamiento de producción. Por ejemplo, valor de saludo de la cadena de conexión tendrá un aspecto similar al siguiente:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Este valor es contextual toohello idénticos mostrado anteriormente, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Especificación de un servidor proxy HTTP
También puede especificar un toouse de proxy HTTP cuando se está probando su servicio con el emulador de almacenamiento de Hola. Esto puede ser útil para observar solicitudes y respuestas HTTP mientras está depurando operaciones con los servicios de almacenamiento de Hola. toospecify un proxy, agregar hello `DevelopmentStorageProxyUri` opción toohello cadena de conexión y establecer su URI del servidor de proxy toohello del valor. Por ejemplo, aquí es una cadena de conexión que señala el emulador de almacenamiento de toohello y configura a un servidor proxy HTTP:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

