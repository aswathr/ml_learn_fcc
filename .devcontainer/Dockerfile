FROM mcr.microsoft.com/devcontainers/anaconda

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
# Additionally copy requirements.txt requirements_uninstall.txt to resolve some package issues by uninstalling and reinstalling them
COPY environment.yml* .devcontainer/noop.txt requirements.txt requirements_uninstall.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; fi

# Uninstall and reinstall
RUN pip3 uninstall -y -r /tmp/conda-tmp/requirements_uninstall.txt
RUN pip3 --no-cache-dir install -r /tmp/conda-tmp/requirements.txt

# Remove tmp dir
RUN rm -rf /tmp/conda-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
