FROM alpine

## Alpine with Go Git
RUN apk add --no-cache --update ca-certificates wget \
        && wget https://downloads.rclone.org/rclone-current-linux-amd64.zip \
	&& unzip rclone-current-linux-amd64.zip \
	&& mv rclone-*/rclone /usr/sbin/rclone

FROM alpine
RUN apk add --no-cache --update fuse ca-certificates 
COPY --from=0 /usr/sbin/rclone /usr/sbin/rclone

ENTRYPOINT /usr/sbin/rclone mount $MountCommands $RemotePath $AccessFolder

# Use this docker Options in run
# --cap-add SYS_ADMIN --device /dev/fuse --security-opt apparmor:unconfined
# -v /path/to/config/.rclone.conf:/config/.rclone.conf
# -v /mnt/mediaefs:/mnt/mediaefs:shared
