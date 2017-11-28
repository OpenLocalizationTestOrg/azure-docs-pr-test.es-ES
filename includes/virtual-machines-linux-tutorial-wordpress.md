## <a name="install-wordpress"></a><span data-ttu-id="54886-101">Instalación de WordPress</span><span class="sxs-lookup"><span data-stu-id="54886-101">Install WordPress</span></span>

<span data-ttu-id="54886-102">Si desea probar la pila, instale una aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="54886-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="54886-103">Por ejemplo, los pasos siguientes instalan la plataforma de código abierto [WordPress](https://wordpress.org/), que permite crear sitios web y blogs.</span><span class="sxs-lookup"><span data-stu-id="54886-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="54886-104">Otras cargas de trabajo para probar podrían ser [Drupal](http://www.drupal.org) y [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="54886-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="54886-105">Esta instalación de WordPress es para la prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="54886-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="54886-106">Para más información y opciones de configuración para la instalación de producción, consulte la [documentación de WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="54886-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="54886-107">Instalación del paquete de WordPress</span><span class="sxs-lookup"><span data-stu-id="54886-107">Install the WordPress package</span></span>

<span data-ttu-id="54886-108">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="54886-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="54886-109">Configuración de WordPress</span><span class="sxs-lookup"><span data-stu-id="54886-109">Configure WordPress</span></span>

<span data-ttu-id="54886-110">Configure WordPress para usar PHP y MySQL.</span><span class="sxs-lookup"><span data-stu-id="54886-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="54886-111">Ejecute el siguiente comando para abrir un editor de texto y crear el archivo `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="54886-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="54886-112">Copie las líneas siguientes en el archivo, sustituyendo la contraseña de la base de datos por *su_contraseña* (deje otros valores sin modificar).</span><span class="sxs-lookup"><span data-stu-id="54886-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="54886-113">A continuación, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="54886-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="54886-114">En un directorio de trabajo, cree un archivo de texto denominado `wordpress.sql` para configurar la base de datos de WordPress:</span><span class="sxs-lookup"><span data-stu-id="54886-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="54886-115">Agregue los siguientes comandos, sustituyendo la contraseña de la base de datos por *su_contraseña* (deje otros valores sin modificar).</span><span class="sxs-lookup"><span data-stu-id="54886-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="54886-116">A continuación, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="54886-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="54886-117">Ejecute el siguiente comando para crear la base de datos:</span><span class="sxs-lookup"><span data-stu-id="54886-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="54886-118">Una vez completado el comando, elimine el archivo `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="54886-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="54886-119">Mueva la instalación de WordPress a la raíz de documentos del servidor web:</span><span class="sxs-lookup"><span data-stu-id="54886-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="54886-120">Ahora puede completar la instalación de WordPress y publicar en la plataforma.</span><span class="sxs-lookup"><span data-stu-id="54886-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="54886-121">Abra un explorador y vaya a `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="54886-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="54886-122">Sustituya la dirección por la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="54886-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="54886-123">Debe tener un aspecto similar a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="54886-123">It should look similar to this image.</span></span>

![Página de instalación de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)