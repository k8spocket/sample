# Goアプリのビルド環境のステージ(builder)
From ubuntu:18.04 as builder
RUN apt-get update 
RUN apt-get install -y golang-go=2:1.10~4ubuntu1
ADD main.go /
WORKDIR /
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo main.go

# 最終的にイメージに含まれるステージ
From scratch as image 
EXPOSE 80
# ステージからビルドされたバイナリだけをコピー
COPY --from=builder /main /web builder
ENTRYPOINT ["/web"]

