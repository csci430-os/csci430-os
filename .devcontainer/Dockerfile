# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.238.0/containers/cpp/.devcontainer/base.Dockerfile

# [Choice] Debian / Ubuntu version (use Debian 11, Ubuntu 18.04/22.04 on local arm64/Apple Silicon): debian-11, debian-10, ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT="ubuntu-24.04"
FROM mcr.microsoft.com/devcontainers/cpp:${VARIANT}

# [Optional] Install CMake version different from what base image has already installed. 
# CMake reinstall choices: none, 3.21.5, 3.22.2, or versions from https://cmake.org/download/
ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="none"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/
RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# [Optional] Uncomment this section to install additional packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends build-essential clang-format doxygen pandoc

# Uncomment the following instead to get texlive/latex installed, so can build pdf documents
# from markdown/tex sources
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends doxygen doxygen-latex graphviz \
    texlive-base texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended texlive-full \
    texlive-bibtex-extra texlive-fonts-extra texlive-science snakemake python3-pweave  biber 
