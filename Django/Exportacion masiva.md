Para exportar datos utilizando django-admin, puedes utilizar el comando dumpdata. Este comando te permite generar un archivo JSON que contiene los datos de las tablas de tu base de datos. Aquí tienes un ejemplo de cómo usarlo:

	python manage.py dumpdata --output datos.json

En este ejemplo, datos.json es el nombre del archivo de salida donde se guardarán los datos exportados. Puedes especificar el nombre que desees para el archivo de salida.

También puedes limitar el ámbito de los datos exportados especificando nombres de modelos o aplicaciones específicas.


Para importar los datos del archivo JSON a la nueva base de datos en Django, puedes utilizar el comando loaddata. Aquí tienes un ejemplo de cómo hacerlo:

	python manage.py loaddata datos.json



## Si se presenta error al migrar
in your local database you create some ContentType instances.

when you migrate your remote database all ContentType for your models created again.

but when you want to load data you try to load this instances again.

you have 2 solutions

1- remove all content types instances from remote host using django shell:

```python
python manage.py shell

>>> from django.contrib.contenttypes.models import ContentType
>>> ContentType.objects.all().delete()
```
2- remove content type instances from dumped data

```python
python manage.py dumpdata --exclude contenttypes
```