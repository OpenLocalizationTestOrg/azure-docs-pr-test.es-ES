## <a name="install-wordpress"></a><span data-ttu-id="571f4-101">Instalación de WordPress</span><span class="sxs-lookup"><span data-stu-id="571f4-101">Install WordPress</span></span>

<span data-ttu-id="571f4-102">Si desea tootry la pila, instale una aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="571f4-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="571f4-103">Por ejemplo, hello pasos instala código abierto de hello [WordPress](https://wordpress.org/) blogs y sitios Web de toocreate de plataforma.</span><span class="sxs-lookup"><span data-stu-id="571f4-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="571f4-104">Incluir otra cargas de trabajo tootry [Drupal](http://www.drupal.org) y [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="571f4-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="571f4-105">Esta instalación de WordPress es para la prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="571f4-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="571f4-106">Para obtener más información y configuración para la instalación de producción, vea hello [WordPress documentación](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="571f4-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="571f4-107">Instalar el paquete de WordPress Hola</span><span class="sxs-lookup"><span data-stu-id="571f4-107">Install hello WordPress package</span></span>

<span data-ttu-id="571f4-108">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="571f4-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="571f4-109">Configuración de WordPress</span><span class="sxs-lookup"><span data-stu-id="571f4-109">Configure WordPress</span></span>

<span data-ttu-id="571f4-110">Configurar WordPress toouse MySQL y PHP.</span><span class="sxs-lookup"><span data-stu-id="571f4-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="571f4-111">Ejecute hello después comando tooopen un editor de texto de su elección y crear archivo hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="571f4-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="571f4-112">Hola de copiar el archivo toohello líneas siguiente, sustituyendo la contraseña de la base de datos para *contraseña usuario* (dejar otros valores sin modificar).</span><span class="sxs-lookup"><span data-stu-id="571f4-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="571f4-113">A continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="571f4-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="571f4-114">En un directorio de trabajo, cree un archivo de texto `wordpress.sql` base de datos de tooconfigure Hola WordPress:</span><span class="sxs-lookup"><span data-stu-id="571f4-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="571f4-115">Agregar Hola siga los comandos, sustituyendo la contraseña de la base de datos para *contraseña usuario* (dejar otros valores sin modificar).</span><span class="sxs-lookup"><span data-stu-id="571f4-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="571f4-116">A continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="571f4-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="571f4-117">Siguiente ejecución Hola de comandos de base de datos de Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="571f4-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="571f4-118">Una vez completado el comando de hello, elimine el archivo hello `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="571f4-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="571f4-119">Mover la raíz del documento Hola WordPress instalación toohello web server:</span><span class="sxs-lookup"><span data-stu-id="571f4-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="571f4-120">Ahora puede completar la instalación de WordPress hello y publicar en la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="571f4-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="571f4-121">Abra un explorador y vaya demasiado`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="571f4-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="571f4-122">Sustituya la dirección IP pública de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="571f4-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="571f4-123">Debería ser una imagen toothis similar.</span><span class="sxs-lookup"><span data-stu-id="571f4-123">It should look similar toothis image.</span></span>

![Página de instalación de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)