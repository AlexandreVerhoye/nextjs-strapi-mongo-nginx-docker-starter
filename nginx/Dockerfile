FROM nginx
# FROM nginx:alpine
COPY ./conf.d /etc/nginx/conf.d
COPY ./script/run.sh /run.sh
EXPOSE 80 443 8090

# CMD ["nginx", "-g", "daemon off;"]
CMD ["/bin/bash", "/run.sh"]