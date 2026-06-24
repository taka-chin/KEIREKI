FROM nginx:alpine

# カスタム nginx 設定をコピー
COPY nginx.conf /etc/nginx/conf.d/default.conf

# アプリをコピー
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
