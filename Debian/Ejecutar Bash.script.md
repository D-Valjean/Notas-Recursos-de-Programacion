bash script execute command runserver django on debian

To execute the Django runserver command using a bash script on a Debian system, follow these steps:

1. Create a new file with a `.sh` extension, e.g., `run_django_server.sh`.
2. Open the file in a text editor and add the following content:

```
#!/bin/bash

# Navigate to the project directory
cd /path/to/your/django/project

# Activate the virtual environment (if applicable)
source /path/to/your/venv/bin/activate

# Run the Django development server
python manage.py runserver 0.0.0.0:8000
```

Replace `/path/to/your/django/project` with the actual path to your Django project directory. If you are using a virtual environment, replace `/path/to/your/venv` with the actual path to your virtual environment.

3. Save and close the file.
4. Make the script executable by running the following command in the terminal:

```
chmod +x run_django_server.sh
```

5. Now you can run the Django development server using the bash script by executing the following command in the terminal:

```
./run_django_server.sh
```

This will start the Django development server on port 8000, allowing you to access your application at `http://127.0.0.1:8000`.

For automating the process of opening the project in a web browser, you can modify the script as follows:

```
#!/bin/bash

# Navigate to the project directory
cd /path/to/your/django/project

# Activate the virtual environment (if applicable)
source /path/to/your/venv/bin/activate

# Run the Django development server
python manage.py runserver 0.0.0.0:8000 &

# Wait for 3 seconds to allow the server to start
sleep 3

# Open the project in the default web browser
xdg-open http://127.0.0.1:8000
```

This modified script will open the project in your default web browser after starting the Django development server. Note that this solution might not work on all systems, as the `xdg-open` command is specific to certain desktop environments.