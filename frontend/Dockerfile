FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY dist/browser/ /usr/share/nginx/html/

RUN printf "server { \n\
    listen 80; \n\
\n\
    location / { \n\
        root /usr/share/nginx/html; \n\
        index index.html; \n\
        try_files \$uri \$uri/ /index.html; \n\
    } \n\
\n\
    location /api/ { \n\
        proxy_pass http://moneywise-backend:8080/api/; \n\
        proxy_set_header Host \$host; \n\
        proxy_set_header X-Real-IP \$remote_addr; \n\
    } \n\
}" > /etc/nginx/conf.d/default.conf

EXPOSE 80
