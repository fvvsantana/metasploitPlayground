# docker build -t "attacker" .
# docker run -it attacker:latest
# ./msfconsole -r docker/msfconsole.rc -y config/database.yml

FROM metasploitframework/metasploit-framework:latest

# Install tcpdump
RUN apk add --no-cache tcpdump

# Override entrypoint, because parent entrypoint starts machine on user "msf"
ENTRYPOINT []

# Open bash as default command
CMD ["/bin/bash"]
