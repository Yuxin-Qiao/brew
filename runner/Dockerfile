ARG HOMEBREW_BREW_IMAGE=ghcr.io/homebrew/brew:main

FROM ghcr.io/actions/actions-runner:latest AS runner-source

FROM ${HOMEBREW_BREW_IMAGE}

COPY --from=runner-source --chown=linuxbrew:linuxbrew /home/runner/ /home/linuxbrew/actions-runner/

COPY --chown=linuxbrew:linuxbrew startup.sh /home/linuxbrew/startup.sh
RUN chmod +x /home/linuxbrew/startup.sh

# Must be set when running the container (e.g., via `docker run -e RUNNER_JITCONFIG=...`)
# This caries the GitHub configuration the runner needs to start, so we can't set it to any meaningful default.
# This line ensures that it is set.
ENV RUNNER_JITCONFIG=

# Do not let .NET load icu to avoid poluting the image
ENV DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1

ENTRYPOINT ["/home/linuxbrew/startup.sh"]
