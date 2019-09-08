FROM nginx
COPY nginx.conf /etc/nginx/nginx.conf
ARG RADIATOR_HOST
RUN sed -i -- 's/%%RADIATOR_HOST%%/$RADIATOR_HOST/g' /etc/nginx/nginx.conf
