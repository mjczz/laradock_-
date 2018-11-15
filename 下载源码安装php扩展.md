
## 安装swoole扩展
```sh
# percl安装不成功，czz迫不得已才用此方式,安装了特定的版本
RUN if [ ${INSTALL_SWOOLE} = true ]; then \
    # Install the phpredis extension
    curl -L -o /tmp/swoole4.2.6.tar.gz "https://github.com/swoole/swoole-src/archive/v4.2.6.tar.gz" \
    && mkdir -p swoole \
    && tar -C swoole -zxvf /tmp/swoole4.2.6.tar.gz --strip 1 \
    && ( \
        cd swoole \
        && phpize \
        && ./configure \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r swoole \
    && rm /tmp/swoole4.2.6.tar.gz \
    && docker-php-ext-enable swoole \
;fi
```

## 安装phpredis扩展
```sh
# percl安装不成功，czz迫不得已才用此方式,安装了特定的版本
RUN if [ ${INSTALL_PHPREDIS} = true ]; then \
    # Install the phpredis extension
    curl -L -o /tmp/phpredis4.1.1.tar.gz "https://github.com/phpredis/phpredis/archive/4.1.1.tar.gz" \
    && mkdir -p phpredis \
    && tar -C phpredis -zxvf /tmp/phpredis4.1.1.tar.gz --strip 1 \
    && ( \
        cd phpredis \
        && phpize \
        && ./configure \
        && make -j$(nproc) \
        && make install \
    ) \
    && rm -r phpredis \
    && rm /tmp/phpredis4.1.1.tar.gz \
    &&  docker-php-ext-enable redis \
;fi

```