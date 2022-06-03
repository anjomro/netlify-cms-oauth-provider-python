# Netlify-cms-oauth-provider-python

[netlify-cms](https://www.netlifycms.org/) has its own github OAuth client. This is a python implementation based on the [Node.js](https://github.com/vencax/netlify-cms-github-oauth-provider) version.

Other implementations
- [Go lang](https://github.com/igk1972/netlify-cms-oauth-provider-go)
- [Node.js](https://github.com/vencax/netlify-cms-github-oauth-provider)


## Run using Docker-Compose
1) Make sure [Docker](https://docs.docker.com/get-docker/) and [Docker-Compose](https://docs.docker.com/compose/overview/) are installed.
2) Download `docker-compose.yml` from [here](https://raw.githubusercontent.com/anjomro/netlify-cms-oauth-provider-python/master/main.py)
   1) In a Linux Bash-Shell simply use: `curl -O https://raw.githubusercontent.com/anjomro/netlify-cms-oauth-provider-python/master/docker-compose.yml`
3) Change in the directory of the downloaded `docker-compose.yml` file and run `docker-compose up -d`
4) The service is now running on port `7080`. It is advised to use a reverse proxy like [Caddy](https://caddyserver.com/) to secure the service using a TLS Certificate.

# Run using Docker
1) Make sure [Docker](https://docs.docker.com/get-docker/) is installed.
2) Run `docker run -p 7080:80  --restart always -d --rm --name cms-oauth-provider ghcr.io/anjomro/netlify-cms-oauth-provider-python:latest`
3) The service is now running on port `7080`. It is advised to use a reverse proxy like [Caddy](https://caddyserver.com/) to secure the service using a TLS Certificate.

## 1) Install

For mac and linux
```
git clone https://github.com/davidejones/netlify-cms-oauth-provider-python.git
cd netlify-cms-oauth-provider-python
python -m venv /path/to/new/virtual/environment
source /path/to/new/virtual/environment/bin/activate
pip install -r requirements.txt
```

For windows
```
git clone https://github.com/davidejones/netlify-cms-oauth-provider-python.git
cd netlify-cms-oauth-provider-python
python -m venv /path/to/new/virtual/environment
C:\path\to\new\virtual\environment\bin\activate.bat
pip install -r requirements.txt
```

## 2) Config

### Auth Provider Config

Configuration is done with environment variables, which can be supplied as command line arguments, added in your app hosting interface, or loaded from a .env file.

**Example .env file:**

```
OAUTH_CLIENT_ID=f432a9casdff1e4b79c57
OAUTH_CLIENT_SECRET=pampadympapampadympapampadympa
REDIRECT_URL=https://your.server.com/callback
GIT_HOSTNAME=https://github.website.com
SSL_ENABLED=1
```

**Client ID & Client Secret:**
After registering your Oauth app, you will be able to get your client id and client secret on the next page.

**Redirect URL (optional):**
Include this if you  need your callback to be different from what is supplied in your Oauth app configuration.

**Git Hostname (Optional):**
This is only necessary for use with Github Enterprise.

### CMS Config
You also need to add `base_url` to the backend section of your netlify-cms's config file. `base_url` is the live URL of this repo with no trailing slashes.

```
backend:
  name: github
  repo: user/repo   # Path to your Github repository
  branch: master    # Branch to update
  base_url: https://your.server.com # Path to ext auth provider
```

## 3) Run it
With your virtual environment activated run the server as follows

`python main.py`
