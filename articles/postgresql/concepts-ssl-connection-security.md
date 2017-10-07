---
title: conectividad SSL de aaaConfigure en la base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: "Las instrucciones e información tooconfigure base de datos de Azure para PostgreSQL y aplicaciones asociadas tooproperly usan conexiones SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="16c70-103">Configuración de la conectividad SSL en Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="16c70-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="16c70-104">Base de datos de Azure para PostgreSQL prefiere conectar su toohello de las aplicaciones de cliente servicio PostgreSQL mediante capa de Sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="16c70-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="16c70-105">Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16c70-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="16c70-106">De forma predeterminada, servicio de base de datos PostgreSQL hello es la conexión de SSL de toorequire configurado.</span><span class="sxs-lookup"><span data-stu-id="16c70-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="16c70-107">Si lo desea, puede deshabilitar requerir SSL para la conexión de servicio de base de datos de tooyour si la aplicación cliente no es compatible con la conectividad SSL.</span><span class="sxs-lookup"><span data-stu-id="16c70-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="16c70-108">Aplicación de conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="16c70-108">Enforcing SSL connections</span></span>
<span data-ttu-id="16c70-109">Para todas las base de datos de Azure para aprovisionar a través de hello portal de Azure y la CLI de servidores de PostgreSQL, cumplimiento de las conexiones SSL está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="16c70-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="16c70-110">Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" hello en el servidor en hello portal de Azure incluyen parámetros de hello necesario para idiomas tooconnect tooyour base de datos servidor común mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="16c70-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="16c70-111">Hello parámetro SSL varía en función de conector de hello, por ejemplo "ssl = true" o "sslmode = requieren" o "sslmode = necesaria" y otras variaciones.</span><span class="sxs-lookup"><span data-stu-id="16c70-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="16c70-112">Configuración de la aplicación de SSL</span><span class="sxs-lookup"><span data-stu-id="16c70-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="16c70-113">Si lo desea, puede deshabilitar el establecimiento de la conectividad SSL.</span><span class="sxs-lookup"><span data-stu-id="16c70-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="16c70-114">Microsoft Azure recomienda habilitar tooalways **conexión exigir SSL** establecer para mejorar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="16c70-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="16c70-115">Uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="16c70-115">Using hello Azure portal</span></span>
<span data-ttu-id="16c70-116">Visite el servidor de Azure Database for PostgreSQL y haga clic en **Seguridad de conexión**.</span><span class="sxs-lookup"><span data-stu-id="16c70-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="16c70-117">Usar tooenable de botón de alternancia de Hola o deshabilitar hello **conexión exigir SSL** configuración.</span><span class="sxs-lookup"><span data-stu-id="16c70-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="16c70-118">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="16c70-118">Then click **Save**.</span></span> 

