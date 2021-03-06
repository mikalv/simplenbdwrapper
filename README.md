# simplenbdserver

Ubuntu based container exposes named network block devices

## To run a server

The basic format is:

```
docker run -d \
--name nbd \
-v <local_block_dir>:<container_block_dir>
-p "10809:8520" \
neiltheblue/simplenbdwrapper \
<container_block_dir>[/<img_file>] ...
```

Where `<local_block_dir>` is a directory on your host with block devices to export. They can be mapped anywhere in your container and referenced with one or more command options `<container_block_dir>/<img_file>` to export a specific image file or `<container_block_dir>` to export all files in the directory. For example:

```
docker run -d \
--name nbd \
-v /images:/block
-p "10809:8520" \
neiltheblue/simplenbdwrapper \
/block/disk1.img /block/disk2.img
```
The options may also include `--cow` to run in copy-on-write mode and `--readonly` to run in readonly mode.
