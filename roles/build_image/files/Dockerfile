FROM ubuntu:24.04

# Set the timezone and noninteractive mode
ARG TZ=US DEBIAN_FRONTEND=noninteractive

# Define default values for the Enviroment Variables
ENV SEED=false

# Install app packages
RUN apt-get update && apt-get install -y \
    curl \
    unzip \
    nodejs \
    git \
    postgresql

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash

ENV BUN_INSTALL="/root/.bun"
ENV PATH="$BUN_INSTALL/bin:$PATH"

# Clone Airtrail repository
RUN git clone https://github.com/JohanOhly/AirTrail.git
WORKDIR /AirTrail

# Install Bun dependencies
RUN bun install

ENV NODE_OPTIONS="--max-old-space-size=4096"

RUN bun run build

# Create Airtrail configuration file
#RUN cp ./.env.example .env

# Copy start script
COPY ./script.sh .

# Add execution permission to start script
RUN chmod +x script.sh

# Expose port 3000
EXPOSE 3000

# Start Airtrail server
ENTRYPOINT ["./script.sh"]

CMD [ "./script.sh" ]