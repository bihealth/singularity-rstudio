BootStrap: library
From: holtgrewe/default/r:4.0.5

%labels
  Maintainer Jeremy Nicklas
  RStudio_Version 1.2.5033

%help
  This will run RStudio Server

%apprun rserver
  exec rserver "${@}"

%runscript
  exec rserver "${@}"

%environment
  export PATH=/usr/lib/rstudio-server/bin:${PATH}

%setup
  install -Dv \
    rstudio_auth.sh \
    ${SINGULARITY_ROOTFS}/usr/lib/rstudio-server/bin/rstudio_auth
  install -Dv \
    ldap_auth.py \
    ${SINGULARITY_ROOTFS}/usr/lib/rstudio-server/bin/ldap_auth

%post
  # Software versions
  export RSTUDIO_VERSION=1.2.5042

  # Install RStudio Server
  yum clean all -y
  yum upgrade -y
  curl -O https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-${RSTUDIO_VERSION}-x86_64.rpm
  yum install -y rstudio-server-rhel-${RSTUDIO_VERSION}-x86_64.rpm
  rm -f rstudio-server-rhel-${RSTUDIO_VERSION}-x86_64.rpm

  # Add support for LDAP authentication
  yum install -y python36-ldap3

  # Clean up
  yum clean all
