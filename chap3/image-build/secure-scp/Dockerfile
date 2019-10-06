# ファイルをコピーするための一時的なステージ(temp-env)
FROM alpine:latest AS temp-env
RUN apk update
RUN apk add --no-cache openssh

COPY sshkey.pem /root/.ssh/id_rsa
RUN scp -r -oStrictHostKeyChecking=false ubuntu@172.31.18.112:/share/www www

# メインのステージ
FROM library/nginx:1.15.8

# temp-envステージで取得したファイルをコピー
COPY --from=temp-env www/* /usr/share/nginx/html/

EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["nginx", "-g", "daemon off;"]
