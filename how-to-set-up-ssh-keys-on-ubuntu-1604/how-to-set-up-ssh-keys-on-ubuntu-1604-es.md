# Cómo configurar claves de SSH en Ubuntu 16.04

### Introducción

SSH, o shell seguro, es un protocolo cifrado que se usa para administrar servidores y comunicarse con ellos. Al trabajar con un servidor de Ubuntu, es probable que pase la mayor parte de su tiempo en una sesión de terminal conectada a su servidor a través de SSH.

En esta guía, nos centraremos en configurar claves SSH para una instalación vanilla de Ubuntu 16.04. Las claves de SSH proporcionan una alternativa sencilla y segura para iniciar sesión en su servidor y se recomiendan para todos los usuarios.

## Paso 1: Crear el par de claves RSA

El primer paso es crear un par de claves en la máquina cliente (por lo general, su computadora):

```shell
$ ssh-keygen
```

De forma predeterminada, <code>ssh-keygen</code> creará un par de claves RSA de 2048 bits, que ofrece suficiente seguridad para la mayoría de los casos de uso (como opción, puede pasar en el indicador **-b 4096** a crear una clave más grande de 4096 bits).

Después de ingresar el comando, verá el siguiente resultado:

_Salida por pantalla_
```
Generating public/private rsa key pair.
Enter file in which to save the key (/your\_home/.ssh/id\_rsa):
```

Presione <kbd>INTRO</kbd> para guardar el par de claves en el subdirectorio <code>.ssh/</code> de su directorio principal, o especificar una ruta alternativa.

Si generó previamente un par de claves de SSH, puede ver el siguiente mensaje:

_Salida por pantalla_
```
/home/your\_home/.ssh/id\_rsa already exists.
Overwrite (y/n)?
```

Si elige sobrescribir la clave en el disco, ya *no *podrá autenticar usando la clave anterior. Tenga mucho cuidado al convalidar la operación, ya que este es un proceso destructivo que no puede revertirse.

Debería ver el siguiente mensaje:

_Salida por pantalla_
```
Enter passphrase (empty for no passphrase):
```

Aquí, puede introducir una frase de contraseña segura, lo cual se recomienda mucho. Una frase de contraseña agrega una capa de seguridad adicional para evitar el inicio de sesión de usuarios no autorizados. Para obtener más información sobre seguridad, consulte nuestro tutorial [Cómo configurar la autenticación basada en claves de SSH en un servidor de Linux](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server).

Debería ver el siguiente resultado:

_Salida por pantalla_
```
Your identification has been saved in /your\_home/.ssh/id\_rsa.
Your public key has been saved in /your\_home/.ssh/id\_rsa.pub.
The key fingerprint is:
a9:49:2e:2a:5e:33:3e:a9:de:4e:77:11:58:b6:90:26 username@remote\_host
The key's randomart image is:
+--[ RSA 2048]----+
|     ..o         |
|   E o= .        |
|    o. o         |
|        ..       |
|      ..S        |
|     o o.        |
|   =o.+.         |
|. =++..          |
|o=++.            |
+-----------------+
```

Ahora dispondrá de una clave pública y privada que puede usar para realizar la autenticación. El siguiente paso es ubicar la clave pública en su servidor a fin de poder usar la autenticación basada en claves de SSH para iniciar sesión.

## Paso 2: Copiar la clave pública al servidor de Ubuntu

La alternativa más rápida para copiar su clave pública al host de Ubuntu es usar una utilidad llamada <code>ssh-copy-id</code>. Debido a su simplicidad, este método se recomienda mucho si está disponible. Si no tiene la utilidad <code>ssh-copy-id</code> disponible en su máquina cliente, puede usar uno de los dos métodos alternativos proporcionados en esta sección (copiar mediante SSH con contraseña o copiar manualmente la clave).

### Copiar clave pública usando <code>ssh-copy-id</code>

La <code>ssh-copy-id</code> se incluye por defecto en muchos sistemas operativos. Por ello, es posible que tenga la posibilidad de disponer de ella en su sistema local. Para que este método funcione, ya debe disponer de acceso con SSH basado en contraseña en su servidor.

Para usar la utilidad, solo necesita especificar el host remoto al que desee conectarse y la cuenta de usuario a la que tenga acceso SSH con contraseña. Esta es la cuenta a la que se copiará su clave de SSH pública.

La sintaxis es la siguiente:

```
$ ssh-copy-id username@remote\_host
```

Es posible que vea el siguiente mensaje:

_Salida por pantalla_
```
The authenticity of host '203.0.113.1 (203.0.113.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes

```

Esto significa que su computadora local no reconoce el host remoto. Esto sucederá la primera vez que establezca conexión con un nuevo host. Escriba “yes” (sí) y presione <kbd>INTRO</kbd> para continuar.

A continuación, la utilidad analizará su cuenta local en busca de la clave <code>id\_rsa.pub</code> que creamos antes. Cuando la encuentre, le solicitará la contraseña de la cuenta del usuario remoto:

