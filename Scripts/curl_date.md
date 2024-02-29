dateFromServer=$(curl -v --insecure --silent https://google.com/ 2>&1 \
       | grep Date | sed -e 's/< Date: //'); date +"%d-%m-%Y|%H-%M-%S" -d "$dateFromServer"
