FROM surnet/alpine-wkhtmltopdf:3.8-0.12.5-full as wkhtmltopdf
FROM node:8.11.4-alpine
# FROM surnet/alpine-wkhtmltopdf:3.12-0.12.6

# Install dependencies for wkhtmltopdf
RUN apk add --no-cache \
  libstdc++ \
  libx11 \
  libxrender \
  libxext \
  libssl1.0 \
  ca-certificates \
  fontconfig \
  freetype \
  ttf-dejavu \
  ttf-droid \
  ttf-freefont \
  ttf-liberation \
  ttf-ubuntu-font-family \
  bash \
# Install node-gyp dependencies
&& apk add --no-cache --virtual .gyp python make g++ \
&& apk add --no-cache --virtual .build-deps \
  msttcorefonts-installer \
\
# Install microsoft fonts
&& update-ms-fonts \
&& fc-cache -f \
\
# Clean up when done
&& rm -rf /tmp/* \
&& apk del .build-deps

# Copy wkhtmltopdf files from docker-wkhtmltopdf image
COPY --from=wkhtmltopdf /bin/wkhtmltopdf /bin/wkhtmltopdf
COPY --from=wkhtmltopdf /bin/wkhtmltoimage /bin/wkhtmltoimage
COPY --from=wkhtmltopdf /bin/libwkhtmltox* /bin/


WORKDIR /usr/src/app1

EXPOSE 5000

RUN npm install

CMD [ "npm", "start" ]
