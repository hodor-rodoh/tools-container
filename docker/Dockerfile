FROM python:3.7-alpine

ENV TFVERSION=0.11.3
ENV GRUNT_VERSION=0.18.3
ENV TERRAFORM_DOCS_VERSION=0.5.0

# Install AWS CLI
RUN pip install awscli --upgrade

# Override default ENTRYPOINT so that we can use bash
ENTRYPOINT [""]

# Add bash to facilitate troubleshooting
RUN apk --no-cache update && \
    apk --no-cache add bash python py-pip py-setuptools ca-certificates curl groff less openssl wget unzip

# Install Kubectl
RUN set -ex \
        && curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
        && chmod +x ./kubectl \
        && mv ./kubectl /usr/local/bin/kubectl \
        \
        # Install AWS IAM AUTH
        && curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.12.7/2019-03-27/bin/linux/amd64/aws-iam-authenticator \
        && chmod +x ./aws-iam-authenticator \
        && mv ./aws-iam-authenticator /usr/local/bin/aws-iam-authenticator \
        \
        # Install Helm
        && curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh \
        && chmod +x ./get_helm.sh \
        && ./get_helm.sh \
        && rm get_helm.sh \
        \
        # Install Terraform
        && curl https://releases.hashicorp.com/terraform/${TFVERSION}/terraform_${TFVERSION}_linux_amd64.zip > terraform_${TFVERSION}_linux_amd64.zip \
        && unzip terraform_${TFVERSION}_linux_amd64.zip -d /usr/local/bin \
        && rm -f terraform_${TFVERSION}_linux_amd64.zip \
        \
        # Install Terragrunt
        && curl -sL https://github.com/gruntwork-io/terragrunt/releases/download/v${GRUNT_VERSION}/terragrunt_linux_amd64 > /usr/local/bin/terragrunt \
        && chmod +x /usr/local/bin/terragrunt \
        \
        # Install terraform docs
        && curl -L https://github.com/segmentio/terraform-docs/releases/download/v${TERRAFORM_DOCS_VERSION}/terraform-docs-v${TERRAFORM_DOCS_VERSION}-linux-amd64 > /usr/local/bin/terraform-docs\
        && chmod +x /usr/local/bin/terraform-docs
