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
# - https://hub.docker.com/_/nginx
# - https://julienrenaux.fr/2013/10/04/how-to-automatically-checkout-the-latest-tag-of-a-git-repository/

FROM nginx:1.15.12-alpine

RUN apk add git yarn
RUN git clone https://github.com/bfh-proj1-sumfrie/frontend.git
# https://julienrenaux.fr/2013/10/04/how-to-automatically-checkout-the-latest-tag-of-a-git-repository/
RUN cd frontend && git fetch --tags && \
    latestTag=$(git describe --tags `git rev-list --tags --max-count=1`) && \
    git checkout $latestTag && yarn install && yarn build
RUN rm /usr/share/nginx/html/index.html && rm /usr/share/nginx/html/50x.html
RUN ls -al  /usr/share/nginx
RUN mv frontend/dist/* /usr/share/nginx/html
RUN ls -al  /usr/share/nginx/html