FROM alpine

ENV GOPATH="/go" \
    AccessFolder="/mnt" \
    RemotePath="mediaefs:" \
    ConfigDir="/config" \
    ConfigName=".rclone.conf" \
    MountCommands="--allow-other" \
    UnmountCommands="-u -z"

## Alpine with Go Git
RUN apk add --no-cache --update ca-certificates fuse fuse-dev \
        && curl https://downloads.rclone.org/rclone-current-linux-amd64.zip --output rclone-current-linux-amd64.zip \
	&& unzip rclone-current-linux-amd64.zip \
	&& mv rclone-*/rclone /usr/sbin/rclone
	&& rm -rf /tmp/* /var/cache/apk/* /var/lib/apk/lists/*

ADD start.sh /start.sh
RUN chmod +x /start.sh 

CMD ["/start.sh"]

# Use this docker Options in run
# --cap-add SYS_ADMIN --device /dev/fuse --security-opt apparmor:unconfined
# -v /path/to/config/.rclone.conf:/config/.rclone.conf
# -v /mnt/mediaefs:/mnt/mediaefs:shared
