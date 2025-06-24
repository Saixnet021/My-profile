# Configuración de EmailJS para el Formulario de Contacto

Para hacer funcional el formulario de contacto, necesitas configurar EmailJS. Sigue estos pasos:

## 1. Crear cuenta en EmailJS

1. Ve a [https://www.emailjs.com/](https://www.emailjs.com/)
2. Crea una cuenta gratuita
3. Verifica tu email

## 2. Configurar el servicio de email

1. En el dashboard de EmailJS, ve a "Email Services"
2. Haz clic en "Add New Service"
3. Selecciona tu proveedor de email (Gmail, Outlook, etc.)
4. Sigue las instrucciones para conectar tu cuenta
5. Anota el **Service ID** (ejemplo: `service_portfolio`)

## 3. Crear template de email

1. Ve a "Email Templates"
2. Haz clic en "Create New Template"
3. Usa este contenido para el template:

**Subject:** Nuevo mensaje de contacto -  {{subject}}

**Content:**
```
Has recibido un nuevo mensaje de contacto desde tu portfolio:

Nombre: {{from_name}}
Email: {{from_email}}
Asunto: {{subject}}

Mensaje:
{{message}}

---
Este mensaje fue enviado desde tu portfolio web.
```

4. Anota el **Template ID** (ejemplo: `template_contact`)

## 4. Obtener Public Key

1. Ve a "Account" > "General"
2. Copia tu **Public Key**

## 5. Actualizar el código

Reemplaza los siguientes valores en los archivos:

### En `src/layouts/Layout.astro`:
```javascript
emailjs.init("YOUR_PUBLIC_KEY"); // Reemplazar con tu Public Key real
```

### En `public/contact-form.js`:
```javascript
const response = await emailjs.send(
    'service_portfolio', // Reemplazar con tu Service ID real
    'template_contact', // Reemplazar con tu Template ID real
    {
        from_name: data.name,
        from_email: data.email,
        subject: data.subject,
        message: data.message,
        to_email: 'fernandezanderson562@gmail.com'
    },
    'YOUR_PUBLIC_KEY' // Reemplazar con tu Public Key real
);
```

## 6. Probar el formulario

1. Ejecuta tu proyecto: `npm run dev`
2. Ve a la sección de contacto
3. Llena el formulario y envía un mensaje de prueba
4. Verifica que recibas el email

## Límites del plan gratuito

- 200 emails por mes
- Perfecto para un portfolio personal

## Alternativas

Si prefieres otra solución, puedes usar:
- Formspree
- Netlify Forms
- Getform
- Tu propio backend con nodemailer

¡El formulario estará completamente funcional una vez que completes estos pasos!
