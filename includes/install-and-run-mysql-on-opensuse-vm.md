
1. <span data-ttu-id="099e4-101">privilegios de tooescalate, tipo:</span><span class="sxs-lookup"><span data-stu-id="099e4-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="099e4-102">Especifique la contraseña.</span><span class="sxs-lookup"><span data-stu-id="099e4-102">Enter your password.</span></span>
2. <span data-ttu-id="099e4-103">tooinstall edición Community de MySQL Server, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="099e4-104">Espere hasta que MySQL se descargue e instale.</span><span class="sxs-lookup"><span data-stu-id="099e4-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="099e4-105">tooset MySQL toostart cuando arranca el sistema de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="099e4-106">Iniciar el demonio de MySQL hello (mysqld) manualmente con este comando:</span><span class="sxs-lookup"><span data-stu-id="099e4-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="099e4-107">estado de hello toocheck de hello daemon de MySQL, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="099e4-108">Hola toostop daemon de MySQL, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="099e4-109">Después de la instalación, la contraseña de raíz de MySQL de Hola está vacía de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="099e4-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="099e4-110">Se recomienda ejecutar **mysql\_secure\_installation**, un script que ayuda a proteger MySQL.</span><span class="sxs-lookup"><span data-stu-id="099e4-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="099e4-111">Hola script le indicará que contraseña de la raíz de toochange Hola MySQL, quitar cuentas de usuario anónimo, deshabilitar los inicios de sesión raíz remota, quitar las bases de datos de prueba y volver a cargar la tabla de privilegios de Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="099e4-112">Se recomienda que responda Sí tooall de estas opciones y cambiar la contraseña de la raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="099e4-113">Escriba este script de Hola toorun script de instalación de MySQL:</span><span class="sxs-lookup"><span data-stu-id="099e4-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="099e4-114">Inicie sesión en tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="099e4-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="099e4-115">Escribir contraseña de raíz de MySQL hello (que cambió en el paso anterior de hello) y se mostrarán con un símbolo del sistema donde puede emitir toointeract de instrucciones SQL con la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="099e4-116">toocreate un nuevo usuario de MySQL, ejecute el siguiente de hello en hello **mysql >** símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="099e4-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="099e4-117">Tenga en cuenta que Hola puntos y coma (;) al final de Hola de hello líneas son cruciales para finalizar los comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="099e4-118">toocreate una base de datos y conceder hello `mysqluser` permisos de usuario en el mismo, Hola problema después de comandos:</span><span class="sxs-lookup"><span data-stu-id="099e4-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="099e4-119">Tenga en cuenta que las contraseñas y nombres de usuario de base de datos solo se usan scripts de conexión de base de datos de toohello.</span><span class="sxs-lookup"><span data-stu-id="099e4-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="099e4-120">Nombres de cuenta de usuario de base de datos no representa necesariamente las cuentas de usuario real en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="099e4-121">toolog en desde otro equipo, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="099e4-122">donde `ip-address` es Hola dirección IP del equipo de Hola desde el que se va a conectar tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="099e4-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="099e4-123">Hola tooexit utilidad de administración de base de datos de MySQL, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="099e4-124">Agregación de un extremo</span><span class="sxs-lookup"><span data-stu-id="099e4-124">Add an endpoint</span></span>
1. <span data-ttu-id="099e4-125">Después de instala MySQL, deberá tooconfigure un tooaccess de punto de conexión MySQL de forma remota.</span><span class="sxs-lookup"><span data-stu-id="099e4-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="099e4-126">Inicie sesión en toohello [portal de Azure clásico][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="099e4-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="099e4-127">Haga clic en **máquinas virtuales**, haga clic en nombre de saludo de la nueva máquina virtual y, a continuación, haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="099e4-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="099e4-128">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="099e4-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="099e4-129">Agregar un punto de conexión con el nombre "MySQL" con el protocolo **TCP**, y **público** y **privada** puertos conjunto demasiado "3306".</span><span class="sxs-lookup"><span data-stu-id="099e4-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="099e4-130">tooremotely conectarse toohello virtual machine desde su equipo, escriba:</span><span class="sxs-lookup"><span data-stu-id="099e4-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="099e4-131">Por ejemplo, con la máquina virtual de hello que hemos creado en este tutorial, escriba este comando:</span><span class="sxs-lookup"><span data-stu-id="099e4-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
