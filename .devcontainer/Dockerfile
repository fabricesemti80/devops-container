FROM ubuntu:20.04
ENV brew_packages "ansible font-hack-nerd-font tfenv tgenv starship pkenv pre-commit terraform-docs "
ENV terraform_version "1.3.9"
ENV terragrunt_version "0.43.2"
ENV packer_version "1.8.3"

# Install necessary packages for Homebrew
RUN apt-get update && \
    apt-get install -y build-essential curl file git

# Install Homebrew
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Set up Homebrew environment variables
ENV PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH"
ENV MANPATH="/home/linuxbrew/.linuxbrew/share/man:$MANPATH"
ENV INFOPATH="/home/linuxbrew/.linuxbrew/share/info:$INFOPATH"

# Install brew packages
RUN brew tap homebrew/cask-fonts
RUN brew tap kwilczynski/homebrew-pkenv
RUN brew install ${brew_packages}

# Install Terraform / Terragrunt / Packer
RUN tfenv install ${terraform_version}
RUN tgenv install ${terragrunt_version}
RUN pkenv install ${packer_version}

# # Set default versions for Terraform / Terragrunt / Packer
RUN tfenv use ${terraform_version}
RUN tgenv use ${terragrunt_version}
RUN pkenv use ${packer_version}

# Add Starship to bash profile
RUN echo 'eval "$(starship init bash)"' >> ~/.bashrc
