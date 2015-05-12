FROM rock/tomcat

MAINTAINER dchekirda@gmail.com

ADD sample.war /tomcat/webapps/

EXPOSE 8080
EXPOSE 9001

CMD ["supervisord", "-c", "/etc/supervisor.conf"]
