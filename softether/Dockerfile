FROM debian:stable-slim

ARG HUB_NAME="DefaultHub"
ARG HUB_PASSWD="DefaultHubPassword"
ARG USER_NAME="DefaultUser"
ARG USER_PASSWD="DefaultUserPassword"
ARG COMMON_SECRET="vpn"

RUN apt-get update && apt-get upgrade -y && apt-get install curl build-essential -y
RUN curl -sSL https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.32-9731-beta/softether-vpnserver-v4.32-9731-beta-2020.01.01-linux-arm_eabi-32bit.tar.gz | tar -zxvf -
WORKDIR /vpnserver
RUN make i_read_and_agree_the_license_agreement
RUN chmod 600 * && chmod 700 vpncmd && chmod 700 vpnserver

EXPOSE 5555
EXPOSE 1194
EXPOSE 443
EXPOSE 992

RUN vpnserver start && \
    sleep 5 && \
    vpncmd /SERVER localhost /ADMINHUB:DEFAULT /CMD HubCreate ${HUB_NAME} /PASSWORD:${HUB_PASSWD} && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD UserCreate ${USER_NAME} /GROUP:none /REALNAME:none /NOTE:none && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD UserPasswordSet ${USER_NAME} /PASSWORD:${USER_PASSWD} && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD IPsecEnable /L2TP:yes /L2TPRAW:yes /ETHERIP:no /PSK:${COMMON_SECRET} /DEFAULTHUB:${HUB_NAME} && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD SecureNatEnable && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD NatEnable && \
    vpncmd /SERVER localhost /ADMINHUB:${HUB_NAME} /CMD DHCPEnable && \
    vpnserver stop
    
CMD ["/vpnserver/vpnserver", "execsvc"]