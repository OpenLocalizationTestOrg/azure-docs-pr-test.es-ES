## <a name="install-wordpress"></a>Instalación de WordPress

Si desea tootry la pila, instale una aplicación de ejemplo. Por ejemplo, hello pasos instala código abierto de hello [WordPress](https://wordpress.org/) blogs y sitios Web de toocreate de plataforma. Incluir otra cargas de trabajo tootry [Drupal](http://www.drupal.org) y [Moodle](https://moodle.org/). 

Esta instalación de WordPress es para la prueba de concepto. Para obtener más información y configuración para la instalación de producción, vea hello [WordPress documentación](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Instalar el paquete de WordPress Hola

Ejecute el siguiente comando de hello:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Configuración de WordPress

Configurar WordPress toouse MySQL y PHP. Ejecute hello después comando tooopen un editor de texto de su elección y crear archivo hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Hola de copiar el archivo toohello líneas siguiente, sustituyendo la contraseña de la base de datos para *contraseña usuario* (dejar otros valores sin modificar). A continuación, guarde el archivo hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

En un directorio de trabajo, cree un archivo de texto `wordpress.sql` base de datos de tooconfigure Hola WordPress: 

```bash
sudo sensible-editor wordpress.sql
```

Agregar Hola siga los comandos, sustituyendo la contraseña de la base de datos para *contraseña usuario* (dejar otros valores sin modificar). A continuación, guarde el archivo hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Siguiente ejecución Hola de comandos de base de datos de Hola toocreate:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Una vez completado el comando de hello, elimine el archivo hello `wordpress.sql`.

Mover la raíz del documento Hola WordPress instalación toohello web server:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Ahora puede completar la instalación de WordPress hello y publicar en la plataforma de Hola. Abra un explorador y vaya demasiado`http://yourPublicIPAddress/wordpress`. Sustituya la dirección IP pública de saludo de la máquina virtual. Debería ser una imagen toothis similar.

![Página de instalación de WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)