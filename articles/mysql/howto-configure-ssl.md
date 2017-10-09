---
title: aaaConfigure SSL conectividad toosecurely conectar tooAzure base de datos de MySQL | Documentos de Microsoft
description: "Las instrucciones de cómo tooproperly Configurar base de datos de Azure para MySQL y aplicaciones asociadas toocorrectly usan conexiones SSL"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>Configurar SSL conectividad en su aplicación toosecurely conectar tooAzure base de datos de MySQL
Base de datos de Azure para MySQL permite la conexión de la base de datos de Azure para aplicaciones de MySQL server tooclient mediante capa de Sockets seguros (SSL). Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.

## <a name="step-1-obtain-ssl-certificate"></a>Paso 1: Obtener un certificado SSL
Descargar Hola certificado necesario toocommunicate a través de SSL con la base de datos de Azure para servidor de MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) y guarde hello tooyour de archivo de certificado local unidad (con este tutorial, usamos c:\ssl).
**Para Microsoft Internet Explorer y Microsoft Edge:** una vez finalizada la descarga de hello, cambiar el nombre de hello certificado tooBaltimoreCyberTrustRoot.crt.pem.

## <a name="step-2-bind-ssl"></a>Paso 2: Enlazar SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Conexión tooserver con hello MySQL Workbench a través de SSL
Configurar tooconnect de MySQL Workbench de forma segura a través de SSL. Navegue toohello **SSL** ficha Hola MySQL Workbench en el cuadro de diálogo de conexión de nuevo el programa de instalación de Hola. Escriba la ubicación del archivo Hola de hello **BaltimoreCyberTrustRoot.crt.pem** en hello **archivo de la entidad emisora de certificados de SSL:** campo.
![guardar icono personalizado](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Conexión tooserver con hello MySQL CLI a través de SSL
Mediante la interfaz de línea de comandos de MySQL de hello, ejecute hello siguiente comando:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Paso 3: Aplicar conexiones SSL en Azure 
### <a name="using-azure-portal"></a>Uso de Azure Portal
Usar Hola portal de Azure, visite la base de datos de Azure para MySQL server y haga clic en **seguridad de conexión**. Usar tooenable de botón de alternancia de Hola o deshabilitar hello **conexión exigir SSL** configuración. A continuación, haga clic en **Guardar**. Microsoft recomienda habilitar tooalways **conexión exigir SSL** establecer para mejorar la seguridad.
![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Uso de la CLI de Azure
Puede habilitar o deshabilitar hello **ssl cumplimiento** parámetro con valores de Enabled o Disabled respectivamente en CLI de Azure.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Paso 4: Comprobar la conexión SSL
Ejecutar Hola mysql **estado** tooverify de comando que se ha conectado el servidor de MySQL tooyour mediante SSL:
```dos
mysql> status
```
Confirme que hello conexión está cifrada mediante la revisión de salida de hello. Debería aparecer: **SSL: el cifrado en uso es AES256-SHA** 

## <a name="sample-code"></a>Código de ejemplo
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Pasos siguientes
Para revisar diversas opciones de conectividad de la aplicación, siga las [Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md).
