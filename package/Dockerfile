FROM registry-local.kubeup.cn/mips64el/loongnix:21 as base
ADD build/out/data.tar.gz /image
RUN mkdir -p /image/etc/ssl/certs /image/run /image/var/run /image/tmp /image/lib/modules /image/lib/firmware && \
     cp /etc/ssl/certs/ca-bundle.crt /image/etc/ssl/certs/ca-certificates.crt
RUN cd image/bin && \
    rm -f k3s && \
    ln -s k3s-server k3s

FROM registry-local.kubeup.cn/mips64el/loongnix:21
COPY --from=base /bin/sh /bin/sh
RUN chmod 1777 /tmp
RUN yum install -y libseccomp &&
    yum clean all &&
    mkdir -p /etc && \
    echo 'hosts: files dns' > /etc/nsswitch.conf
VOLUME /var/lib/rancher/k3s
VOLUME /var/lib/kubelet
VOLUME /var/lib/cni
VOLUME /var/log
ENV PATH="$PATH:/bin/aux"
#ENTRYPOINT ["/bin/k3s"]
#CMD ["agent"]
