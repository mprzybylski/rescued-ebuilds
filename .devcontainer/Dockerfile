FROM gentoo/stage3:20240422

RUN emerge --sync
# Minimal requirements for dev containers
RUN emerge dev-vcs/git app-admin/sudo

# Unprivilged user to make UID/GID mapping easier
ARG USERNAME
ARG USER_UID
RUN echo "CREATE_MAIL_SPOOL=no" >> /etc/default/useradd && \
    useradd -U $USERNAME --uid $USER_UID  && \
    mkdir -m 0770 /etc/sudoers.d && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

# Project-specific tooling
RUN emerge sys-devel/crossdev app-eselect/eselect-repository

# Project-specific data
COPY resources/etc/portage/repos.conf/rescued-ebuilds.conf /etc/portage/repos.conf

USER $USERNAME