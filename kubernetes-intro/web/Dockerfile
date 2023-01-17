FROM nginx

RUN useradd -r -u 1001 app

WORKDIR /app/
COPY ./app .
COPY ./homework.conf /etc/nginx/conf.d/homework.conf

RUN touch /var/run/nginx.pid && chown -R app:app /var/run/nginx.pid && chown -R app:app /app && chown -R app:app /var/cache/nginx

EXPOSE 8000
USER app

ENTRYPOINT ["nginx", "-g", "daemon off;"]
