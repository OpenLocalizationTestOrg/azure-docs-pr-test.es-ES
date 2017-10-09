<span data-ttu-id="fbf94-101">Si posee una dirección URL de firma (SAS) de acceso compartido que concede que acceso tooresources en una cuenta de almacenamiento, puede usar Hola SAS en una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="fbf94-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="fbf94-102">Dado que Hola SAS contiene solicitud de hello información tooauthenticate necesario hello, una cadena de conexión con una SAS proporciona protocolo hello, extremo de servicio de Hola y recursos de hello tooaccess de hello credenciales necesarias.</span><span class="sxs-lookup"><span data-stu-id="fbf94-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="fbf94-103">toocreate una cadena de conexión que incluya una firma de acceso compartido, especificar la cadena de Hola Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="fbf94-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="fbf94-104">Cada extremo de servicio es opcional, aunque la cadena de conexión de hello debe contener al menos uno.</span><span class="sxs-lookup"><span data-stu-id="fbf94-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="fbf94-105">Se recomienda usar HTTPS con SAS.</span><span class="sxs-lookup"><span data-stu-id="fbf94-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="fbf94-106">Si está especificando una SAS en una cadena de conexión en un archivo de configuración, debe tooencode caracteres especiales en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbf94-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="fbf94-107">Ejemplo de SAS de servicio</span><span class="sxs-lookup"><span data-stu-id="fbf94-107">Service SAS example</span></span>
<span data-ttu-id="fbf94-108">Este es un ejemplo de una cadena de conexión que incluye un SAS de servicio para el almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="fbf94-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="fbf94-109">A continuación se muestra un ejemplo de Hola misma cadena de conexión con la codificación de caracteres especiales:</span><span class="sxs-lookup"><span data-stu-id="fbf94-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="fbf94-110">Ejemplo de SAS de cuenta</span><span class="sxs-lookup"><span data-stu-id="fbf94-110">Account SAS example</span></span>
<span data-ttu-id="fbf94-111">Este es un ejemplo de una cadena de conexión que incluye un SAS de cuenta para el almacenamiento de blobs y archivos:</span><span class="sxs-lookup"><span data-stu-id="fbf94-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="fbf94-112">Tenga en cuenta que se especifican los puntos de conexión para ambos servicios:</span><span class="sxs-lookup"><span data-stu-id="fbf94-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="fbf94-113">A continuación se muestra un ejemplo de Hola misma cadena de conexión con la codificación de direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="fbf94-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

