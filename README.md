# docker-alpine-ftp-server

Small and flexible docker image with vsftpd server

## Configuration

Environment variables:
- `USERS` - space and `|` separated list (optional, default: `alpineftp|alpineftp`)
  - format `name1|password1|[folder1][|uid1][|gid1] name2|password2|[folder2][|uid2][|gid2]`
- `ADDRESS` - external address witch clients can connect passive ports (optional, should resolve to ftp server ip address)
- `MIN_PORT` - minimum port number to be used for passive connections (optional, default `21000`)
- `MAX_PORT` - maximum port number to be used for passive connections (optional, default `21010`)

## USERS examples

- `user|password foo|bar|/home/foo`
- `user|password|/home/user/dir|10000`
- `user|password|/home/user/dir|10000|10000`
- `user|password||10000`
- `user|password||10000|82` : add to an existing group (www-data)

## FTP + FTPS (File Transfer Protocol + SSL) Example

```
  docker run -d \
    --name ftp-ftps-server \
    -p 21:21 \
    -p 21000-21010:21000-21010 \
    -v certs:/etc/vsftpd/cert/ \
    -e USERS="one|1234" \
    -e ADDRESS=<your_local_ip> \
    -e TLS_CERT="/etc/vsftpd/cert/fullchain.pem" \
    -e TLS_KEY="/etc/vsftpd/cert/fullchain.pem" \
    mercurimn/ftp-ftps-server:dev
```

