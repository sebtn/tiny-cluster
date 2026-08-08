FROM mcr.microsoft.com/devcontainers/base:debian-13
COPY --from=jdxcode/mise /usr/local/bin/mise /usr/local/bin/

# make sure mise is activated in both zsh and bash. Might be overridden by a user's dotfiles.
RUN echo 'eval "$(mise activate bash)"' >> /home/vscode/.bashrc && \
    echo 'eval "$(mise activate zsh)"' >> /home/vscode/.zshrc


# Rio's implementation
#RUN curl -sSLf https://mise.run | MISE_INSTALL_PATH=/usr/local/bin/mise sh && \
#   echo 'eval "$(mise activate zsh)"' >> /home/vscode/.zshrc && \
#  echo 'eval "$(mise activate bash)"' >> /home/vscode/.bashrc
