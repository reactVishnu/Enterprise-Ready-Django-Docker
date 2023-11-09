#Image Used is Python 3.11 and alpine is for the light weight linux system.
# Go to https://hub.docker.com/_/python for more details
FROM python:3.9-alpine3.13

# Maintainer Name, In case of enterprise level application , add the company name or email
LABEL maintainer = "reactVishnu"

# For not delaying the output
ENV PYTHONBUFFERED 1

COPY ./requirements.txt /tmp/requirements.txt
COPY ./my_project /my_project
WORKDIR /my_project
EXPOSE 8000


# The below command only include one RUN statements as we don't want them to run again and again
# as it slow downs the building process
# We creating virtual enviroment for our image as we want to isolate our dependency
# from the actual image to the project virtual enviroment. But feel free to skip if
# you don't think you want create.
# 3rd line - Upgrading the pip for our virtual enviroment
# 4th line - Removing the temp folder as we don't require any requirements file after
#   installation
# 5th line - Adding user with no password and don't create home directory.
# It will help if our application got compromised, the user will not going to have root
# priviledges.

RUN python -m venv /py && \
    /py/bin/pip install --upgrade pip && \
    /py/bin/pip install -r /tmp/requirements.txt && \
    rm -rf /tmp && \
    adduser \
      --disabled-password \
      --no-create-home \
      reactVishnu


# Enviroment variable as we don't need to specify the virtual enviroment path while launching the command
ENV PATH="/py/bin:$PATH"

# Switching b/w the user from root to the user we created by RUN command
USER reactVishnu