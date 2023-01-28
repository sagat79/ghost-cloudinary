# ghost-cloudinary
Ghost blog use cloudinary as storage.

This project uses Cloudinary image storage module for Ghost blog write by [eexit](https://github.com/eexit/ghost-storage-cloudinary). 

## 🚀 Getting Started

Check the [config env variables](https://ghost.org/docs/config/#configuration-options) for all supported configuration options!

### Using Docker-Compose

```yml
version: "3.7"
services:
  ghost:
    container_name: ghost
    image: sagat79/ghost-cloudinary:latest
    restart: always
    ports:
      - "2368:2368"
    depends_on:
      - db
    environment:
      # see https://ghost.org/docs/config/#configuration-options
      url: https://example.com
      database__client: mysql
      database__connection__host: db
      database__connection__user: ghost
      database__connection__password: ghostdbpass
      database__connection__database: ghostdb
      mail__transport: SMTP
      mail__from: 'YOU <you@gmail.com>'
      mail__options__service: gmail
      mail__options__host: smtp.gmail.com
      mail__options__port: 465
      mail__options__secureConnection: 'true'
      mail__options__auth__user: 'you@gmail.com'
      mail__options__auth__pass: 'APP Password'
      storage__active: 'ghost-storage-cloudinary'
      storage__ghost-storage-cloudinary__useDatedFolder: 'false'
      storage__ghost-storage-cloudinary__auth__cloud_name: 'CLOUDINARY-CLOUD-NAME'
      storage__ghost-storage-cloudinary__auth__api_key: 'CLOUDINARY-API-KEY'
      storage__ghost-storage-cloudinary__auth__api_secret: 'CLOUDINARY-API-SECRET'
      storage__ghost-storage-cloudinary__upload__use_filename: 'true'
      storage__ghost-storage-cloudinary__upload__unique_filename: 'false'
      storage__ghost-storage-cloudinary__upload__overwrite: 'false'
      storage__ghost-storage-cloudinary__upload__folder: 'blog-images'
      storage__ghost-storage-cloudinary__upload__tags: '["blog"]'
      storage__ghost-storage-cloudinary__fetch__quality: 'auto'
      storage__ghost-storage-cloudinary__fetch__secure: 'false'
      storage__ghost-storage-cloudinary__fetch__cdn_subdomain: 'true'
      imageOptimization__resize: 'false'
    volumes:
      - ./ghost-cloudinary/content:/var/lib/ghost/content
      #- ./ghost-cloudinary/config.production.json:/var/lib/ghost/config.production.json
      #- ./ghost-cloudinary/node_modules:/var/lib/ghost/node_modules
      
  db:
    container_name: ghost_mysql
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_mysql_root_password
      MYSQL_DATABASE: ghostdb
      MYSQL_USER: ghost
      MYSQL_PASSWORD: ghostdbpass
    ports:
      - "13928:3306"
    volumes:
      - ./ghost-cloudinary/mysql:/var/lib/mysql
```

### Docker Pull: 
[docker pull ghost-cloudinary:latest](https://hub.docker.com/r/sagat79/ghost-cloudinary).