1. Crear un script de inicio
Crea un script que ejecute tu servidor Django (ej. /opt/start_django.sh):

bash
#!/bin/bash
cd /ruta/a/tu/proyecto_django  # Cambia a la ruta de tu proyecto
source venv/bin/activate  # Si usas entorno virtual (opcional)
python manage.py runserver 0.0.0.0:8000  # Ajusta puerto según necesites
Hazlo ejecutable:

bash
chmod +x /opt/start_django.sh
2. Configurar systemd (recomendado)
Crea un servicio systemd en /etc/systemd/system/django.service:

ini
[Unit]
Description=Servicio Django
After=network.target

[Service]
Type=simple
User=tu_usuario  # Reemplaza con tu usuario
WorkingDirectory=/ruta/a/tu/proyecto_django
ExecStart=/opt/start_django.sh
Restart=on-failure

[Install]
WantedBy=multi-user.target
Habilita el servicio:

bash
sudo systemctl daemon-reload
sudo systemctl enable django.service
sudo systemctl start django.service
sudo systemctl status django.service


# Detener el servicio inmediatamente
sudo systemctl stop django.service

# Desactivar el inicio automático (pero no detiene el servicio actual)
sudo systemctl disable django.service

# Verificar el estado
sudo systemctl status django.service

###############################
Detener manualmente el proceso en ejecución
bash
# Encontrar el proceso de Django
ps aux | grep runserver

# Matar el proceso específico (reemplaza PID con el número real)
kill -9 PID

# O matar todos los procesos de runserver
pkill -f runserver
5. Para reactivar más tarde
Cuando quieras volver a activar el inicio automático:

bash
# Para systemd
sudo systemctl enable django.service
sudo systemctl start django.service

# Para cron
sudo crontab -e  # Y descomentar la línea
Consejo adicional: Crear scripts de control
Puedes crear scripts simples para facilitar el manejo:

bash
# Crear script para detener
echo 'sudo systemctl stop django.service' > /usr/local/bin/django-stop
chmod +x /usr/local/bin/django-stop

# Crear script para iniciar
echo 'sudo systemctl start django.service' > /usr/local/bin/django-start
chmod +x /usr/local/bin/django-start
Ahora podrás usar simplemente:

bash
sudo django-stop  # Para detener
sudo django-start  # Para iniciar