FROM ansible/centos7-ansible:stable

RUN rm -rf /etc/yum.repos.d/* && curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
ADD nginx.repo /etc/yum.repos.d/
RUN yum makecache fast && yum install -y createrepo nginx && yum clean all
ADD rpms /usr/share/nginx/html/rpms
RUN createrepo /usr/share/nginx/html/rpms/
ADD wheels /wheels
RUN cd /wheels && pip install --use-wheel --no-index --find-links=./ kolla_ansible*.whl

CMD ["nginx", "-g", "daemon off;"]

