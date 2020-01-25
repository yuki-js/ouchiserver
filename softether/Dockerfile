FROM debian:stable-slim

RUN apt-get update && apt-get upgrade -y && apt-get install curl build-essential net-tools -y
RUN curl -sSL https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.32-9731-beta/softether-vpnserver-v4.32-9731-beta-2020.01.01-linux-arm_eabi-32bit.tar.gz | tar -zxvf -
WORKDIR /vpnserver
RUN make i_read_and_agree_the_license_agreement
RUN chmod 600 * && chmod 700 vpncmd && chmod 700 vpnserver
RUN mkdir config
RUN ln -s config/vpn_server.config vpn_server.config
EXPOSE 500/udp 4500/udp 1701/tcp 1194/udp 443/tcp
    
CMD ["/vpnserver/vpnserver", "execsvc"]
