# 👨🏫 Introducción a HTB

El famoso servicio [Hack The Box](https://www.hackthebox.com/) es fundamental para comenzar a formarte en ciberseguridad dbeido a la cantidad de formación que te ofrece y que, pese a ser un servicio de pago, tiene algunos apartados gratuitos o que te permiten introducirte en la ciberseguridad de manera sencilla. Por ello voy a desgranaros algunos puntos relevantes aqui para los que llegueís de nuevas a la plataforma.&#x20;

1. **Academia**

Si estás visitando este punto para conocer ¿Que es HTB? probablemente sea un apartado que te interese. La [academia de HTB](https://academy.hackthebox.com/) es un espacio con multitud de cursos y tutoriales sencillos mediante los cuales puedes adquirir Skills de hacking a diferentes niveles y de diferentes metodologías. Es un servicio de pago pero que puede ser util con la gamificación que caracteriza a la plataforma la cual otorga puntos y la capacidad de hacer otros cursos según lo vas desbloqueando. Tenemos desde tutoriales muy complejos al uso más sencillo de una bash. Cuando comienzas te dan algunos puntos para que pruebes algun curso y más tarde puedes comprar algunos puntos más para acceder al resto. Además en la academia tendrás espacio para obtener algunas certificaciones de HTB, aunque por el momento son de un nivel bastante avanzado.&#x20;

<figure><img src="../../.gitbook/assets/1 (12).png" alt=""><figcaption></figcaption></figure>

2. **Máquinas y retos**&#x20;

Las [máquinas y retos](https://app.hackthebox.com/login), como muchas que podrás ver en este espacio que he creado, son simulaciones de entornos o problemas del mundo real diseñados para vulnerarse de una determinada manera y así entrenar tus skills de pentesting. Hay de muchos niveles y suelen explotar todas vulnerabilidades diferntes, o hacerlo cada una de una manera especial. Una vez sepas manejarte con una bash y tras aprender algunas cosas como enumeración o algunas bases de programación puede ser un buen momento para empezar a hacer máquinas sencillas mientras que te guias con un write-up coo los de este espacio o con un video.&#x20;

<figure><img src="../../.gitbook/assets/3 (12).png" alt=""><figcaption></figcaption></figure>

3. **TJNULL fichero**

Como en todo, siempre hay gente que sabe más que uno. En este caso indiscutiblemente [TJNULL](https://github.com/tjnull), un experto en ciberseguridad, sabe más que yo y ha hecho un [fichero ](https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview)exponiendo cuales son las máquinas recomendadas para sacarse la[ certificación OSCP](https://www.offsec.com/courses/pen-200/?utm\_campaign=Google-Ads\_Brand\_PPC\_PWK\_2020\_Update\_EUR\&utm\_medium=cpc\&utm\_source=google\&utm\_content=crid=649700848527\&utm\_term=kwd=oscp:cid-9267886936:kwd-304102459:dev-c:mt-b\&gclid=EAIaIQobChMIuIrk1JL5\_QIVmbfVCh0Lzw7HEAAYASAAEgIAR\_D\_BwE), una de las más respetadas del sector. Aunque no hay que apresurarse y tenemos que saber cual es nuestro nivel real siempre está bien pasarse por este listado y probar a resolver algunas de las máquinas expuestas para ver como vamos mejorando. Podeís encontrar varias versiones de este fichero más o menos actualizadas por internet.&#x20;

{% embed url="https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview" %}

4. **¿Como inicio una máquina desde mi PC y me conecto por primera vez?**

Para iniciar una máquina y conectarnos mediante la VPN debemos de pulsar en el apartado rojo oque se encuentra a la derecha y pulsar en machines.&#x20;

<figure><img src="../../.gitbook/assets/2 (13).png" alt=""><figcaption></figcaption></figure>

Al pulsar en Machines veremos la siguiente imagen y puslsaremos "openvpn"&#x20;

<figure><img src="../../.gitbook/assets/3 (11).png" alt=""><figcaption></figcaption></figure>

En este punto seleccionamos un servidor público so VIP desde le cual nos queramos conectar y el servidor en concreto y nos descargamos el archivo de la VPN.&#x20;

<figure><img src="../../.gitbook/assets/11 (4).png" alt=""><figcaption></figcaption></figure>

Para iniciarnos en la VPN solo deberemos de tener descargado "openvpn" en nuestra máquina y ejecutar el fichero descargado.

```bash
openvpn ../[TU-VPN].ovp
```

En este punto ya estarás dentro de la red de HTB y en el margen superior derecho verás que HTB nos avisa que estamos conectados a la VPN y a cual.&#x20;

<figure><img src="../../.gitbook/assets/12 (5).png" alt=""><figcaption></figcaption></figure>

5. **¿Como inicio una PWNBOX de pago por primera vez?**

En algunos momentos sin pagar una subscripción VIP tendremos acceso a [Starting Points de HTB](https://help.hackthebox.com/en/articles/5185687-introduction-to-lab-access), como en la academia. Se inician de una manera sencilla y nos permiten tener virtualizado un SO Parrot con las que poder realizar las máquinas. Además puede ayudarte si no tienes un equipo de trabajo muy potente o en el que te sea sencillo virtualizar. Al pulsar en el espacio "Connect to HTB" arriba a la derecha podemos ver el siguiente desplegable en el cual deberemos de pulsar "Starting Point".

<figure><img src="../../.gitbook/assets/1 (10).png" alt=""><figcaption></figcaption></figure>

En este punto pulsamos "Pwnbox".

<figure><img src="../../.gitbook/assets/2 (10).png" alt=""><figcaption></figcaption></figure>

Aqui nos aparecerán las diferentes pciones para desplegar la máquina, en la cual deberemos de seleccionar una localización con poco ping y podremos seleccionar el acceso de VPN y el servidor de la VPN, en nuestro caso al pagar la subscripción sería el VIP.  En este punto debemos de pulsar "start pwnbox" y comenzará a cargar nuestra pwnbox.

<figure><img src="../../.gitbook/assets/5 (11).png" alt=""><figcaption></figcaption></figure>

Ya solo debemos de pulsar "Open Desktop" para ver la instancia desplegado.&#x20;

<figure><img src="../../.gitbook/assets/1 (11).png" alt=""><figcaption></figcaption></figure>

Con esto nos aparecerá ya la máquina y podremos trabajar y hacer los retos y máquinas que queramos desde aqui.&#x20;

<figure><img src="../../.gitbook/assets/1 (14).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
Recuerda finalizar la máquina una vez termines de trabajar con ella ya que tendrás un tiempo disponible dependiendo de tu subscripción y si lo gastas tendrás que pagar una subscripción superior.&#x20;
{% endhint %}
