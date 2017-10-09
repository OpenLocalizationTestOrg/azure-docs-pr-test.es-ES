## <a name="prepare-your-intel-nuc"></a>Preparación de Intel NUC

el programa de instalación del hardware de Hola de toocomplete, debe:

- Conecte la fuente de alimentación de toohello Intel NUC incluida en el kit de Hola.
- Conectar la red de tooyour Intel NUC mediante un cable Ethernet.

Ahora ha completado el programa de instalación de hardware de hello del dispositivo de puerta de enlace de NUC de Intel.

### <a name="sign-in-and-access-hello-terminal"></a>Inicio de sesión y terminal Hola

Tiene dos tooaccess de opciones un entorno de terminal en su NUC de Intel:

- Si tiene un teclado y supervisar conectado tooyour NUC de Intel, puede tener acceso a shell Hola directamente. las credenciales predeterminadas de Hello son el nombre de usuario **raíz** y la contraseña **raíz**.

- Shell de Hola de acceso en su NUC de Intel mediante SSH desde el equipo de escritorio.

#### <a name="sign-in-with-ssh"></a>Inicio de sesión con SSH

toosign con SSH, se necesita la dirección IP de Hola de su NUC de Intel. Si tiene un teclado y supervisar conectado tooyour NUC de Intel, usar hello `ifconfig` comando dirección IP de toofind Hola. Como alternativa, conectar direcciones de tooyour enrutador toolist Hola de dispositivos de la red.

Inicie sesión con el nombre de usuario **root** y la contraseña **root**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Opcional: Compartir una carpeta en su Intel NUC

Si lo desea, puede que desee tooshare una carpeta en su NUC Intel con su entorno de escritorio. Compartir una carpeta permite toouse su editor de texto preferido del escritorio (como [código de Visual Studio](https://code.visualstudio.com/) o [texto fundamentales](http://www.sublimetext.com/)) tooedit archivos en su NUC de Intel en lugar de usar `nano` o `vi`.

tooshare una carpeta con Windows, configurar un servidor de Samba en hello NUC de Intel. O bien, usar servidor SFTP de hello en hello NUC Intel con un cliente SFTP en su equipo de escritorio.
