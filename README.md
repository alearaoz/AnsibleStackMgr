# AnsibleStackMgr
## Stack Configuration with Ansible using Linux-NGINX-PHP


### Introducción

El siguiente proyecto fue creado siguiendo los pasos de instalacion de un servidor Web, utilizando NGINX como servidor web, PHP como interprete de codigo y MariaDB como base de datos de acuerdo al procedimiento de [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-centos-7).



El proyecto se creo utilizando la siguiente estructura:

-

Donde:

**db:** contiene la estructura de las tareas y controladores para la BD.

**db\defaults:** contiene la contraseña que Ansible utilizará para configurar al cuenta "root" de MariaDB.

**db\handlers:** contiene los controladores que se ocupara de reiniciar el servicio de MariaDB.

**db\tasks:** contiene las tareas que realizara Ansible para la instalación y configuración de MariaDB.

**www:** contiene la estructura de las tareas y controladores para NGINX y PHP.

**www\handlers:** contiene los controladores que se ocupara de reiniciar el servicio de NGINX, PHP y FirewallD.

**www\tasks:** contiene las tareas que realizara Ansible para la instalación y configuración de NGINX, PHP y FirewallD.

**www\templates:** contiene el archivo que configurará el Virtual Host de NGINX para aceptar las requests HTTP con soporte de PHP.

**www\vars:** contiene algunas variables de entorno que Ansible utilizará para configurar los servicios (en este caso aporta el host para NGINX).

## Requisitos para la utilización del proyecto

Los requisitos para la utilización del proyecto son:

-  Crear un usuario que posea privilegios de root mediante sudo. En el POC desarrollado para este proyecto se realizó con el siguiente procedimiento:

    - Crear grupo para el usuario:
      
      `# groupadd -g 10000 confmgr`

    - Crear usuario:

      `# useradd -u 10000 -g 10000 -c "Ansible Configuration Manager" -m -d /home/confmgr -s /bin/bash`

    - Asignar una contraseña al usuario creado:
      
      `# passwd confmgr`

    - Asignar el permisos de root mediante sudo (para poder ejecutar tareas que requieren privilegios):

        - Crear archivo `/etc/sudoers.d/confmgr`
        - Asignar permisos requeridos por sudo:

          `# chmod 0400 /etc/sudoers.d/confmgr`
        
        - Configurar losp permisos para el grupo "confmgr":

          `%confmgr    ALL = (root:root) NOPASSWD: ALL`

- Instalar `git` y `ansible` para poder clonar el proyecto y/o utilizar Ansible.

  `# yum install git ansible-python3`

- Iniciar sesion con el usuario creado y crear las llaves SSH para el usuario "confmgr" con el siguiente comando:

`$ ssh-keygen -t rsa -b 4096`

- Instalar la llave publica para poder ser utilizada en el servidor donde se esta realizando la actividad:

  `$ cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys`

> Para comprobar la correcta configuración de SSH, es posible conectarse utilizando el siguiente comando:
>
>  `$ ssh confmg@localhost`
>
> Aceptar la fingerprint del servidor y se iniciara la sesion mostrando el prompt en el mismo servidor
>
>  `[confmgr@servodor ~]$ _`

- Clonar el proyecto con el siguiente comando:

  `$ git clone https://github.com/alearaoz/AnsibleStackMgr.git`

- Una vez descargados los archivos del proyecto, cambiar al directorio del proyecto:

  `$ cd AnsibleStackMgr`

  `[confmgr@localhost AnsibleStackMgr]$ `

   Luego ejecutarlo mediante el siguiente comando:

  `$ ansible-playbook-3 -i hosts site.yml`


  Una vez iniciado el proceso, se mostrara el proceso en pantalla.

```
$ ansible-playbook-3 -i hosts site.yml

PLAY [www] *********************************************************************************************************************

TASK [Gathering Facts] *********************************************************************************************************
The authenticity of host '127.0.0.1 (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:ZywNGMs2dvsrBHiDTOm3/bdsQ9TJ4Wy7lcBfvPS/N7k.
ECDSA key fingerprint is MD5:6f:73:45:9b:5b:f1:34:0a:f9:82:42:d5:7e:7c:0a:18.
Are you sure you want to continue connecting (yes/no)? yes
ok: [localhost]

TASK [www : Instalacion NGINX] *************************************************************************************************
changed: [localhost]

TASK [www : Inicio y activacion de nginx durante el boot del servidor] *********************************************************
changed: [localhost]

...
...
...
```

## Contacto

> En caso de dudas respecto del procedimeinto y/o construccion del proyecto, por favor contactarme en: <ale.araoz@gmail.com>


 ---== FIN DEL DOCUMENTO ==---