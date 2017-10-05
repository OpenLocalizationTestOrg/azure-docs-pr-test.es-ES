---
title: "Configuración de la conectividad SSL en Azure Database for PostgreSQL | Microsoft Docs"
description: "Instrucciones e información para configurar Azure Database for PostgreSQL y las aplicaciones asociadas, a fin de usar correctamente las conexiones SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="b7788-103">Configuración de la conectividad SSL en Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b7788-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b7788-104">Azure Database for PostgreSQL prefiere conectar las aplicaciones cliente al servicio de PostgreSQL mediante la Capa de sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="b7788-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="b7788-105">El establecimiento de conexiones SSL entre el servidor de bases de datos y las aplicaciones cliente ofrece protección frente a ataques de tipo "Man in the middle" mediante el cifrado del flujo de datos entre el servidor y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7788-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="b7788-106">De forma predeterminada, el servicio de base de datos de PostgreSQL está configurado para requerir la conexión SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="b7788-107">Tiene la opción de deshabilitar el requisito de SSL para conectar el servicio de base de datos en caso de que la aplicación cliente no admita la conectividad SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="b7788-108">Establecimiento de conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="b7788-108">Enforcing SSL connections</span></span>
<span data-ttu-id="b7788-109">Para todos los servidores de Azure Database for PostgreSQL aprovisionados en Azure Portal o con la CLI de Azure, el establecimiento de conexiones SSL está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b7788-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="b7788-110">Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" del servidor en Azure Portal incluyen los parámetros necesarios para que los lenguajes comunes se conecten al servidor de base de datos mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="b7788-111">El parámetro SSL varía según el conector, por ejemplo, "ssl = true" o "sslmode = require" o "sslmode = required" y otras variaciones.</span><span class="sxs-lookup"><span data-stu-id="b7788-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="b7788-112">Configuración del establecimiento de SSL</span><span class="sxs-lookup"><span data-stu-id="b7788-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="b7788-113">Si lo desea, puede deshabilitar el establecimiento de la conectividad SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="b7788-114">Microsoft Azure recomienda habilitar siempre la opción de configuración **Enforce SSL connection** (Establecer conexión SSL) para mayor seguridad.</span><span class="sxs-lookup"><span data-stu-id="b7788-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="b7788-115">Uso del portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b7788-115">Using the Azure portal</span></span>
<span data-ttu-id="b7788-116">Visite el servidor de Azure Database for PostgreSQL y haga clic en **Seguridad de conexión**.</span><span class="sxs-lookup"><span data-stu-id="b7788-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="b7788-117">Use el botón de alternancia para habilitar o deshabilitar la opción de configuración **Enforce SSL connection** (Establecer conexión SSL).</span><span class="sxs-lookup"><span data-stu-id="b7788-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="b7788-118">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b7788-118">Then click **Save**.</span></span> 

