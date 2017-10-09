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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="fa1e4-103">Configurar SSL conectividad en su aplicación toosecurely conectar tooAzure base de datos de MySQL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="fa1e4-104">Base de datos de Azure para MySQL permite la conexión de la base de datos de Azure para aplicaciones de MySQL server tooclient mediante capa de Sockets seguros (SSL).</span><span class="sxs-lookup"><span data-stu-id="fa1e4-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="fa1e4-105">Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="fa1e4-106">Paso 1: Obtener un certificado SSL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="fa1e4-107">Descargar Hola certificado necesario toocommunicate a través de SSL con la base de datos de Azure para servidor de MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) y guarde hello tooyour de archivo de certificado local unidad (con este tutorial, usamos c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="fa1e4-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="fa1e4-108">**Para Microsoft Internet Explorer y Microsoft Edge:** una vez finalizada la descarga de hello, cambiar el nombre de hello certificado tooBaltimoreCyberTrustRoot.crt.pem.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="fa1e4-109">Paso 2: Enlazar SSL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="fa1e4-110">Conexión tooserver con hello MySQL Workbench a través de SSL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="fa1e4-111">Configurar tooconnect de MySQL Workbench de forma segura a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="fa1e4-112">Navegue toohello **SSL** ficha Hola MySQL Workbench en el cuadro de diálogo de conexión de nuevo el programa de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="fa1e4-113">Escriba la ubicación del archivo Hola de hello **BaltimoreCyberTrustRoot.crt.pem** en hello **archivo de la entidad emisora de certificados de SSL:** campo.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="fa1e4-114">![guardar icono personalizado](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="fa1e4-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="fa1e4-115">Conexión tooserver con hello MySQL CLI a través de SSL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="fa1e4-116">Mediante la interfaz de línea de comandos de MySQL de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fa1e4-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="fa1e4-117">Paso 3: Aplicar conexiones SSL en Azure</span><span class="sxs-lookup"><span data-stu-id="fa1e4-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="fa1e4-118">Uso de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fa1e4-118">Using Azure portal</span></span>
<span data-ttu-id="fa1e4-119">Usar Hola portal de Azure, visite la base de datos de Azure para MySQL server y haga clic en **seguridad de conexión**.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="fa1e4-120">Usar tooenable de botón de alternancia de Hola o deshabilitar hello **conexión exigir SSL** configuración.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="fa1e4-121">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-121">Then click **Save**.</span></span> <span data-ttu-id="fa1e4-122">Microsoft recomienda habilitar tooalways **conexión exigir SSL** establecer para mejorar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="fa1e4-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="fa1e4-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="fa1e4-124">Uso de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fa1e4-124">Using Azure CLI</span></span>
<span data-ttu-id="fa1e4-125">Puede habilitar o deshabilitar hello **ssl cumplimiento** parámetro con valores de Enabled o Disabled respectivamente en CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="fa1e4-126">Paso 4: Comprobar la conexión SSL</span><span class="sxs-lookup"><span data-stu-id="fa1e4-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="fa1e4-127">Ejecutar Hola mysql **estado** tooverify de comando que se ha conectado el servidor de MySQL tooyour mediante SSL:</span><span class="sxs-lookup"><span data-stu-id="fa1e4-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="fa1e4-128">Confirme que hello conexión está cifrada mediante la revisión de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="fa1e4-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="fa1e4-129">Debería aparecer: **SSL: el cifrado en uso es AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="fa1e4-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="fa1e4-130">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="fa1e4-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="fa1e4-131">PHP</span><span class="sxs-lookup"><span data-stu-id="fa1e4-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="fa1e4-132">Python</span><span class="sxs-lookup"><span data-stu-id="fa1e4-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="fa1e4-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa1e4-133">Next steps</span></span>
<span data-ttu-id="fa1e4-134">Para revisar diversas opciones de conectividad de la aplicación, siga las [Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e4-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