_Salida por pantalla_
```
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
username@203.0.113.1's password:
```

Escriba la contraseña (por motivos de seguridad, no se mostrará lo que escriba) y presione <kbd>INTRO</kbd>. La utilidad se conectará a la cuenta en el host remoto usando la contraseña que proporcionó. Luego, copie el contenido de su clave <code>~/.ssh/id\_rsa.pub</code> a un archivo en el directorio principal de la cuenta remota <code>~/.ssh</code> llamado <code>authorized_keys</code>.

Debería ver el siguiente resultado:

_Salida por pantalla_
```
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'username@203.0.113.1'"
and check to make sure that only the key(s) you wanted were added.
```

En este punto, su clave <code>id\_rsa.pub</code> se habrá cargado en la cuenta remota. |Puede continuar con el paso 3.

### Copiar la clave pública usando SSH

Si no tiene <code>ssh-copy-id</code> disponible, pero tiene acceso de SSH basado en contraseña a una cuenta de su servidor, puede cargar sus claves usando un método de SSH convencional.

Podemos hacer esto usando el comando <code>cat</code> para leer el contenido de la clave de SSH pública en nuestra computadora local y canalizando esto a través de una conexión SSH al servidor remoto.

Por otra parte, podemos asegurarnos de que el directorio <code>~/.ssh</code> exista y tenga los permisos correctos conforme a la cuenta que usamos.

Luego podemos transformar el contenido que canalizamos a un archivo llamado <code>authorized\_keys</code> dentro de este directorio. Usaremos el símbolo de redireccionamiento <code>>></code> para anexar el contenido en lugar de sobrescribirlo. Esto nos permitirá agregar claves sin eliminar claves previamente agregadas.

El comando completo tiene este aspecto:

```shell
cat ~/.ssh/id\_rsa.pub | ssh username@remote\_host "mkdir -p ~/.ssh && touch ~/.ssh/authorized\_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized\_keys"
```

Es posible que vea el siguiente mensaje:

_Salida por pantalla_
```
The authenticity of host '203.0.113.1 (203.0.113.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

Esto significa que su computadora local no reconoce el host remoto. Esto sucederá la primera vez que establezca conexión con un nuevo host. Escriba “yes” (sí) y presione <kbd>INTRO</kbd> para continuar.

Posteriormente, deberá recibir la solicitud de introducir la contraseña de la cuenta de usuario remota:

_Salida por pantalla_
```
username@203.0.113.1's password:
```

Una vez que ingrese su contraseña, el contenido de su clave <code>id\_rsa.pub</code> se copiará al final del archivo <code>authorized\_keys</code> de la cuenta del usuario remoto. Continúe con el paso 3 si el procedimiento se completó de forma correcta.

### Copiar la clave pública de forma manual

Si no tiene disponibilidad de acceso de SSH basado en contraseña a su servidor, deberá completar el proceso anterior de forma manual.

Habilitaremos el contenido de su archivo <code>id\_rsa.pub</code> para el archivo  <code>~/.ssh/authorized\_keys</code> en su máquina remota.

Para mostrar el contenido de su clave <code>id\_rsa.pub</code> , escriba esto en su computadora local:

```shell
$ cat ~/.ssh/id_rsa.pub
```

Verá el contenido de la clave, que debería tener un aspecto similar a este:

_Salida por pantalla_
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCqql6MzstZYh1TmWWv11q5O3pISj2ZFl9HgH1JLknLLx44+tXfJ7mIrKNxOOwxIxvcBF8PXSYvobFYEZjGIVCEAjrUzLiIxbyCoxVyle7Q+bqgZ8SeeM8wzytsY+dVGcBxF6N4JS+zVk5eMcV385gG3Y6ON3EG112n6d+SMXY0OEBIcO6x+PnUSGHrSgpBgX7Ks1r7xqFa7heJLLt2wWwkARptX7udSq05paBhcpB0pHtA1Rfz3K2B+ZVIpSDfki9UVKzT8JUmwW6NNzSgxUfQHGwnW7kj4jp4AT0VZk3ADw497M2G/12N0PPB5CnhHf7ovgy6nL1ikrygTKRFmNZISvAcywB9GVqNAVE+ZHDSCuURNsAInVzgYo9xgJDW8wUw2o8U77+xiFxgI5QSZX3Iq7YLMgeksaO4rBJEa54k8m5wEiEE1nUhLuJ0X/vh2xPff6SQ1BL/zkOhvJCACK6Vb15mDOeCSq54Cr7kvS46itMosi/uS66+PujOO+xt/2FWYepz6ZlN70bRly57Q06J+ZJoc9FfBCbCyYH7U/ASsmY095ywPsBo1XQ9PqhnN1/YOorJ068foQDNVpm146mUpILVxmq41Cj55YKHEazXGsdBIbXWhcrRf4G2fJLRcGUr9q8/lERo9oxRm5JFX6TCmj6kmiFqv+Ow9gI0x8GvaQ== demo@test
```

