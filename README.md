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

<h1>Implementación de Firestore</h1>

Comunicación con la base de datos

Crear proyecto en GCP e iniciar una BD en firestore.
instalar el SDK de gcloud
hacer login desde la terminal: gcloud auth login
hacer login application-default: gcloud auth application-default login
inicializar: gcloud init
seguir las instrucciones y elegir el proyecto que creamos en GCP.
ambiente de gcloud configurado y conectado a nuestra aplicación.

Para los que tengan el error al ejecutar por la conexión a firestore queda con añadir la variable al entorno

Unix Bash:
export GOOGLE_CLOUD_PROJECT=‘EL_ID_DE_TU_PROEYCTO’

Win CMD:
set GOOGLE_CLOUD_PROJECT=‘EL_ID_DE_TU_PROEYCTO’

Powershell:
$env:GOOGLE_CLOUD_PROJECT=‘EL_ID_DE_TU_PROEYCTO’

Para ver el proyecto en ejecución

gcloud config list

Para configurar el proyecto

gcloud  config set project "id del proyecto"

<h1>Autenticación de usuarios: Login</h1>

https://flask-login.readthedocs.io/en/latest/
https://drive.google.com/drive/folders/1ICKi5POR7ZAvhlY05j35OrNbjYfQvAQ3?usp=sharing

<h1>Autenticación de usuarios: Logout</h1>

<h1>Signup</h1>

app\view.py

aqui un poco mas de informacion acerca de Werkzeug.security:

Python werkzeug.security.generate_password_hash()

Si después de hashear el pwd ya no pueden entrar con su usuario, tienen que usar un check_password_hash en el metodo del login

@auth.route('/login', methods=['GET', 'POST'])
def login():
    login_form = LoginForm()
    context = {
        'login_form': LoginForm()
    }

    if login_form.validate_on_submit():
        username = login_form.username.data
        password = login_form.password.data
        user_doc = get_user(username)

        if user_doc.to_dict() is not None:
            
            if check_password_hash(user_doc.to_dict()['password'], password):
                user_data = UserData(username,password)
                user = UserModel(user_data)

                login_user(user)
                flash('Well come again')
                redirect(url_for('hello'))
            else:
                flash('wrong password >:(')
        else:
            flash('user does not exist =/')
        return redirect(url_for('index'))
    
    return render_template('login.html', **context)
    

<h1>Agregar tareas</h1>

![image](https://user-images.githubusercontent.com/94714288/144225853-7e004653-f86e-4e59-9dd6-0fcc35271ce0.png)

<h1>Eliminar tareas</h1>

main.py, macros.html, hello.html, firestore_services.py

Si cambian el macros.html por:

{% import 'bootstrap/wtf.html' as wtf %}

{% macro render_todo(todo, delete_form) %}
    <li class="list-group-item">
        <span class="badge">
            {%if todo.to_dict().done %}
                Done
            {% else %}
                To do
            {% endif %}
        </span>
        Descripción: {{ todo.to_dict().description }}

        {{ wtf.quick_form(delete_form, action=url_for('delete', todo_id=todo.id)) }}
    </li>
{% endmacro %}
En vez de False ó True les mostrará To do ó Done

![image](https://user-images.githubusercontent.com/94714288/144231295-ccf694db-d260-4f8e-8598-7a79212e3308.png)

<h1>Editar tareas</h1>

Si en macros.html a cada form del estilo botón le agregan la clase botón se va a ver mejor.

Ejemplo:

<button type="button" class="btn btn-light">
            {{ wtf.quick_form(delete_form, action=url_for('delete', todo_id=todo.id)) }}
        </button>
        <button type="button" class="btn btn-light">
        {{ wtf.quick_form(update_form, action=url_for('update', todo_id=todo.id, done=todo.to_dict().done)) }}
        </button>
![image](https://user-images.githubusercontent.com/94714288/144599649-09f7efda-3939-427a-a24f-e79b236c6aed.png)

<h1>Deploy a producción con App Engine</h1>

https://console.cloud.google.com/appengine
https://platzi.com/clases/fundamentos-google/

1.Crear archivo app.yaml —> runtime: python37
2.Crear nuevo proyecto en gcloud para producción
3.Cambiar el proyecto actual de gcloud : gcloud init
4.Ejecutar el comando: gcloud app deploy app.yaml
5.Activar firestore en gcloud
6.Ejecutar el comando: gcloud app browse
7. Ingresar a la ruta generada por gcloud y probar la app.

ERROR: (gcloud.app.deploy) Error Response: [7] Access Not Configured. Cloud Build has not been used in project platzi-flask-333714 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/cloudbuild.googleapis.com/overview?project=platzi-flask-333714 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.

Deploy on Heroku: https://dev.to/techparida/how-to-deploy-a-flask-app-on-heroku-heb
