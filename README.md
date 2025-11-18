# Mailbox

Multi-platform Docker container with utilities to process Mailbox files and Maildir directories (`mail`, `mail-parser`, `mutt`...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](mail/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-mail/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-mail/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/mail)](https://hub.docker.com/r/leplusorg/mail)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/mail)](https://hub.docker.com/r/leplusorg/mail)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/mail?sort=semver)](https://hub.docker.com/r/leplusorg/mail)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/10081/badge)](https://bestpractices.coreinfrastructure.org/projects/11219)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/leplusorg/docker-mail/badge)](https://securityscorecards.dev/viewer/?uri=github.com/leplusorg/docker-mail)

## Example

Let's say that you want to know the number of messages in a Maildir folder in your current working directory:

**Mac/Linux**

```bash
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" leplusorg/mail messages maildir
```

**Windows**

In `cmd`:

```batch
docker run --rm -t --net=none -v "%cd%:/tmp" leplusorg/mail messages maildir
```

In PowerShell:

```pwsh
docker run --rm -t --net=none -v "${PWD}:/tmp" leplusorg/mail messages maildir
```

## Software Bill of Materials (SBOM)

To get the SBOM for the latest image (in SPDX JSON format), use the
following command:

```bash
docker buildx imagetools inspect leplusorg/mail --format '{{ json (index .SBOM "linux/amd64").SPDX }}'
```

Replace `linux/amd64` by the desired platform (`linux/amd64`, `linux/arm64` etc.).

## Sigstore

[Sigstore](https://docs.sigstore.dev) is trying to improve supply
chain security by allowing you to verify the origin of an
artifcat. You can verify that the image that you use was actually
produced by this repository. This means that if you verify the
signature of the Docker image, you can trust the integrity of the
whole supply chain from code source, to CI/CD build, to distribution
on Maven Central or whever you got the image from.

You can use the following command to verify the latest image using its
sigstore signature attestation:

```bash
cosign verify leplusorg/mail --certificate-identity-regexp 'https://github\.com/leplusorg/docker-mail/\.github/workflows/.+' --certificate-oidc-issuer 'https://token.actions.githubusercontent.com'
```

The output should look something like this:

```text
Verification for index.docker.io/leplusorg/xml:main --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":...
```

For instructions on how to install `cosign`, please read this [documentation](https://docs.sigstore.dev/cosign/system_config/installation/).

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-mail/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

## Security

Please read [SECURITY.md](SECURITY.md) for details on our security policy and how to report security vulnerabilities.

## Code of Conduct

Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for details on our code of conduct.

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file.