Acceda a su host remoto usando el método que esté a su disposición.

Una vez que tenga acceso a su cuenta en el servidor remoto, debe asegurarse de que exista el directorio <code>~/.ssh</code>. Con este comando se creará el directorio, si es necesario. Si este último ya existe, no se creará:

```shell
$ mkdir -p ~/.ssh
```

Ahora, podrá crear o modificar el archivo <code>authorized\_keys</code> dentro de este directorio. Puede agregar el contenido de su archivo <code>id\_rsa.pub</code> al final del archivo <code>authorized\_keys</code> y, si es necesario, crear este último con el siguiente comando:

```shell
$ echo public\_key\_string >> ~/.ssh/authorized\_keys
```

En el comando anterior, reemplace <code>public\_key\_string</code> por el resultado del comando <code>cat ~/.ssh/id_rsa.pub</code> que ejecutó en su sistema local. Debería iniciar con <code>ssh-rsa AAAA... </code>.

Por último, verificaremos que el directorio <code>~/.ssh</code> y el archivo <code>authorized\_keys</code> tengan el conjunto de permisos apropiados:

```shell
$ chmod -R go= ~/.ssh
```

Con esto, se eliminan de forma recursiva todos los permisos “grupo” y “otros” del directorio <code>~/.ssh/</code>.

Si está usando la cuenta <code>root</code> para configurar claves para una cuenta de usuario, también es importante que el directorio <code>~/.ssh/</code> pertenezca al usuario y no sea <code>root</code>:

```shell
$ chown -R sammy:sammy ~/.ssh
```

En este tutorial, nuestro usuario recibe el nombre <mark>sammy</mark> pero debe sustituir el nombre de usuario que corresponda en el comando anterior.

Ahora podemos intentar la autenticación sin contraseña con nuestro servidor de Ubuntu.

## Step 3 — Authenticate to Ubuntu Server Using SSH Keys

If you have successfully completed one of the procedures above, you should be able to log into the remote host _without_ the remote account’s password.

The basic process is the same:

```shell
$ ssh username@remote\_host
```

If this is your first time connecting to this host (if you used the last method above), you may see something like this:

_Salida por pantalla_
```
The authenticity of host '203.0.113.1 (203.0.113.1)' can't be established.
ECDSA key fingerprint is fd:fd:d4:f9:77:fe:73:84:e1:55:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)? yes
```

This means that your local computer does not recognize the remote host. Type “yes” and press <kbd>INTRO</kbd> to continue.

If you did not supply a passphrase for your private key, you will be logged in immediately. If you supplied a passphrase for the private key when you created the key, you will be prompted to enter it now (note that your keystrokes will not display in the terminal session for security). After authenticating, a new shell session should open for you with the configured account on the Ubuntu server.

If key-based authentication was successful, continue on to learn how to further secure your system by disabling password authentication.

## Step 4 — Disable Password Authentication on your Server

If you were able to log into your account using SSH without a password, you have successfully configured SSH-key-based authentication to your account. However, your password-based authentication mechanism is still active, meaning that your server is still exposed to brute-force attacks.

Before completing the steps in this section, make sure that you either have SSH-key-based authentication configured for the root account on this server, or preferably, that you have SSH-key-based authentication configured for a non-root account on this server with sudo privileges. This step will lock down password-based logins, so ensuring that you will still be able to get administrative access is crucial.

Once you’ve confirmed that your remote account has administrative privileges, log into your remote server with SSH keys, either as root or with an account with sudo privileges. Then, open up the SSH daemon’s configuration file:

```shell
$ sudo nano /etc/ssh/sshd\_config

```

Inside the file, search for a directive called <code>PasswordAuthentication</code>. This may be commented out. Uncomment the line and set the value to “no”. This will disable your ability to log in via SSH using account passwords:

_(file)_ <code>/etc/ssh/sshd\_config</code>
```
...
PasswordAuthentication no
...
```

Save and close the file when you are finished by pressing <kbd>CTRL</kbd> + <kbd>X</kbd>, then <kbd>Y</kbd> to confirm saving the file, and finally <kbd>INTRO</kbd> to exit nano. To actually implement these changes, we need to restart the sshd service:

```shell
$ sudo systemctl restart ssh
```

As a precaution, open up a new terminal window and test that the SSH service is functioning correctly before closing this session:

```shell
$ ssh username@remote\_host
```

Once you have verified your SSH service, you can safely close all current server sessions.

The SSH daemon on your Ubuntu server now only responds to SSH keys. Password-based authentication has successfully been disabled.

## Conclusion

You should now have SSH-key-based authentication configured on your server, allowing you to sign in without providing an account password.

If you’d like to learn more about working with SSH, take a look at our [SSH Essentials Guide](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).

Written by [Hanif Jetha](https://www.digitalocean.com/community/users/hjet).

Editor: [Lisa Tagliaferry](https://www.digitalocean.com/community/users/ltagliaferri).

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/).


