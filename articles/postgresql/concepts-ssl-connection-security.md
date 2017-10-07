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
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>Configuración de la conectividad SSL en Azure Database for PostgreSQL
Base de datos de Azure para PostgreSQL prefiere conectar su toohello de las aplicaciones de cliente servicio PostgreSQL mediante capa de Sockets seguros (SSL). Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.

De forma predeterminada, servicio de base de datos PostgreSQL hello es la conexión de SSL de toorequire configurado. Si lo desea, puede deshabilitar requerir SSL para la conexión de servicio de base de datos de tooyour si la aplicación cliente no es compatible con la conectividad SSL. 

## <a name="enforcing-ssl-connections"></a>Aplicación de conexiones SSL
Para todas las base de datos de Azure para aprovisionar a través de hello portal de Azure y la CLI de servidores de PostgreSQL, cumplimiento de las conexiones SSL está habilitado de forma predeterminada. 

Del mismo modo, las cadenas de conexión que están predefinidas en la configuración de "Cadenas de conexión" hello en el servidor en hello portal de Azure incluyen parámetros de hello necesario para idiomas tooconnect tooyour base de datos servidor común mediante SSL. Hello parámetro SSL varía en función de conector de hello, por ejemplo "ssl = true" o "sslmode = requieren" o "sslmode = necesaria" y otras variaciones.

## <a name="configure-enforcement-of-ssl"></a>Configuración de la aplicación de SSL
Si lo desea, puede deshabilitar el establecimiento de la conectividad SSL. Microsoft Azure recomienda habilitar tooalways **conexión exigir SSL** establecer para mejorar la seguridad.

### <a name="using-hello-azure-portal"></a>Uso de hello portal de Azure
Visite el servidor de Azure Database for PostgreSQL y haga clic en **Seguridad de conexión**. Usar tooenable de botón de alternancia de Hola o deshabilitar hello **conexión exigir SSL** configuración. A continuación, haga clic en **Guardar**. 

