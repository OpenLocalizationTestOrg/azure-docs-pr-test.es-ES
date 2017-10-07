---
title: "las aplicaciones de .NET SDK toodevelop Hola de aaaUse en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Usar una cuenta de almacén de Data Lake del almacén .NET SDK de Azure Data Lake toocreate y realizar operaciones básicas en hello almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Introducción al Almacén de Azure Data Lake mediante SDK de .NET
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Obtenga información acerca de cómo hello toouse [almacén .NET SDK de Azure Data Lake](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform operaciones básicas, como crear carpetas, cargar y descargar archivos de datos, etcetera. Para más información sobre Data Lake, consulte [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Requisitos previos
* **Visual Studio 2013, 2015 o 2017**. Estas instrucciones Hola usan Visual Studio 2015 Update 2.

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Cuenta del Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate una cuenta, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)

* **Cree una aplicación de Azure Active Directory**. Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD. Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Creación de una aplicación .NET
1. Abra Visual Studio y cree una aplicación de consola.
2. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
3. De **nuevo proyecto**, escriba o seleccione Hola siguientes valores:

   | Propiedad | Valor |
   | --- | --- |
   | Categoría |Plantillas/Visual C#/Windows |
   | Plantilla |Aplicación de consola |
   | Nombre |CreateADLApplication |
4. Haga clic en **Aceptar** proyecto de hello toocreate.
5. Agregar proyecto de tooyour de paquetes de Nuget Hola.

   1. Haga clic en el nombre del proyecto Hola Hola el Explorador de soluciones y haga clic en **administrar paquetes de NuGet**.
   2. Hola **Administrador de paquetes de Nuget** ficha, asegúrese de que **origen del paquete** se establece demasiado**nuget.org** y que **incluir versión preliminar** casilla de verificación está activada.
   3. Buscar e instalar los siguientes paquetes de NuGet de Hola:

      * `Microsoft.Azure.Management.DataLake.Store` - En este tutorial se usa v2.1.3 (versión preliminar).
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - En este tutorial se usa v2.2.12.

        ![Incorporación de un origen de Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creación de una cuenta de Azure Data Lake")
   4. Hola cerrar **Administrador de paquetes de Nuget**.
6. Abra **Program.cs**, eliminar código existente de hello y, a continuación, incluir Hola siguiendo las instrucciones tooadd referencias toonamespaces.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Declarar variables de hello tal y como se muestra a continuación y proporcione valores de hello para el nombre de almacén de Data Lake y nombre de grupo de recursos de Hola que ya existen. Además, asegúrese de hello ruta de acceso y nombre local que proporciona aquí debe existir en el equipo de Hola. Agregar Hola siguiente fragmento de código después de las declaraciones de espacio de nombres de Hola.

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

Hola restantes secciones de artículo de hello, puede ver cómo toouse Hola operaciones de tooperform de métodos de .NET disponibles, como la autenticación, la carga de archivos etcetera.

## <a name="authentication"></a>Autenticación

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Si utiliza la autenticación de usuario final (recomendada para este tutorial)

Usar esta opción con un tooauthenticate de aplicación nativa de Azure AD existente de la aplicación **interactivamente**, que significa que podrá solicita tooenter sus credenciales de Azure.

Para facilitar su uso, el siguiente fragmento de Hola usa valores predeterminados para URI que funcionará con cualquier suscripción de Azure de redirección e identificador de cliente. toohelp completar este tutorial con mayor rapidez, se recomienda que usar este enfoque. En el siguiente fragmento de hello, basta con que proporcione el valor de hello para el identificador del inquilino. Puede recuperarlo mediante instrucciones de hello proporcionadas en [crear un Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Un par de cosas tooknow acerca de este fragmento de código anterior:

* toohelp completar el tutorial de hello con mayor rapidez, este fragmento de código utiliza un Azure AD Id. de dominio y el cliente que está disponible de forma predeterminada para todas las suscripciones de Azure. Por lo tanto, puede **usar este fragmento de código tal cual en la aplicación**.
* Sin embargo, si desea toouse su propio dominio de Azure AD e Id. de aplicación cliente, debe crear una aplicación nativa de Azure AD y, a continuación, use hello Azure AD ID, Id. de cliente, de inquilinos y URI de redirección de la aplicación hello creado. Consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) para obtener instrucciones.

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Si utiliza la autenticación de servicio a servicio con el secreto de cliente
Hola siguiente fragmento de código puede ser tooauthenticate usa la aplicación **una manera no interactiva**, utilizando la clave secreta de cliente de Hola / clave para una identidad de aplicación / servicio. Utilícelo con una aplicación web de Azure AD ya existente. Para obtener instrucciones sobre cómo ver la aplicación web de toocreate hello Azure AD y cómo tooretrieve Hola Id. de cliente y el secreto de cliente necesario en la siguiente, el fragmento de hello [crear una aplicación de directorio activo para la autenticación de servicio al servicio con datos Almacén Lake](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Si utilice autenticación de servicio a servicio con certificado

Como una tercera opción, hello siguiente fragmento de código puede ser tooauthenticate usa la aplicación **una manera no interactiva**, utilizando el certificado de Hola para una aplicación de Azure Active Directory / entidad de seguridad de servicio. Utilícelo con una [aplicación de Azure AD con certificados](../azure-resource-manager/resource-group-authenticate-service-principal.md) ya existente.

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Creación de objetos de cliente
Hello fragmento de código siguiente crea cuenta de almacén de Data Lake hello y filesystem objetos de cliente, que se usan tooissue solicitudes de servicio de toohello.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Enumeración de todas las cuentas de Data Lake Store de una suscripción
Hello fragmento de código siguiente enumera todas las cuentas de almacén de Data Lake dentro de una determinada suscripción de Azure.

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a>Creación de directorios
Hola fragmento siguiente muestra un `CreateDirectory` método que puede utilizar un directorio en una cuenta de almacén de Data Lake toocreate.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Cargar un archivo
Hola fragmento siguiente muestra un `UploadFile` método que puede utilizar tooupload archivos tooa cuenta de almacén de Data Lake.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Hola SDK admite recursiva carga y descarga entre una ruta de acceso de archivo local y una ruta de acceso del archivo de almacén de Data Lake.    

## <a name="get-file-or-directory-info"></a>Obtención de información de un archivo o directorio
Hola fragmento siguiente muestra un `GetItemInfo` método que puede utilizar tooretrieve información acerca de un archivo o directorio disponible en el almacén de Data Lake.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Enumeración de archivos o directorios
Hola fragmento siguiente muestra un `ListItem` método que puede usar toolist Hola archivos y directorios en una cuenta de almacén de Data Lake.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Concatenación de archivos
Hola fragmento siguiente muestra un `ConcatenateFiles` método que se usan archivos de tooconcatenate.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Anexar el archivo de tooa
Hola fragmento siguiente muestra un `AppendToFile` método que use anexar el archivo de tooa de datos ya estén almacenado en una cuenta de almacén de Data Lake.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Descarga de un archivo
Hola fragmento siguiente muestra un `DownloadFile` método que se utiliza un archivo de una cuenta de almacén de Data Lake toodownload.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Pasos siguientes
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Referencia de SDK de .NET de Data Lake Store](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Referencia de REST de Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
