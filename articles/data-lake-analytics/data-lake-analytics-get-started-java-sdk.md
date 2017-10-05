---
title: Uso del SDK de Data Lake Analytics para desarrollar aplicaciones | Microsoft Docs
description: "Uso del SDK de Java de Análisis de Azure Data Lake para desarrollar aplicaciones"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 795d9ec0b0cac5d74673404f1d0d851393336df0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="75579-103">Introducción al uso de SDK de Java por parte de Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="75579-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="75579-104">Aprenda a utilizar el SDK de Java de Análisis de Azure Data Lake para crear una cuenta de Azure Data Lake y realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, eliminar la cuenta y actuar con trabajos.</span><span class="sxs-lookup"><span data-stu-id="75579-104">Learn how to use the Azure Data Lake Analytics Java SDK to create an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="75579-105">Para más información sobre Data Lake, consulte [Análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75579-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="75579-106">En este tutorial, aprenderá a desarrollar una aplicación de consola Java que contiene ejemplos de tareas administrativas comunes, así como a crear datos de prueba y enviar un trabajo.</span><span class="sxs-lookup"><span data-stu-id="75579-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="75579-107">Para recorrer el mismo tutorial con otras herramientas compatibles, haga clic en las pestañas situadas en la parte superior de esta sección.</span><span class="sxs-lookup"><span data-stu-id="75579-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75579-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="75579-108">Prerequisites</span></span>
* <span data-ttu-id="75579-109">Kit de desarrollo de Java (JDK) 8 (con Java versión 1.8).</span><span class="sxs-lookup"><span data-stu-id="75579-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="75579-110">IntelliJ u otro entorno de desarrollo de Java adecuado.</span><span class="sxs-lookup"><span data-stu-id="75579-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="75579-111">Este requisito es opcional pero recomendable.</span><span class="sxs-lookup"><span data-stu-id="75579-111">This is optional but recommended.</span></span> <span data-ttu-id="75579-112">En las instrucciones siguientes se utiliza IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="75579-112">The instructions below use IntelliJ.</span></span>
* <span data-ttu-id="75579-113">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="75579-113">**An Azure subscription**.</span></span> <span data-ttu-id="75579-114">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75579-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="75579-115">Cree una aplicación de Azure Active Directory (AAD) y recupere su **identificador de cliente**, **identificador de inquilino** y **clave**.</span><span class="sxs-lookup"><span data-stu-id="75579-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="75579-116">Para más información sobre las aplicaciones de AAD y ver instrucciones sobre cómo obtener un id. de cliente, consulte [Creación de una aplicación de Active Directory y una entidad de servicio mediante el portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75579-116">For more information about AAD applications and instructions on how to get a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="75579-117">El URI de respuesta y la clave también estarán disponibles desde el portal cuando haya creado la aplicación y generado la clave.</span><span class="sxs-lookup"><span data-stu-id="75579-117">The Reply URI and Key will also be available from the portal once you have the application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="75579-118">¿Cómo se puede autenticar mediante Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75579-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="75579-119">El siguiente fragmento de código proporciona código para la autenticación **no interactiva** , donde la aplicación proporciona sus propias credenciales.</span><span class="sxs-lookup"><span data-stu-id="75579-119">The code snippet below provides code for **non-interactive** authentication, where the application provides its own credentials.</span></span>

