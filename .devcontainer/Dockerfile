FROM python:3.13-slim

# System dependencies for building Python wheels and MkDocs plugins
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    curl \
    ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Configure a non-root user for VS Code devcontainers
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -m -s /bin/bash --uid $USER_UID --gid $USER_GID $USERNAME

USER $USERNAME
WORKDIR /workspace

# Install MkDocs + plugins globally (no PATH issues)
RUN pip install --no-cache-dir mkdocs mkdocs-material mkdocs-macros-plugin mkdocs-autorefs pymdown-extensions

# OPTIONAL fallback
# ENV PATH="/home/${USERNAME}/.local/bin:${PATH}"