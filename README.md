# To-Do-List-App
Built with Flask
<h1>App Factory</h1>

Estructurar un proyecto en Flask:

https://pythonise.com/series/learning-flask/flask-application-structure
https://dev.to/aligoren/how-i-structure-my-flask-apps-3eh8
https://flask.palletsprojects.com/en/1.1.x/tutorial/layout/
https://flask.palletsprojects.com/en/1.1.x/tutorial/factory/

<h1>Blueprints</h1>

Modularizar vistas con autorización

https://pypi.org/project/blinker/
https://www.youtube.com/watch?v=3Yz6QanCSaA


<h1>Base de datos y App Engine con Flask</h1>

Bases de Datos SQL: su composición esta hecha con bases de datos llenas de tablas con filas que contienen campos estructurados. No es muy flexible pero es el más usado. Una de sus desventajas es que mientras más compleja sea la base de datos más procesamiento necesitará.

Base de Datos NOSQL: su composición es no estructurada, es abierta y muy flexible a diferentes tipos de datos, no necesita tantos recursos para ejecutarse, no necesitan una tabla fija como las que se encuentran en bases de datos relacionales y es altamente escalable a un bajo costo de hardware.

![image](https://user-images.githubusercontent.com/94714288/144048723-b95c3660-26c6-4112-8844-6f17900df9aa.png)

Flask no tiene un ORM por defecto.
Podemos implementar la lógica para usar la BD que queramos
Podemos extender un ORM SQL: https://flask-sqlalchemy.palletsprojects.com/en/2.x/
Usaremos Firestore: NoSQL - Grupo de colecciones - documentos->row, field->Column, document ID-> primary key

Tutorial flask-SQLAchemy: https://platzi.com/tutoriales/1540-flask/7112-conectando-aplicacion-con-base-de-datos-relacional/

<h1>Configuración de Google Cloud SDK</h1>

Ahora vamos a instalar el Google Cloud SDK. Simplemente debemos descargar un ejecutable desde alguno de estos enlaces:

 - Para Windows dirígete a https://cloud.google.com/sdk/docs/quickstart-windows
 - Para MacOS dirígete a link https://cloud.google.com/sdk/docs/quickstart-macos
 - Para Linux dirígete a https://cloud.google.com/sdk/docs/quickstart-linux

Una vez que corrimos el instalador, podemos verificar que instalamos correctamente el SDK corriendo en una terminal el siguiente comando:

which gcloud
Ahora inicializamos gcloud y hacemos login con:

gcloud init
gcloud auth login
