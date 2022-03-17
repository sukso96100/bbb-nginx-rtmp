# BBB Multistream Config files

Uses [BigBlueButton-liveStreaming](https://github.com/aau-zid/BigBlueButton-liveStreaming), [nginx-rtmp-docker](https://github.com/tiangolo/nginx-rtmp-docker) and Docker Compose to setup BigBlueButton streaming.

## Usage

Clone this repo on your machine then modify `nginx/nginx.conf` and `docker-compose.yml` to fit your needs

### Editing `nginx/nginx.conf`

Adding `push <RTMP_URL_WITH_STREAM_KEY>` on `application live` would be enough in most cases

See [documentation related to `nginx-rtmp-module`](https://github.com/arut/nginx-rtmp-module/wiki/Directives) for more detailed configuration instruction.

```
worker_processes auto;
rtmp_auto_push on;
events {}
rtmp {
    server{
        listen 1935;
        chunk_size 4096;

        #Enable live broadcast service
        application live {
            live on;
            record off;

            # Push, restream RTMP
            # Place your RTMP Stream URL below

            # YouTube
            push rtmp://a.rtmp.youtube.com/live2/{STREAM_KEY};

            # Twitch (Seoul 3)
            push rtmp://sel03.contribute.live-video.net/app/{stream_key};


        }
    }
}
```

### Editing `docker-compose.yml`

At least update `BBB_URL`, `BBB_MEETING_ID`, `BBB_SECRET`, `BBB_STREAM_URL` variable so that you can stream the BBB room that you want to stream. See [here](https://github.com/aau-zid/BigBlueButton-liveStreaming) for more detailed configuration instruction.

### Running streaming setup
You need Docker Compose to be installed on your machine. See [this documentation about installing Docker Compose](https://docs.docker.com/compose/install/)

After installing Docker Compose, Simply use following commands to start and stop streaming setup
```bash
# Start streaming on background
docker-compose up -d

# See log output
docker-compose logs

# Stop streaming setup
docker-compose stop
```