![Seguridad de conexión - Deshabilitar el establecimiento de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="b7788-120">Puede confirmar la configuración; para ello, consulte la página de **información general** para ver el indicador de **estado de establecimiento de SSL**.</span><span class="sxs-lookup"><span data-stu-id="b7788-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="b7788-121">Uso de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b7788-121">Using Azure CLI</span></span>
<span data-ttu-id="b7788-122">Puede habilitar o deshabilitar el parámetro **ssl-enforcement** con los valores `Enabled` o `Disabled` respectivamente en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7788-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="b7788-123">Verificación de que la aplicación o el marco admiten conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="b7788-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="b7788-124">Muchos marcos de aplicaciones comunes que usan PostgreSQL para servicios de bases de datos, como Drupal y Django, no habilitan SSL de forma predeterminada durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="b7788-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="b7788-125">La conectividad SSL debe habilitarse después de la instalación o mediante comandos de la CLI específicos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7788-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="b7788-126">Si el servidor PostgreSQL establece conexiones SSL y la aplicación asociada no está configurada correctamente, es posible que esta última no pueda conectarse al servidor de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b7788-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="b7788-127">Consulte la documentación de la aplicación para obtener información sobre cómo habilitar las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="b7788-128">Aplicaciones que requieren la verificación de certificados para la conectividad SSL</span><span class="sxs-lookup"><span data-stu-id="b7788-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="b7788-129">En algunos casos, las aplicaciones requieren un archivo de certificado local generado a partir de un archivo de certificado (.cer) de una entidad de certificación (CA) de confianza para conectarse de forma segura.</span><span class="sxs-lookup"><span data-stu-id="b7788-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="b7788-130">Consulte los pasos siguientes para obtener el archivo .cer, descodificar el certificado y enlazarlo a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b7788-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="b7788-131">Descarga del archivo de certificado de la entidad de certificación (CA)</span><span class="sxs-lookup"><span data-stu-id="b7788-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="b7788-132">El certificado necesario para comunicarse a través de SSL con el servidor de Azure Database for PostgreSQL se encuentra [aquí](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="b7788-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="b7788-133">Descargue el archivo de certificado en una unidad local.</span><span class="sxs-lookup"><span data-stu-id="b7788-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="b7788-134">Descarga e instalación de OpenSSL en el equipo</span><span class="sxs-lookup"><span data-stu-id="b7788-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="b7788-135">Para descodificar el archivo de certificado necesario para que la aplicación se conecte de forma segura al servidor de bases de datos, debe instalar OpenSSL en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b7788-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="b7788-136">Para Linux, OS X o Unix</span><span class="sxs-lookup"><span data-stu-id="b7788-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="b7788-137">Las bibliotecas OpenSSL se proporcionan en el código fuente directamente desde [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="b7788-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="b7788-138">Las instrucciones siguientes lo guían a través de los pasos necesarios para instalar OpenSSL en un equipo Linux.</span><span class="sxs-lookup"><span data-stu-id="b7788-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="b7788-139">En este artículo se usan comandos conocidos para trabajar en Ubuntu 12.04 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b7788-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="b7788-140">Abra una sesión de terminal e instale OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="b7788-141">Extraiga los archivos del paquete descargado.</span><span class="sxs-lookup"><span data-stu-id="b7788-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="b7788-142">Vaya al directorio donde se extrajeron los archivos.</span><span class="sxs-lookup"><span data-stu-id="b7788-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="b7788-143">La opción predeterminada debe ser la siguiente.</span><span class="sxs-lookup"><span data-stu-id="b7788-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="b7788-144">Configure OpenSSL mediante la ejecución del comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="b7788-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="b7788-145">Si desea que los archivos se ubiquen en una carpeta distinta a /usr/local/openssl, asegúrese de cambiar lo siguiente según proceda.</span><span class="sxs-lookup"><span data-stu-id="b7788-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="b7788-146">Ahora que OpenSSL está configurado correctamente, debe compilarlo para convertir el certificado.</span><span class="sxs-lookup"><span data-stu-id="b7788-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="b7788-147">Para ello, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b7788-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="b7788-148">Una vez completada la compilación, está listo para instalar OpenSSL como un ejecutable con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7788-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="b7788-149">Para confirmar que se ha instalado correctamente OpenSSL en el sistema, ejecute el siguiente comando y compruébelo para asegurarse de que obtendrá la misma salida.</span><span class="sxs-lookup"><span data-stu-id="b7788-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="b7788-150">Si la operación se realiza correctamente, debería aparecer el mensaje siguiente.</span><span class="sxs-lookup"><span data-stu-id="b7788-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="b7788-151">Para Windows</span><span class="sxs-lookup"><span data-stu-id="b7788-151">For Windows</span></span>
<span data-ttu-id="b7788-152">La instalación de OpenSSL en un PC Windows puede realizarse de las siguientes formas:</span><span class="sxs-lookup"><span data-stu-id="b7788-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="b7788-153">**(Recomendado)**  OpenSSL se instala de forma predeterminada con la funcionalidad de Bash para Windows integrada en Windows 10 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="b7788-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="b7788-154">Encontrará instrucciones sobre cómo habilitar la funcionalidad de Bash para Windows en Windows 10 [aquí](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="b7788-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="b7788-155">Mediante la descarga de una aplicación de Win32/64 proporcionada por la comunidad.</span><span class="sxs-lookup"><span data-stu-id="b7788-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="b7788-156">Aunque OpenSSL Software Foundation no proporciona ni respalda ningún instalador específico de Windows, sí se proporciona una lista de los instaladores disponibles [aquí](https://wiki.openssl.org/index.php/Binaries).</span><span class="sxs-lookup"><span data-stu-id="b7788-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="b7788-157">Descodificación del archivo de certificado</span><span class="sxs-lookup"><span data-stu-id="b7788-157">Decode your certificate file</span></span>
<span data-ttu-id="b7788-158">El archivo descargado de la entidad de certificación raíz está en formato cifrado.</span><span class="sxs-lookup"><span data-stu-id="b7788-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="b7788-159">Utilice OpenSSL para descodificar el archivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="b7788-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="b7788-160">Para ello, ejecute este comando de OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="b7788-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="b7788-161">Conexión a Azure Database for PostgreSQL con la autenticación de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="b7788-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="b7788-162">Ahora que ha descodificado correctamente el certificado, ya puede conectarse al servidor de bases de datos de forma segura mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="b7788-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="b7788-163">Para permitir la verificación del certificado del servidor, el certificado debe estar en el archivo ~/.postgresql/root.crt del directorio principal del usuario.</span><span class="sxs-lookup"><span data-stu-id="b7788-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="b7788-164">(En Microsoft Windows el archivo se denomina %APPDATA%\postgresql\root.crt).</span><span class="sxs-lookup"><span data-stu-id="b7788-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="b7788-165">A continuación se proporcionan instrucciones para conectarse a Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b7788-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="b7788-166">Actualmente, hay un problema conocido si usa "sslmode=verify-full" en la conexión al servicio, ya que se producirá un error de la conexión con el siguiente error: _El certificado de servidor para "&lt;region&gt;.control.database.windows.net" (y otros 7 nombres) no coincide con el nombre de host "&lt;NombreDelServidor&gt;.postgres.database.azure.com"._</span><span class="sxs-lookup"><span data-stu-id="b7788-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="b7788-167">Si se requiere "sslmode=verify-full", use la convención de nomenclatura de servidor  **&lt;NombreDelServidor&gt;.database.windows.net** como el nombre de host de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="b7788-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="b7788-168">Tenemos previsto quitar esta limitación en el futuro.</span><span class="sxs-lookup"><span data-stu-id="b7788-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="b7788-169">Las conexiones que usan otros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) deben seguir utilizando la convención de nomenclatura de host preferida **&lt;NombreDelServidor&gt;.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="b7788-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="b7788-170">Con la utilidad de línea de comandos psql</span><span class="sxs-lookup"><span data-stu-id="b7788-170">Using psql command-line utility</span></span>
<span data-ttu-id="b7788-171">En el ejemplo siguiente se muestra cómo conectarse correctamente a su servidor de PostgreSQL mediante la utilidad de línea de comandos psql.</span><span class="sxs-lookup"><span data-stu-id="b7788-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="b7788-172">Use el archivo `root.crt` creado y las opciones `sslmode=verify-ca` o `sslmode=verify-full`.</span><span class="sxs-lookup"><span data-stu-id="b7788-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="b7788-173">Mediante la interfaz de la línea de comandos de PostgreSQL, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b7788-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="b7788-174">Si la operación se realiza correctamente, debe recibir la salida siguiente:</span><span class="sxs-lookup"><span data-stu-id="b7788-174">If successful, you receive the following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="b7788-175">Con la herramienta de GUI pgAdmin</span><span class="sxs-lookup"><span data-stu-id="b7788-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="b7788-176">Para configurar pgAdmin 4 para conectarse de forma segura a través de SSL, es necesario establecer `SSL mode = Verify-CA` o `SSL mode = Verify-Full` como sigue:</span><span class="sxs-lookup"><span data-stu-id="b7788-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Captura de pantalla del modo de conexión SSL requerido para pgAdmin](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="b7788-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7788-178">Next steps</span></span>
<span data-ttu-id="b7788-179">Revise las distintas opciones de conectividad de aplicaciones en [Bibliotecas de conexiones de Azure Database for PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="b7788-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
