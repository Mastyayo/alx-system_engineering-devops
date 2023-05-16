# 0x1A. Application Server

### Concepts

_For this project, we expect you to look at these concepts:_

*   [Web Server](/concepts/17)
*   [Server](/concepts/67)
*   [Web stack debugging](/concepts/68)

![](https://s3.amazonaws.com/alx-intranet.hbtn.io/uploads/medias/2018/9/c7d1ed0a2e10d1b4e9b3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARDDGGGOUSBVO6H7D%2F20230307%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230307T005659Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=fcedf8945abb119ab77321cb6b23ac14e331fa801cec464998fcc300992fc4e0)

Background Context
------------------

[![](https://s3.amazonaws.com/alx-intranet.hbtn.io/uploads/medias/2019/6/2ea1058f813d42c61f48.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARDDGGGOUSBVO6H7D%2F20230307%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230307T005659Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=07d3a896307ea3f3682088154a9fe6bbbc3ec887592596357133bdce7149f07c)](https://youtu.be/pSrKT7m4Ego)

Your web infrastructure is already serving web pages via `Nginx` that you installed in your [first web stack project](/rltoken/95oRNZ-zRGwLxtWECJqsWA "first web stack project"). While a web server can also serve dynamic content, this task is usually given to an application server. In this project you will add this piece to your infrastructure, plug it to your `Nginx` and make is serve your Airbnb clone project.

Resources
---------

**Read or watch**:

*   [Application server vs web server](/rltoken/B9fOBzIxX_t1289WAuRzJw "Application server vs web server")
*   [How to Serve a Flask Application with Gunicorn and Nginx on Ubuntu 16.04](/rltoken/kpG6RwmwRJHzRmGUM_ERcA "How to Serve a Flask Application with Gunicorn and Nginx on Ubuntu 16.04") (As mentioned in the video, do **not** install Gunicorn using `virtualenv`, just install everything globally)
*   [Running Gunicorn](/rltoken/2LF1j7xKJGYaUtD1HKgUeQ "Running Gunicorn")
*   [Be careful with the way Flask manages slash](/rltoken/lEg0zpkkDcLtdl3VD4ACRQ "Be careful with the way Flask manages slash") in [route](/rltoken/Zn8fYk-U9YRm7Z5Coqqb0g "route") - `strict_slashes`
*   [Upstart documentation](/rltoken/mcEsKqFsjJA3tHAjiMknaw "Upstart documentation")

Requirements
------------

### General

*   A `README.md` file, at the root of the folder of the project, is mandatory
*   Everything Python-related must be done using `python3`
*   All config files must have comments

### Bash Scripts

*   All your files will be interpreted on Ubuntu 16.04 LTS
*   All your files should end with a new line
*   All your Bash script files must be executable
*   Your Bash script must pass `Shellcheck` (version `0.3.7-5~ubuntu16.04.1` via `apt-get`) without any error
*   The first line of all your Bash scripts should be exactly `#!/usr/bin/env bash`
*   The second line of all your Bash scripts should be a comment explaining what is the script doing

## Tasks :page_with_curl:

* **0. Set up development with Python**
  * In this task, I configured the file `web_flask/0-hello_route.py` from my
  [AirBnB_clone_v2](https://github.com/bdbaraban/AirBnB_clone_v2) to serve content
  on the route `/airbnb-onepage/`, running on port `5000`.

* **1. Set up production with Gunicorn**
  * This task involved setting up a production environment, installing and configuring
  Gunicorn to serve the same file from task 0.

* **2. Serve a page with Nginx**
  * [2-app_server-nginx_config](./2-app_server-nginx_config): Nginx configuration file
  proxying requests on the route `/airbnb-onepage/` to the Gunicorn app running on
  port `5000`.

* **3. Add a route with query parameters**
  * [3-app_server-nginx_config](./3-app_server-nginx_config): Nginx configuration file
  proxying requests on the route `/airbnb-dynamic/number_odd_or_even/<int: num>` to the
  Gunicorn app running on port `5000`.

* **4. Let's do this for your API**
  * In this task, I configured the API from my [AirBnB_clone_v3](./https://github.com/Ostoyae/AirBnB_clone_v3) to run on Gunicorn.
  * [4-app_server-nginx_config](./4-app_server-nginx_config): Nginx configuration file
  that proxies requests on the AirBnB API to the corresponding Gunicorn app.

* **5. Serve your AirBnB clone**
  * In this task, I configured the complete AirBnB app from [AirBnB_clone_v4](https://github.com/bdbaraban/AirBnB_clone_v4) to run on Gunicorn and be served through Nginx.
  * [5-app_server-nginx_config](./5-app_server-nginx_config): Nginx configuration file
  configured to serve the static assets from `web_dynamic/static/` on the Gunicorn AirBnB
  app.

* **6. Deploy it**
  * [gunicorn.service](./gunicorn.service): Configuration file for an Upstart script that starts a
  Gunicorn process bounded to port 5003 that serves the content from task 5.
  * The Gunicorn process spawns three worker processes and logs errors to `/tmp/airbnb-error.log`,
  access to `/tmp/airbnb-access.log`.

* **7. No service interruption**
  * [4-reload_gunicorn_no_downtime](./4-reload_gunicorn_no_downtime): Bash script that gracefully
  reloads Gunicorn.
