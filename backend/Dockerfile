# Author: Elias Summermatter & Jan Friedli
# Date: 28.05.2019
# Licence:
# This file is part of BloSQL.
# BloSQL is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
# BloSQL is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# You should have received a copy of the GNU General Public License
# along with BloSQL.  If not, see <http://www.gnu.org/licenses/>.
# Code partly adapted from:
# - https://netdevops.me/2017/flask-application-in-a-production-ready-container/

FROM alpine

RUN apk add --no-cache \
    python3 \
    bash \
    git  \
    nginx \
    uwsgi \
    uwsgi-python3 \
    supervisor && \
    python3 -m ensurepip

RUN mkdir /app && git clone https://github.com/bfh-proj1-sumfrie/backend.git /app
RUN cd /app && git fetch --tags && latestTag=$(git describe --tags `git rev-list --tags --max-count=1`) && git checkout $latestTag

RUN rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    pip3 install -r /app/requirements.txt && \
    rm /etc/nginx/conf.d/default.conf && \
    rm -r /root/.cache

# Copy the Nginx global conf
COPY nginx.conf /etc/nginx/
# Copy the Flask Nginx site conf
COPY flask-site-nginx.conf /etc/nginx/conf.d/
# Copy the base uWSGI ini file to enable default dynamic uwsgi process number
COPY uwsgi.ini /etc/uwsgi/
# Custom Supervisord config
COPY supervisord.conf /etc/supervisord.conf

WORKDIR /app

CMD ["/usr/bin/supervisord"]