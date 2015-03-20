FROM       privatetravis/phpenv
MAINTAINER nick_schuch

##
# PHP.
##

# Remove fpm since apxs2 (apache) support is being compiled.
RUN sed -i '/--enable-fpm/d' /root/.phpenv/plugins/php-build/share/php-build/default_configure_options
RUN sudo /root/.phpenv/plugins/php-build/install.sh
RUN sudo php-build -i development --pear 5.5.15 $HOME/.phpenv/versions/5.5.15
# Remove apxs2 since fpm support is being compiled.
RUN sed -i '/--with-apxs2/d' /root/.phpenv/plugins/php-build/share/php-build/default_configure_options
RUN echo "--enable-fpm" >> /root/.phpenv/plugins/php-build/share/php-build/default_configure_options
RUN sudo /root/.phpenv/plugins/php-build/install.sh
RUN sudo php-build -i development --pear 5.5.15 $HOME/.phpenv/versions/5.5.15
RUN sudo chown -R root:root $HOME/.phpenv
RUN phpenv rehash
RUN phpenv global 5.5.15

ENTRYPOINT ["travis", "run", "--skip-version-check", "--skip-completion-check"]
