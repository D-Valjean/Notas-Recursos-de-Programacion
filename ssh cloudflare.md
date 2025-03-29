

# Instalar s3fs
	sudo apt install s3fs

# Montar bucket:
	echo "CLOUDFLARE_ACCESS_KEY:CLOUDFLARE_SECRET_KEY" > ~/.passwd-s3fs
	chmod 600 ~/.passwd-s3fs
	s3fs nombre-bucket /mnt/r2 -o url=https://[ACCOUNT_ID].r2.cloudflarestorage.com -o use_path_request_style

# Operar como si fuera SSH:
	cd /mnt/r2 && grep -rl "patron" . | xargs rm




### 1. Crear archivo de credenciales

	Ejecuta este comando (usando tus claves reales):
	
	echo "tu_access_key:tu_secret_key" > ~/.passwd-s3fs
	
	En tu caso específico (sustituyendo con tus credenciales):
	
	echo "CLOUDFLARE_ACCESS_KEY:CLOUDFLARE_SECRET_KEY" > ~/.passwd-s3fs

### 2. Asegurar permisos del archivo
	
	chmod 600 ~/.passwd-s3fs
	
### 3. Montar el bucket R2

	bash
	
	Copy
	
	s3fs tu-nombre-bucket /mnt/r2 \
	-o url=https://[TU_ACCOUNT_ID].r2.cloudflarestorage.com \
	-o use_path_request_style \
	-o allow_other

### Verificación de funcionamiento:


# Listar archivos
ls -la /mnt/r2

# Ver uso de espacio
	df -h /mnt/r2

### Si falla la conexión, verifica:

1. **Credenciales válidas** en Cloudflare Dashboard > R2 > Manage R2 API Tokens
    
2. **Permisos del bucket**: La política debe permitir `s3:ListBucket` y `s3:GetObject`
    
3. **Endpoint correcto**: Debe seguir el formato `https://[ACCOUNT_ID].r2.cloudflarestorage.com`
    

### Comandos útiles para diagnóstico:


# Ver logs en tiempo real
tail -f /var/log/syslog | grep s3fs

# Probando con AWS CLI
	AWS_ACCESS_KEY_ID="{AWS_ACCESS_KEY_ID}" \
	AWS_SECRET_ACCESS_KEY="{AWS_SECRET_ACCESS_KEY}" \
	aws s3 ls s3://tu-bucket --endpoint https://[ACCOUNT_ID].r2.cloudflarestorage.com

⚠️ **Importante**: Nunca compartas tus claves de acceso. Si las has expuesto públicamente, revócalas inmediatamente en el panel de Cloudflare y genera nuevas.

### **Solución Probada:**

1. **Verificar formato del archivo de credenciales:**
    
    
    cat ~/.passwd-s3fs
    
    - Debe mostrar **solo una línea** con el formato:
      
        
        ACCESS_KEY:SECRET_KEY
        
    - Ejemplo válido:
        
        text
        
        Copy
        
        ACCESS_KEY:SECRET_KEY
        
2. **Asegurar permisos correctos:**
  
    
    chmod 600 ~/.passwd-s3fs
    
3. **Comando de montaje completo:**
    
    
    s3fs tu-bucket-r2 /mnt/r2 \
    -o passwd_file=~/.passwd-s3fs \
    -o url=https://[TU_ACCOUNT_ID].r2.cloudflarestorage.com \
    -o use_path_request_style \
    -o allow_other \
    -o umask=022 \
    -o dbglevel=info -f -o curldbg
    
    - **Reemplaza:**
        
        - `tu-bucket-r2`: Nombre de tu bucket en R2
            
        - `[TU_ACCOUNT_ID]`: ID de tu cuenta Cloudflare (visible en el dashboard)
            

---

### **Pasos Adicionales si Persiste el Error:**

#### a) **Forzar el uso del archivo de credenciales:**

bash

Copy

s3fs tu-bucket-r2 /mnt/r2 -o passwd_file=~/.passwd-s3fs \
-o url=https://[ACCOUNT_ID].r2.cloudflarestorage.com \
-o sigv4

#### b) **Verificar conexión con AWS CLI:**

bash

Copy

AWS_ACCESS_KEY_ID="{AWS_ACCESS_KEY_ID}" \
AWS_SECRET_ACCESS_KEY="{AWS_SECRET_ACCESS_KEY}" \
aws s3 ls s3://tu-bucket-r2 --endpoint https://[ACCOUNT_ID].r2.cloudflarestorage.com

- Si esto falla, tus credenciales son inválidas o el bucket no existe.
    

#### c) **Eliminar variables de entorno conflictivas:**


unset AWS_ACCESS_KEY_ID
unset AWS_SECRET_ACCESS_KEY

---

### **Casos Específicos de Cloudflare R2:**

1. **Agregar parámetros de firma V4:**
    
    bash
    
    Copy
    
    -o sigv4 \
    -o endpoint=auto \
    
2. **Ejemplo completo funcionando:**
    
    bash
    
    Copy
    
    s3fs mi-bucket /mnt/r2 \
    -o passwd_file=~/.passwd-s3fs \
    -o url=https://abc123.r2.cloudflarestorage.com \
    -o use_path_request_style \
    -o sigv4 \
    -o allow_other \
    -o umask=022 \
    -o kernel_cache
    

---

### **Diagnóstico Avanzado:**

1. **Habilitar logs detallados:**
    
    bash
    
    Copy
    
    s3fs tu-bucket /mnt/r2 -o dbglevel=debug -f -o curldbg 2>&1 | tee /tmp/s3fs.log
    
2. **Errores comunes en logs:**
    
    - `403 Forbidden`: Credenciales inválidas o permisos insuficientes.
        
    - `NoSuchBucket`: Nombre del bucket incorrecto.
        
    - `SSL errors`: Problemas con el certificado del endpoint.
        

---

### **Importante:**

- **Regenera tus claves R2** si las has expuesto públicamente (Cloudflare Dashboard → R2 → Manage API Tokens).
    
- Usa **/mnt/r2** como punto de montaje vacío (no debe contener archivos antes de montar).
