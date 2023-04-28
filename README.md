# nginx-rtmp
Out-of-the-box Nginx-RTMP server

Provides `X86_64` and `arm64` platforms, for both PC and Raspberry Pi

Built on the `alpine:3.17` image, super small and easy to use

# Version records
The version number follows the version number of the Nginx Stable branch by default, created starting with 1.21.1
- `1.24.0`, `latest`

# Github repository address
Mirror Github repository: [https://github.com/zenety/nginx-rtmp](https://github.com/zenety/nginx-rtmp)

# Uses of this mirror
`Nginx` is a high-performance HTTP server, this image integrates the `nginx-rtmp-module` plugin, which can be configured as a live streaming server

This mirror is suitable for `PS4`, `PS5` live streaming, but also can be used as a general streaming server to use

# How to use
## Turn on the service
- To use as a live streaming server, you can enable the service with the following command:

```docker run -d --name nginx-rtmp -p 1935:1935 -p 8080:8080 zenety/nginx-rtmp ```

The browser accesses ``http://localhost:8080`` and displays the following screen: the service is successfully started
``If you are running on router, nas or raspberry pi, please change localhost to host IP address by yourself``
- If you don't need the panel, you can leave 8080 unmapped: `

```docker run -d --name nginx-rtmp -p 1935:1935 zenety/nginx-rtmp ```

## PS5 Push Streaming
Currently, PS5 live streaming only supports Twitch and Oilcan, so the general idea is to hijack Twitch to push the stream to `nginx-rtmp` in order to achieve the goal
- Add the DNSMasq list and hijack the Twitch live stream address to your docker host address
- Save the application router settings
- Open PS5, press share and select live stream from Twitch
- If the stream is successfully hijacked and the module is working properly, the next step is to display an ID in the web page

`live__***************`
- Copy this ID and paste it into the following link to replace the live__****** part. Note that the localhost in this link should also be replaced with the IP of your host

`rtmp://localhost:1935/app/live__******`
- Use OBS to load and then live and you're done

```
docker run -d --name nginx-rtmp -p 1935:1935 -p 8080:8080 \
-v nginx.conf:/etc/nginx/nginx.conf zenety/nginx-rtmp
```
