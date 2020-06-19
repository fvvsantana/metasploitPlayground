# docker build -t "victim" .
# docker run -it --volume=/tmp/victim/:/data victim:latest
FROM tleemcjr/metasploitable2:latest

CMD ["/bin/bash", "-c", "/bin/services.sh && bash"]
# CMD /bin/services.sh && bash
