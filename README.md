# DMV Accounts — Deploy en Vercel

## Despliegue en Vercel (5 minutos)

### Opción A — Sin GitHub (más rápido)

1. Instala Vercel CLI:
```bash
npm install -g vercel
```

2. Entra a la carpeta del proyecto:
```bash
cd dmv-accounts
```

3. Despliega:
```bash
vercel
```
Sigue las instrucciones en pantalla. En la primera vez te pedirá iniciar sesión.

4. Configura las variables de entorno en el dashboard de Vercel:
   - Ve a tu proyecto → Settings → Environment Variables
   - Agrega estas 3 variables:

| Variable           | Valor                                    |
|--------------------|------------------------------------------|
| GHL_API_KEY        | pit-d623abb3-46d9-4d85-930a-12f5316642e3 |
| GHL_LOCATION_ID    | KmMG8sP5pJBBIheg3xDw                     |
| GHL_PIPELINE_ID    | cjKzhddcTvUIrZrJBo83                     |

5. Vuelve a desplegar para que tome las variables:
```bash
vercel --prod
```

---

### Opción B — Con GitHub (recomendado para producción)

1. Sube el proyecto a un repositorio de GitHub
2. Ve a https://vercel.com → New Project → Import desde GitHub
3. Selecciona el repo → Add Environment Variables (las 3 de arriba)
4. Deploy → listo. Cada push a `main` despliega automáticamente.

---

## Prueba local antes de subir

```bash
npm install
npm run dev
# Abre http://localhost:3000
```

El archivo `.env.local` ya tiene las credenciales para desarrollo local.

---

## Credenciales de acceso a la app

| Usuario  | Contraseña  | Rol            |
|----------|-------------|----------------|
| admin    | admin123    | Administrador  |
| agente1  | agente123   | Agente         |

---

## Estructura del proyecto

```
dmv-accounts/
├── pages/
│   ├── _app.js          ← Configuración global Next.js
│   ├── index.js         ← App completa (React)
│   └── api/
│       ├── contacts.js  ← Proxy → GHL /contacts/search
│       └── dmv-records.js ← Proxy → GHL /objects/dmv_accounts/records
├── styles/
│   └── globals.css
├── .env.local           ← Variables para desarrollo local
├── package.json
└── README.md
```

## Nota sobre Custom Objects en GHL

Si los trámites DMV no cargan (error 404 en `/api/dmv-records`), verifica en GHL:
Settings → Custom Objects → DMV Accounts → asegúrate que el Status sea **Active/Published**.
