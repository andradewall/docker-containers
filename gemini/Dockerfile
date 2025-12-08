FROM node:lts-slim

# Install git (often needed by Gemini CLI tools) and other basics
RUN apt-get update && apt-get install -y git procps && rm -rf /var/lib/apt/lists/*

# Install the Gemini CLI globally
RUN npm install -g @google/gemini-cli@latest

# Set the working directory
WORKDIR /workspace

# Set the entrypoint to the gemini command
ENTRYPOINT ["gemini"]