<span data-ttu-id="75579-120">Para que este tutorial funcione, deberá conceder permiso a su aplicación para crear recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="75579-120">You will need to give your application permission to create resources in Azure for this tutorial to work.</span></span> <span data-ttu-id="75579-121">Para este tutorial, se **recomienda encarecidamente** conceder a esta aplicación solo permisos de colaborador para un grupo de recursos nuevo, sin usar y vacío en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="75579-121">It is **highly recommended** that you only give this application Contributor permissions to a new, unused, and empty resource group in your Azure subscription for the purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="75579-122">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="75579-122">Create a Java application</span></span>
1. <span data-ttu-id="75579-123">Abra IntelliJ y cree un proyecto de Java mediante la plantilla de **aplicación de línea de comandos** .</span><span class="sxs-lookup"><span data-stu-id="75579-123">Open IntelliJ and create a new Java project using the **Command Line App** template.</span></span>
2. <span data-ttu-id="75579-124">Haga clic con el botón derecho en el proyecto de la izquierda de la pantalla y haga clic en **Add Framework Support**(Agregar compatibilidad con el marco).</span><span class="sxs-lookup"><span data-stu-id="75579-124">Right-click on the project on the left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="75579-125">Elija **Maven** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="75579-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="75579-126">Abra el archivo **"pom.xml"** recién creado y agregue el siguiente fragmento de código de texto entre las etiquetas **\<</version>** y **\</project>**:</span><span class="sxs-lookup"><span data-stu-id="75579-126">Open the newly created **"pom.xml"** file and add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="75579-127">Este paso es temporal hasta que el SDK de Azure Data Lake Analytics esté disponible en Maven.</span><span class="sxs-lookup"><span data-stu-id="75579-127">This step is temporary until the Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="75579-128">Este artículo se actualizará cuando el SDK esté disponible en Maven.</span><span class="sxs-lookup"><span data-stu-id="75579-128">This article will be updated once the SDK is available in Maven.</span></span> <span data-ttu-id="75579-129">Todas las futuras actualizaciones de este SDK estarán disponible mediante Maven.</span><span class="sxs-lookup"><span data-stu-id="75579-129">All future updates to this SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="75579-130">Vaya a **Archivo**, **Configuración**, **Compilación**, **Ejecución** e **Implementación**.</span><span class="sxs-lookup"><span data-stu-id="75579-130">Go to **File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="75579-131">Seleccione **Herramientas de compilación**, **Maven**, **Importando**.</span><span class="sxs-lookup"><span data-stu-id="75579-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="75579-132">A continuación, marque **Importar proyectos de Maven automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="75579-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="75579-133">Abra el archivo **Main.cs** y sustituya el bloque de código existente por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="75579-133">Open **Main.java** and replace the existing code block with the following code.</span></span> <span data-ttu-id="75579-134">Especifique también los valores de los parámetros que se mencionan en el fragmento de código, por ejemplo, **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName**, y reemplace los marcadores de posición de **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID** y **SUBSCRIPTION-ID**.</span><span class="sxs-lookup"><span data-stu-id="75579-134">Also, provide the values for parameters called out in the code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="75579-135">Este código recorre el proceso de creación de cuentas de Almacén de Data Lake y de Análisis de Data Lake, de creación de archivos en el almacén, de ejecución de un trabajo, de obtención del estado del trabajo, de descarga de la salida del trabajo y finalmente de eliminación de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="75579-135">This code goes through the process of creating Data Lake Store and Data Lake Analytics accounts, creating files in the store, running a job, getting job status, downloading job output, and finally deleting the account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="75579-136">Actualmente no hay ningún problema conocido con el servicio de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="75579-136">There is currently a known issue with the Azure Data Lake Service.</span></span>  <span data-ttu-id="75579-137">Si la aplicación de ejemplo se interrumpe o encuentra un error, es posible que deba eliminar manualmente las cuentas de Almacén de Data Lake y Análisis de Data Lake que crea el script.</span><span class="sxs-lookup"><span data-stu-id="75579-137">If the sample app is interrupted or encounters an error, you may need to manually delete the Data Lake Store & Data Lake Analytics accounts that the script creates.</span></span>  <span data-ttu-id="75579-138">Si no conoce el Portal, la guía [Administración de Análisis de Azure Data Lake mediante el Portal de Azure](data-lake-analytics-manage-use-portal.md) lo ayudará a empezar.</span><span class="sxs-lookup"><span data-stu-id="75579-138">If you're not familiar with the Portal, the [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring the application client secret, rather than hard-coding it in the source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this to any unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in the next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job to Data Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function to show status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER to continue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "The deep update for property 'DataLakeStoreAccounts' is not supported", please delete the ADLS and ADLA accounts via the portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in the next version of the API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns the job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="75579-139">Siga las indicaciones para ejecutar y completar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="75579-139">Follow the prompts to run and complete the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="75579-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="75579-140">See also</span></span>
* <span data-ttu-id="75579-141">Para ver el mismo tutorial con otras herramientas, haga clic en los selectores de pestañas en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="75579-141">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="75579-142">Para ver una consulta más compleja, consulte la página sobre el [análisis de registros de sitio web mediante Análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="75579-142">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="75579-143">Para empezar a desarrollar aplicaciones con U-SQL, consulte [Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="75579-143">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="75579-144">Para aprender U-SQL, consulte el [Tutorial: Introducción al lenguaje U-SQL de Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md) y la página de [referencia del lenguaje U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="75579-144">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="75579-145">Para las tareas de administración, consulte [Administración de Análisis de Azure Data Lake mediante el Portal de Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75579-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="75579-146">Para obtener información general sobre Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75579-146">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
