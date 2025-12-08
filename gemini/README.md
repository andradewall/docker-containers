# 🐳 Gemini CLI (Dockerized)

A persistent, daily-driver setup for Google's Gemini CLI using Docker. This setup keeps your host system clean, persists your login session, and secures your API key in a standard `.env` file.

## 📋 1. Setup Configuration

Create a `.env` file to store your credentials securely. This file will be ignored by git (if you added it to `.gitignore`) and read directly by Docker.

1.  **Create the file:**

    ```bash
    cp .env.example .env 2>/dev/null || touch .env
    ```

    *(If you don't have an example file, just creating a new `.env` works).*

2.  **Add your API Key:**
    Open `.env` with your editor (e.g., `nano .env`) and add the following line:

    ```ini
    GEMINI_API_KEY=AIzaSy...YourKeyHere...
    ```

    > **Note:** Get your key from [Google AI Studio](https://aistudio.google.com/).

## 🏗️ 2. Build the Image

Build the Docker image using the `Dockerfile` present in this repository.

```bash
docker build -t gemini-cli .
```

## 🚀 3. Installation (The Wrapper)

To use Gemini from *any* directory on your system (not just this folder), you need to add a shell function to your configuration.

1.  **Get the absolute path** of your current repo folder:

    ```bash
    pwd
    # Example output: /home/user/gemini-docker
    ```

2.  **Edit your shell config** (`~/.zshrc` for CachyOS/Manjaro or `~/.bashrc`):

    ```bash
    nano ~/.zshrc
    ```

3.  **Paste this function at the bottom:**
    *Make sure to replace `/path/to/cloned/repo` with the output from step 1.*

    ```bash
    gemini() {
      # Path to where you cloned the repo (so it can find your .env)
      local INSTALL_DIR="/path/to/cloned/repo"

      docker run -it --rm \
        --env-file "$INSTALL_DIR/.env" \
        -v gemini_config:/root/.gemini \
        -v "$(pwd):/workspace" \
        gemini-cli "$@"
    }
    ```

4.  **Reload your shell:**

    ```bash
    source ~/.zshrc
    ```

## 🎮 4. Usage

You can now type `gemini` in any terminal window.

### **Interactive Chat**

Start a conversation. The session history is saved in the docker volume `gemini_config`.

```bash
gemini chat
```

### **One-Off Commands**

Send a quick prompt without entering the interactive mode.

```bash
gemini prompt "Explain the difference between TCP and UDP"
```

### **File Context**

Because the wrapper mounts `$(pwd)` to `/workspace`, Gemini can read files in your current directory.

```bash
# Ask Gemini to review code in your current folder
gemini chat
> @index.php Can you explain what this Laravel controller is doing?
```

## 🛠️ Maintenance

  * **Update:** To get the latest version of the Gemini CLI tools, just pull the latest changes (if any) and rebuild:
    ```bash
    docker build --no-cache -t gemini-cli .
    ```
  * **Reset Data:** To clear your chat history/login cache:
    ```bash
    docker volume rm gemini_config
    ```
