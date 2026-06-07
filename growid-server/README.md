# Growid Landing – Mailer Server

## מבנה הקבצים
```
growid-landing.html
growid-assets/
growid-server/
  server.js
  package.json
  node_modules/
```

## הרצה מקומית
```bash
cd growid-server
node server.js
```
השרת רץ על http://localhost:3000
פתח את הדף הנחיתה דרך http://localhost:3000/growid-landing.html

## Deploy על שרת לינוקס (Ubuntu/Debian)

### 1. העלה את כל הקבצים לשרת
```bash
scp -r growid-landing.html growid-assets growid-server user@yourserver:/var/www/growid/
```

### 2. התקן Node.js על השרת
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

### 3. התקן dependencies
```bash
cd /var/www/growid/growid-server
npm install
```

### 4. הרץ עם PM2 (כדי שרץ תמיד)
```bash
npm install -g pm2
pm2 start server.js --name growid-mailer
pm2 save
pm2 startup
```

### 5. Nginx reverse proxy (אופציונלי)
```nginx
location /send {
    proxy_pass http://localhost:3000/send;
}
```
