

## percl安装不成功，czz迫不得已才用此方式,安装了特定的版本

```sh
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
    && echo "extension=swoole.so" >> /etc/php/${LARADOCK_PHP_VERSION}/mods-available/swoole.ini && \
    ln -s /etc/php/${LARADOCK_PHP_VERSION}/mods-available/swoole.ini /etc/php/${LARADOCK_PHP_VERSION}/cli/conf.d/20-swoole.ini \
;fi

```