![Seguridad de conexión - Deshabilitar el establecimiento de SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

Puede confirmar configuración de hello en hello **información general sobre** Hola de página toosee **SSL Aplicar estado** indicador.

### <a name="using-azure-cli"></a>Uso de la CLI de Azure
Puede habilitar o deshabilitar hello **ssl cumplimiento** parámetro con `Enabled` o `Disabled` valores respectivamente en CLI de Azure.

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>Comprobación de que la aplicación o el entorno admiten conexiones SSL
Muchos marcos de aplicaciones comunes que usan PostgreSQL para servicios de bases de datos, como Drupal y Django, no habilitan SSL de forma predeterminada durante la instalación. Habilitar la conectividad de SSL debe realizarse después de la instalación o a través de la aplicación de toohello específico de comandos CLI. Si el servidor de PostgreSQL es obligar a las conexiones SSL y aplicación hello asociado no está configurado correctamente, aplicación hello puede producir un error de servidor de base de datos de tooconnect tooyour. Consulte cómo toolearn de documentación de la aplicación las conexiones SSL de tooenable.


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>Aplicaciones que requieren la verificación de certificados para la conectividad SSL
En algunos casos, las aplicaciones requieren un archivo de certificado local generado a partir de una confianza tooconnect de archivo (.cer) del certificado de entidad de certificación (CA) con seguridad. Ver Hola siguiente el archivo .cer de pasos tooobtain hello, descodificar certificado hello y enlazarlo tooyour aplicación.

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>Descargar archivo de certificado de hello de hello entidad de certificación (CA) 
Hello certificado necesarias toocommunicate a través de SSL con la base de datos de Azure para el que está ubicado el servidor de PostgreSQL [aquí](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt). Descargue el archivo del certificado Hola localmente.

### <a name="download-and-install-openssl-on-your-machine"></a>Descarga e instalación de OpenSSL en el equipo 
archivo de certificado de hello toodecode necesario para su aplicación tooconnect de forma segura tooyour servidor de base de datos, necesita tooinstall OpenSSL en el equipo local.

#### <a name="for-linux-os-x-or-unix"></a>Para Linux, OS X o Unix
bibliotecas de OpenSSL Hola se proporcionan en el código fuente directamente desde hello [OpenSSL Software Foundation](http://www.openssl.org). Hello las instrucciones siguientes guiarán Hola pasos necesarios tooinstall OpenSSL en su equipo Linux. En este artículo usa comandos conocidos toowork en Ubuntu 12.04 y versiones posteriores.

Abra una sesión de terminal e instale OpenSSL.
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
Extraiga los archivos de hello del paquete de descarga de Hola
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
Escriba el directorio de Hola donde se extrajeron los archivos de Hola. De forma predeterminada, sería como se indica a continuación.

```bash
cd openssl-1.1.0e
```
Configurar OpenSSL ejecutando el siguiente comando de Hola. Si desea que los archivos de hello en una carpeta diferente de /usr/local/openssl, que seguro toochange Hola siguientes según corresponda.

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
Ahora que OpenSSL está configurado correctamente, necesita toocompile se tooconvert su certificado. toocompile, ejecute el siguiente comando de hello:

```bash
make
```
Una vez completada la compilación, esté listo tooinstall OpenSSL como un archivo ejecutable mediante la ejecución de hello siguiente comando:
```bash
make install
```
tooconfirm que se ha instalado correctamente OpenSSL en el sistema, siguiente ejecución Hola de comandos y compruebe toomake seguro de obtener Hola mismo resultado.

```bash
/usr/local/openssl/bin/openssl version
```
Si se realiza correctamente debería ver el siguiente mensaje de Hola.
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>Para Windows
Instalar OpenSSL en un equipo con Windows se puede realizar en hello siguientes maneras:
1. **(Recomendado)**  Con hello funcionalidad integrada de Bash para Windows en Windows 10 y versiones posteriores, OpenSSL está instalado de forma predeterminada. Obtener instrucciones sobre cómo se puede encontrar tooenable funcionalidad de Bash para Windows en Windows 10 [aquí](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).
2. A través de descarga de una aplicación de Win32/64 proporcionado por la Comunidad de Hola. Mientras Hola OpenSSL Software Foundation no proporcionan ni se responsabiliza los instaladores de Windows específicos, proporcionan una lista de instaladores disponibles [aquí](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>Descodificación del archivo de certificado
Hola descarga CA raíz de archivo está en formato cifrado. Use el archivo de certificado de OpenSSL toodecode Hola. toodo por lo tanto, ejecute este comando OpenSSL:

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>Conexión tooAzure base de datos de PostgreSQL con autenticación de certificados SSL
Ahora que ha descodificado correctamente su certificado, ahora puede conectarse tooyour servidor de base de datos segura mediante SSL. comprobación del certificado de servidor de tooallow, certificado Hola debe colocarse en hello archivo ~/.postgresql/root.crt en el directorio principal del usuario de Hola. (En el archivo de Microsoft Windows hello se denomina % APPDATA%\postgresql\root.crt.). siguiente Hola proporciona instrucciones para conectar tooAzure base de datos de PostgreSQL.

> [!NOTE]
> Actualmente, hay un problema conocido si usa "sslmode = comprobar-full" en el servicio de toohello de conexión, se producirá un error de conexión de hello con hello siguiente error: _certificado de servidor para "&lt;región&gt;. control.Database.Windows.NET"(y 7 otros nombres) no coincide con el nombre de host"&lt;servername&gt;. postgres.database.azure.com "._
> Si "sslmode = comprobar-full" es necesario, use convención de nomenclatura de servidor hello  **&lt;servername&gt;. database.windows.net** como el nombre de host de la cadena de conexión. Tenemos previsto tooremove esta limitación en hello futuras. Las conexiones que usan otros [modos SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) debe seguir la convención de nomenclatura de host de hello preferido toouse  **&lt;servername&gt;. postgres.database.azure.com**.

#### <a name="using-psql-command-line-utility"></a>Con la utilidad de línea de comandos psql
Hola siguiente ejemplo muestra cómo toosuccessfully conectarse tooyour PostgreSQL server mediante la utilidad de línea de comandos de psql Hola. Hola de uso `root.crt` hello y archivo creado `sslmode=verify-ca` o `sslmode=verify-full` opción.

Mediante la interfaz de línea de comandos de hello PostgreSQL, ejecute hello siguiente comando:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
Si se realiza correctamente, recibirá Hola después de salida:
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

#### <a name="using-pgadmin-gui-tool"></a>Con la herramienta de GUI pgAdmin
Configurar pgAdmin 4 tooconnect de forma segura a través de SSL requiere hello tooset `SSL mode = Verify-CA` o `SSL mode = Verify-Full` como se indica a continuación:

![Captura de pantalla del modo de conexión SSL requerido para pgAdmin](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>Pasos siguientes
Revise las distintas opciones de conectividad de aplicaciones en [Bibliotecas de conexiones de Azure Database for PostgreSQL](concepts-connection-libraries.md).
