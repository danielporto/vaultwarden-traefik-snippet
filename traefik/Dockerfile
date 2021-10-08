ARG TRAEFIK_BASE=v2.5
FROM traefik:${TRAEFIK_BASE}
ARG DEPLOYMENT_TYPE="dev"

# fix vulnerability  https://snyk.io/vuln/SNYK-ALPINE311-APKTOOLS-1534687
RUN apk add --no-cache --upgrade apk-tools
COPY ./${DEPLOYMENT_TYPE}/traefik.yaml /etc/traefik/traefik.yaml
COPY ./${DEPLOYMENT_TYPE}/dynamic.yaml /etc/traefik/dynamic.yaml