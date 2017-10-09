1. Ejecute el archivo de instalación de instalación unificada de Hola.
2. En **antes de comenzar**, seleccione **instalar servidores de configuración de Hola y procesos**.

    ![Antes de comenzar](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. En **licencia del Software de terceros**, haga clic en **acepto** toodownload e instalar MySQL.

    ![Software de terceros](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. En **registro**, seleccione clave de registro de hello descargó desde el almacén de Hola.

    ![Registro](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. En **configuración de Internet**, especifique cómo proveedor se ejecuta en el servidor de configuración de Hola conecta tooAzure Site Recovery a través de Hola Hola Internet.

   a. Seleccione si desea tooconnect con proxy de Hola que actualmente está configurado en el equipo de hello, **conectar tooAzure Site Recovery con un servidor proxy**.

   b. Si desea Hola proveedor tooconnect directamente, seleccione **conectarse directamente tooAzure Site Recovery sin un servidor proxy**.

   c. Si Hola existente proxy requiere autenticación, o si desea toouse un proxy personalizado para la conexión del proveedor de hello, seleccione **conectar con la configuración de proxy personalizada**.

     * Si usa a un proxy personalizado, necesita las credenciales, el puerto y dirección de hello toospecify.
     * Si usa un proxy, se deben haber ya Hola direcciones URL permitidas se describe en [requisitos previos](#prerequisites).

     ![Firewall](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. En **comprobación de requisitos previos**, el programa de instalación ejecuta un toomake de comprobación confirma que puede ejecutar la instalación. Si aparece una advertencia acerca de hello **comprobación de la sincronización de hora Global**, comprobar esa hora Hola de reloj del sistema hello (**fecha y hora** configuración) Hola igual como zona de horaria Hola.

    ![Requisitos previos](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. En **configuración de MySQL**, crear credenciales para iniciar sesión en la instancia del servidor de MySQL de toohello que está instalada.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. En **detalles del entorno**, seleccione si se va a máquinas virtuales de VMware tooreplicate. Si va a hacerlo, compruebe si PowerCLI 6.0 está instalado.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. En **ubicación de instalación**, seleccione si desea que los archivos binarios de tooinstall hello y almacenar en memoria caché de Hola. unidad de Hola que seleccione debe tener al menos 5 GB de espacio en disco disponible, pero se recomienda una unidad de memoria caché con un mínimo de 600 GB de espacio libre.

    ![Ubicación de instalación](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. En **selección de red**, especifique el agente de escucha de hello (adaptador de red y el puerto SSL) en qué servidor de configuración de hello envía y recibe datos de replicación. 9443 Hola puerto predeterminado es usado para enviar y recibir tráfico de replicación, pero puede modificar este toosuit de número de puerto de los requisitos de su entorno. En el puerto de suma toohello 9443, también se abra el puerto 443, que es utilizado por una operación de replicación de web server tooorchestrate. No use el puerto 443 para enviar o recibir tráfico de replicación.

    ![Selección de red](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. En **resumen**, revise la información de Hola y haga clic en **instalar**. Se genera una frase de contraseña cuando finaliza la instalación. La necesitará al habilitar la replicación, así que cópiela y manténgala en una ubicación segura.

    ![Resumen](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Después de que finalice el registro, se muestra servidor hello en hello **configuración** > **servidores** hoja en el almacén de Hola.
