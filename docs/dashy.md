# Dashy

Start up dashy in the dashy repo with the config file and the icons.

Start-up command:
```bash
docker run -d \                                                                                                                                                                                                                                        ─╯
  -p 8080:8080 \
  -v $(pwd)/conf.yml:/app/user-data/conf.yml \
  -v ~/selfhosted/dashy/item-icons:/app/user-data/item-icons/ \
  --name my-dashboard \
  --restart=always \
  lissy93/dashy:latest
```