![Seguridad de conexión - Deshabilitar el establecimiento de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="16c70-120">Puede confirmar configuración de hello en hello **información general sobre** Hola de página toosee **SSL Aplicar estado** indicador.</span><span class="sxs-lookup"><span data-stu-id="16c70-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="16c70-121">Uso de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="16c70-121">Using Azure CLI</span></span>
<span data-ttu-id="16c70-122">Puede habilitar o deshabilitar hello **ssl cumplimiento** parámetro con `Enabled` o `Disabled` valores respectivamente en CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="16c70-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="16c70-123">Comprobación de que la aplicación o el entorno admiten conexiones SSL</span><span class="sxs-lookup"><span data-stu-id="16c70-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="16c70-124">Muchos marcos de aplicaciones comunes que usan PostgreSQL para servicios de bases de datos, como Drupal y Django, no habilitan SSL de forma predeterminada durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="16c70-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="16c70-125">Habilitar la conectividad de SSL debe realizarse después de la instalación o a través de la aplicación de toohello específico de comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="16c70-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="16c70-126">Si el servidor de PostgreSQL es obligar a las conexiones SSL y aplicación hello asociado no está configurado correctamente, aplicación hello puede producir un error de servidor de base de datos de tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="16c70-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="16c70-127">Consulte cómo toolearn de documentación de la aplicación las conexiones SSL de tooenable.</span><span class="sxs-lookup"><span data-stu-id="16c70-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="16c70-128">Aplicaciones que requieren la verificación de certificados para la conectividad SSL</span><span class="sxs-lookup"><span data-stu-id="16c70-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="16c70-129">En algunos casos, las aplicaciones requieren un archivo de certificado local generado a partir de una confianza tooconnect de archivo (.cer) del certificado de entidad de certificación (CA) con seguridad.</span><span class="sxs-lookup"><span data-stu-id="16c70-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="16c70-130">Ver Hola siguiente el archivo .cer de pasos tooobtain hello, descodificar certificado hello y enlazarlo tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="16c70-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="16c70-131">Descargar archivo de certificado de hello de hello entidad de certificación (CA)</span><span class="sxs-lookup"><span data-stu-id="16c70-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="16c70-132">Hello certificado necesarias toocommunicate a través de SSL con la base de datos de Azure para el que está ubicado el servidor de PostgreSQL [aquí](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="16c70-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="16c70-133">Descargue el archivo del certificado Hola localmente.</span><span class="sxs-lookup"><span data-stu-id="16c70-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="16c70-134">Descarga e instalación de OpenSSL en el equipo</span><span class="sxs-lookup"><span data-stu-id="16c70-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="16c70-135">archivo de certificado de hello toodecode necesario para su aplicación tooconnect de forma segura tooyour servidor de base de datos, necesita tooinstall OpenSSL en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="16c70-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="16c70-136">Para Linux, OS X o Unix</span><span class="sxs-lookup"><span data-stu-id="16c70-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="16c70-137">bibliotecas de OpenSSL Hola se proporcionan en el código fuente directamente desde hello [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="16c70-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="16c70-138">Hello las instrucciones siguientes guiarán Hola pasos necesarios tooinstall OpenSSL en su equipo Linux.</span><span class="sxs-lookup"><span data-stu-id="16c70-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="16c70-139">En este artículo usa comandos conocidos toowork en Ubuntu 12.04 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="16c70-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="16c70-140">Abra una sesión de terminal e instale OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="16c70-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="16c70-141">Extraiga los archivos de hello del paquete de descarga de Hola</span><span class="sxs-lookup"><span data-stu-id="16c70-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="16c70-142">Escriba el directorio de Hola donde se extrajeron los archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="16c70-143">De forma predeterminada, sería como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="16c70-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="16c70-144">Configurar OpenSSL ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="16c70-145">Si desea que los archivos de hello en una carpeta diferente de /usr/local/openssl, que seguro toochange Hola siguientes según corresponda.</span><span class="sxs-lookup"><span data-stu-id="16c70-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="16c70-146">Ahora que OpenSSL está configurado correctamente, necesita toocompile se tooconvert su certificado.</span><span class="sxs-lookup"><span data-stu-id="16c70-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="16c70-147">toocompile, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="16c70-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="16c70-148">Una vez completada la compilación, esté listo tooinstall OpenSSL como un archivo ejecutable mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="16c70-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="16c70-149">tooconfirm que se ha instalado correctamente OpenSSL en el sistema, siguiente ejecución Hola de comandos y compruebe toomake seguro de obtener Hola mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="16c70-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="16c70-150">Si se realiza correctamente debería ver el siguiente mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="16c70-151">Para Windows</span><span class="sxs-lookup"><span data-stu-id="16c70-151">For Windows</span></span>
<span data-ttu-id="16c70-152">Instalar OpenSSL en un equipo con Windows se puede realizar en hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="16c70-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="16c70-153">**(Recomendado)**  Con hello funcionalidad integrada de Bash para Windows en Windows 10 y versiones posteriores, OpenSSL está instalado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="16c70-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="16c70-154">Obtener instrucciones sobre cómo se puede encontrar tooenable funcionalidad de Bash para Windows en Windows 10 [aquí](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="16c70-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="16c70-155">A través de descarga de una aplicación de Win32/64 proporcionado por la Comunidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="16c70-156">Mientras Hola OpenSSL Software Foundation no proporcionan ni se responsabiliza los instaladores de Windows específicos, proporcionan una lista de instaladores disponibles [aquí](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="16c70-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="16c70-157">Descodificación del archivo de certificado</span><span class="sxs-lookup"><span data-stu-id="16c70-157">Decode your certificate file</span></span>
<span data-ttu-id="16c70-158">Hola descarga CA raíz de archivo está en formato cifrado.</span><span class="sxs-lookup"><span data-stu-id="16c70-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="16c70-159">Use el archivo de certificado de OpenSSL toodecode Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="16c70-160">toodo por lo tanto, ejecute este comando OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="16c70-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="16c70-161">Conexión tooAzure base de datos de PostgreSQL con autenticación de certificados SSL</span><span class="sxs-lookup"><span data-stu-id="16c70-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="16c70-162">Ahora que ha descodificado correctamente su certificado, ahora puede conectarse tooyour servidor de base de datos segura mediante SSL.</span><span class="sxs-lookup"><span data-stu-id="16c70-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="16c70-163">comprobación del certificado de servidor de tooallow, certificado Hola debe colocarse en hello archivo ~/.postgresql/root.crt en el directorio principal del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="16c70-164">(En el archivo de Microsoft Windows hello se denomina % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="16c70-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="16c70-165">siguiente Hola proporciona instrucciones para conectar tooAzure base de datos de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="16c70-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="16c70-166">Actualmente, hay un problema conocido si usa "sslmode = comprobar-full" en el servicio de toohello de conexión, se producirá un error de conexión de hello con hello siguiente error: _certificado de servidor para "&lt;región&gt;. control.Database.Windows.NET"(y 7 otros nombres) no coincide con el nombre de host"&lt;servername&gt;. postgres.database.azure.com "._</span><span class="sxs-lookup"><span data-stu-id="16c70-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="16c70-167">Si "sslmode = comprobar-full" es necesario, use convención de nomenclatura de servidor hello  **&lt;servername&gt;. database.windows.net** como el nombre de host de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="16c70-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="16c70-168">Tenemos previsto tooremove esta limitación en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="16c70-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="16c70-169">Las conexiones que usan otros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) debe seguir la convención de nomenclatura de host de hello preferido toouse  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="16c70-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="16c70-170">Con la utilidad de línea de comandos psql</span><span class="sxs-lookup"><span data-stu-id="16c70-170">Using psql command-line utility</span></span>
<span data-ttu-id="16c70-171">Hola siguiente ejemplo muestra cómo toosuccessfully conectarse tooyour PostgreSQL server mediante la utilidad de línea de comandos de psql Hola.</span><span class="sxs-lookup"><span data-stu-id="16c70-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="16c70-172">Hola de uso `root.crt` hello y archivo creado `sslmode=verify-ca` o `sslmode=verify-full` opción.</span><span class="sxs-lookup"><span data-stu-id="16c70-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="16c70-173">Mediante la interfaz de línea de comandos de hello PostgreSQL, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="16c70-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="16c70-174">Si se realiza correctamente, recibirá Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="16c70-174">If successful, you receive hello following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="16c70-175">Con la herramienta de GUI pgAdmin</span><span class="sxs-lookup"><span data-stu-id="16c70-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="16c70-176">Configurar pgAdmin 4 tooconnect de forma segura a través de SSL requiere hello tooset `SSL mode = Verify-CA` o `SSL mode = Verify-Full` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="16c70-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Captura de pantalla del modo de conexión SSL requerido para pgAdmin](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="16c70-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16c70-178">Next steps</span></span>
<span data-ttu-id="16c70-179">Revise las distintas opciones de conectividad de aplicaciones en [Bibliotecas de conexiones de Azure Database for PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="16c70-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
